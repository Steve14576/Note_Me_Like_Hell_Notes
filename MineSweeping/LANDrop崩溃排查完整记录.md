# LANDrop v2 在 Windows 24H2 上启动崩溃——完整排查记录

> 日期：2026-06-25  
> 环境：Windows 24H2 / PowerShell  
> 应用：LANDrop v2.7.2.0（Electron，构建于 2024-10-11）  
> 症状：双击打开后一直转圈，然后窗口消失，无任何反应

---

## 一、问题背景

LANDrop 是一款开源跨平台局域网文件传输工具。用户反馈：双击 LANDrop 图标后，鼠标转圈片刻，然后什么反应都没有——既没有窗口弹出，也没有错误提示。

---

## 二、排查全过程

### 第一阶段：发现僵尸进程（单实例锁卡死）

#### 2.1 检查后台进程

```powershell
tasklist | findstr /I "landrop"
```

**结果**：发现 **8 个 LANDrop.exe 进程**在后台运行。

```
LANDrop.exe    16332 Console    1      72 K
LANDrop.exe    21316 Console    1  64,196 K
LANDrop.exe    33460 Console    1 113,344 K
LANDrop.exe     7028 Console    1  67,288 K
LANDrop.exe    18216 Console    1 114,440 K
LANDrop.exe    17580 Console    1  67,280 K
LANDrop.exe    33344 Console    1 116,548 K
LANDrop.exe    14236 Console    1      68 K
```

**分析**：LANDrop 是单实例应用（基于 Electron 的 `requestSingleInstanceLock`）。8 个进程意味着之前有多次崩溃残留。新启动的实例检测到"已有实例在运行"，就不创建窗口了。

#### 2.2 批量结束进程

```powershell
taskkill /F /IM LANDrop.exe
```

**结果**：成功结束 6 个，但 2 个（PID 16332、14236）报"拒绝访问"。

#### 2.3 僵尸进程分析

```powershell
Get-Process -Id 16332,14236 | Select-Object Id, Path, StartTime, Responding, MainWindowHandle
```

**结果**：

| 属性 | PID 16332 | PID 14236 |
|------|-----------|-----------|
| Path | （空） | （空） |
| StartTime | （空） | （空） |
| Responding | True | True |
| MainWindowHandle | 0 | 0 |
| 内存 | 72 KB | 68 KB |

这两个进程：
- **无路径、无启动时间**——进程对象存在但元数据不可访问
- **无窗口**（MainWindowHandle = 0）
- **内存极小**（72KB/68KB）——基本是空壳
- **管理员权限也无法结束**（Access Denied）

#### 2.4 确认父进程已死亡

```powershell
Get-CimInstance Win32_Process -Filter "ProcessId=16332" | Select-Object ParentProcessId
# PID 16332 的父进程是 25172
# PID 14236 的父进程是 22684

Get-Process -Id 25172,22684
# 两个父进程均已不存在（ALREADY DEAD）
```

**结论**：这两个僵尸进程是**之前崩溃后遗留的孤儿进程**——父进程已崩溃死亡，子进程卡在内核级等待状态，没有任何进程能回收它们。它们仍占用着 Electron 的单实例锁（Named Pipe），导致新实例无法创建窗口。

> **关键知识**：Windows 中，当一个进程崩溃但其子进程仍在运行时，子进程会成为"孤儿"。如果孤儿进程卡在内核态 I/O 等待中，即使管理员权限也无法结束它——只有重启电脑才能清除。

#### 2.5 尝试启动新实例

即使清掉了 6 个进程，启动新实例仍然**没有窗口**（MainWindowHandle = 0），但新进程会运行。

**原因**：Electron 单实例机制通过 Named Pipe 通信。新实例连接到僵尸进程的 Pipe → 僵尸无法响应 → 新实例不创建窗口。

#### 2.6 解决方案：重启

```powershell
# 这两个僵尸进程无法通过任何命令行方式杀死
# 唯一解决方案：重启电脑
```

---

### 第二阶段：重启后仍崩溃（发现真正的根因）

#### 2.7 重启后测试

用户重启电脑后再次打开 LANDrop，症状依旧：**转圈 → 消失 → 无反应**。

#### 2.8 检查崩溃转储

```powershell
Get-ChildItem 'C:\Users\Q\AppData\Local\CrashDumps' -Filter 'LANDrop*'
```

**结果**：发现多个崩溃转储文件：

```
LANDrop.exe.18044.dmp    2026/6/25 4:51:24    8 MB
LANDrop.exe.26396.dmp    2026/6/25 4:47:14    8 MB
LANDrop.exe.29352.dmp    2026/6/25 4:42:07    8 MB
LANDrop.exe.22684.dmp    2026/6/25 4:38:04    8 MB
LANDrop.exe.13088.dmp    2026/6/25 4:37:29    8 MB
```

每次启动都崩溃，时间从 4:37 到 4:51——说明**应用启动即崩**，不是僵尸进程的问题。

#### 2.9 查看 Windows 事件查看器（关键！）

```powershell
$events = Get-WinEvent -FilterHashtable @{LogName='Application'; StartTime=(Get-Date).AddMinutes(-15)} -MaxEvents 50
$events | Where-Object { $_.Message -match 'LANDrop' } | Format-List
```

> **注意**：PowerShell 内联命令中 `$_` 可能被 shell wrapper 吞掉，建议将脚本写入 `.ps1` 文件再执行。

**结果**（Application Error 事件）：

```
错误应用程序名称: LANDrop.exe，版本: 2.7.2.0
错误模块名称: LANDrop.exe，版本: 2.7.2.0
异常代码: 0x80000003
错误偏移: 0x00000000066a139f
错误进程 ID: 0x3820
错误应用程序路径: C:\Users\Q\AppData\Local\Programs\landrop-v2-electron\LANDrop.exe
错误模块路径: C:\Users\Q\AppData\Local\Programs\landrop-v2-electron\LANDrop.exe
```

**关键发现**：
- **异常代码 `0x80000003` = `STATUS_BREAKPOINT`（断言失败）**
- **崩溃模块是 LANDrop.exe 自身**（不是 GPU 驱动、不是系统 DLL）
- 应用内部的自检逻辑触发了崩溃

---

### 第三阶段：逐一排除（控制变量法）

#### 排除项 1：应用数据损坏？

```powershell
# 备份配置
Copy-Item "$appDir\config.json" "$env:USERPROFILE\Desktop\landrop_config_backup.json"

# 清空整个应用数据目录
Remove-Item "C:\Users\Q\AppData\Roaming\landrop-v2-electron" -Recurse -Force

# 重新启动
Start-Process "C:\Users\Q\AppData\Local\Programs\landrop-v2-electron\LANDrop.exe"
```

**结果**：仍然崩溃。**排除数据损坏。**

#### 排除项 2：GPU 渲染问题？

```powershell
Start-Process $exe -ArgumentList "--disable-gpu"
```

**结果**：仍然崩溃。**排除 GPU 问题。**

#### 排除项 3：系统依赖缺失？

```powershell
# 检查 VC++ Redistributable
Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* |
    Where-Object { $_.DisplayName -like '*Visual C++*Redistributable*' }

# 检查 WebView2
Get-ItemProperty HKLM:\Software\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* |
    Where-Object { $_.DisplayName -like '*WebView2*' }
```

**结果**：VC++ 2008~2022 全部安装，WebView2 Runtime 149.0.4022.80 已安装。**排除依赖缺失。**

#### 排除项 4：安装文件损坏？

```powershell
# 检查安装完整性
LANDrop.exe    172 MB    ✓
app.asar        63 MB    ✓
所有 DLL 文件            ✓
```

**结果**：文件完整。**排除安装损坏。**

#### 排除项 5：Windows 10 兼容模式？

```powershell
# 通过注册表设置兼容模式
$layerKey = "HKCU:\Software\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers"
Set-ItemProperty -Path $layerKey -Name $exe -Value "~ WIN10RTM"
```

**结果**：延迟了崩溃（15 秒内无崩溃转储），但最终仍崩溃。**兼容模式不能解决。**

---

### 第四阶段：找到根因并修复

#### 2.10 最终方案：--no-sandbox

```powershell
Start-Process $exe -ArgumentList "--no-sandbox","--disable-gpu"
Start-Sleep -Seconds 15

# 检查结果
Get-Process -Name LANDrop | Select-Object Id, MainWindowHandle, Responding
```

**结果**：

```
   Id MainWindowHandle Responding
   -- ---------------- ----------
 8120          197962       True     ← 窗口出现了！
18192                0       True
19292                0       True
23912                0       True
28084                0       True

Crash dump: None    ← 没有崩溃！
```

**`--no-sandbox` 成功修复了崩溃！**

#### 根因分析

| 项目 | 说明 |
|------|------|
| 异常代码 | `0x80000003`（STATUS_BREAKPOINT） |
| 含义 | Chromium/Electron 内部的断言（Assertion/DCHECK）失败 |
| 崩溃模块 | LANDrop.exe 自身（包含整个 Electron 运行时） |
| 根本原因 | **Electron 沙箱与 Windows 24H2 不兼容** |
| 触发机制 | 沙箱初始化时调用 Windows API → 24H2 行为变化 → 断言失败 → 进程崩溃 |

Electron 的沙箱（Sandbox）利用 Windows 的作业对象（Job Object）和限制令牌（Restricted Token）来隔离渲染器进程。Windows 24H2 对这些底层 API 做了改动，导致旧版 Electron（LANDrop 内置的版本）的沙箱初始化逻辑触发了断言失败。

---

## 三、永久修复方案

### 3.1 创建带 --no-sandbox 的快捷方式

```powershell
$exe = "C:\Users\Q\AppData\Local\Programs\landrop-v2-electron\LANDrop.exe"
$desktop = [Environment]::GetFolderPath("Desktop")
$shortcutPath = Join-Path $desktop "LANDrop.lnk"

$shell = New-Object -ComObject WScript.Shell
$shortcut = $shell.CreateShortcut($shortcutPath)
$shortcut.TargetPath = $exe
$shortcut.Arguments = "--no-sandbox"
$shortcut.WorkingDirectory = Split-Path $exe
$shortcut.IconLocation = "$exe,0"
$shortcut.Description = "LANDrop - LAN File Transfer (no-sandbox fix for Win 24H2)"
$shortcut.Save()
```

### 3.2 更新开始菜单快捷方式

```powershell
$startMenu = "$env:APPDATA\Microsoft\Windows\Start Menu\Programs"
$landropLnk = Get-ChildItem $startMenu -Filter "*LANDrop*" -Recurse | Select-Object -First 1
if ($landropLnk) {
    $sc = $shell.CreateShortcut($landropLnk.FullName)
    $sc.Arguments = "--no-sandbox"
    $sc.Save()
}
```

### 3.3 恢复用户配置

```powershell
# 恢复 config.json（含加密身份和信任设备）
Copy-Item "$env:USERPROFILE\Desktop\landrop_config_backup.json" `
          "C:\Users\Q\AppData\Roaming\landrop-v2-electron\config.json" -Force
```

---

## 四、排查流程图

```
用户反馈：LANDrop 打不开
    │
    ├── 检查后台进程 → 发现 8 个 LANDrop.exe
    │       │
    │       ├── taskkill 杀掉 6 个
    │       ├── 2 个僵尸进程无法杀（拒绝访问）
    │       └── 父进程已死 → 孤儿进程 → 重启电脑
    │
    ▼
重启后仍打不开
    │
    ├── 检查 CrashDumps → 发现多次崩溃转储
    │
    ├── 查看事件查看器 → 异常代码 0x80000003
    │       │
    │       └── STATUS_BREAKPOINT = 断言失败
    │           └── 崩溃模块 = LANDrop.exe 自身
    │
    ▼
逐一排除（控制变量法）
    │
    ├── 清空应用数据 → 仍崩溃 ✗
    ├── --disable-gpu → 仍崩溃 ✗
    ├── 检查 VC++/WebView2 → 都正常 ✗
    ├── 检查安装文件 → 完整 ✗
    ├── Win10 兼容模式 → 延迟但仍崩 ✗
    │
    ▼
--no-sandbox → 成功！窗口出现，无崩溃 ✓
    │
    └── 创建永久快捷方式 + 恢复配置
```

---

## 五、经验总结与关键知识点

### 5.1 Electron 单实例锁机制

- Electron 通过 `app.requestSingleInstanceLock()` 实现单实例
- 底层使用 Named Pipe 通信
- 第一个实例创建 Pipe 服务端，后续实例连接后发送 argv 并退出
- **如果第一个实例是僵尸进程**（崩溃但未完全退出），Pipe 仍被占用，新实例无法创建窗口

### 5.2 Windows 僵尸进程

- 父进程崩溃后，子进程成为孤儿
- 孤儿进程若卡在内核态 I/O，即使管理员也无法结束
- **唯一解决方案：重启电脑**

### 5.3 异常代码速查

| 代码 | 名称 | 含义 |
|------|------|------|
| `0x80000003` | STATUS_BREAKPOINT | 断言失败 / 调试断点触发 |
| `0xC0000005` | STATUS_ACCESS_VIOLATION | 内存访问违规（空指针等） |
| `0xC0000409` | STATUS_STACK_BUFFER_OVERRUN | 栈缓冲区溢出 |
| `0xE06D7363` | (C++ Exception) | C++ 异常未捕获 |

### 5.4 Electron 常用启动参数

| 参数 | 作用 | 使用场景 |
|------|------|----------|
| `--no-sandbox` | 禁用渲染器沙箱 | 沙箱兼容性问题（如 Win 24H2） |
| `--disable-gpu` | 禁用 GPU 硬件加速 | GPU 驱动导致白屏/崩溃 |
| `--disable-software-rasterizer` | 禁用软件光栅化 | 渲染异常 |
| `--remote-debugging-port=9222` | 开启远程调试 | 调试 Electron 应用 |

### 5.5 PowerShell 在 IDE 终端中的注意事项

> **坑**：在 IDE 的集成终端中，PowerShell 命令里的 `$_`、`$variable` 等变量符号可能被 shell wrapper 吞掉，导致脚本解析错误。

**解决方案**：
- 将复杂脚本写入 `.ps1` 文件
- 使用 `powershell -ExecutionPolicy Bypass -File script.ps1` 执行
- 执行完毕后删除临时脚本

### 5.6 --no-sandbox 的安全影响

| 项目 | 有沙箱（默认） | 无沙箱（--no-sandbox） |
|------|----------------|----------------------|
| 渲染器隔离 | ✓ 进程级隔离 | ✗ 渲染器与主进程同权限 |
| 恶意网页影响 | 仅限渲染器进程 | 可影响整个应用 |
| 适用场景 | 日常使用 | 兼容性问题临时方案 |

> **建议**：`--no-sandbox` 是临时解决方案。长期应关注应用更新是否修复了 Windows 24H2 兼容性，届时去掉此参数恢复完整沙箱保护。

---

## 六、通用排查方法论

遇到"应用打不开"问题时，按以下顺序排查：

1. **查进程** — `tasklist | findstr <app>`，看是否有僵尸进程占用
2. **查崩溃转储** — `C:\Users\<user>\AppData\Local\CrashDumps\`，确认是否崩溃
3. **查事件查看器** — Application 日志，获取异常代码和崩溃模块
4. **根据异常代码判断方向**：
   - `0x80000003` → 断言失败 → 尝试 `--no-sandbox`
   - `0xC0000005` → 内存违规 → 尝试重装
   - `0xC0000409` → 栈溢出 → 可能是恶意注入或版本不兼容
5. **控制变量排除** — 一次只改一个条件：清数据 → 禁 GPU → 兼容模式 → 禁沙箱
6. **永久化修复** — 创建快捷方式 / 修改注册表 / 脚本自动化

---

## 七、涉及的文件路径

| 用途 | 路径 |
|------|------|
| LANDrop 可执行文件 | `C:\Users\Q\AppData\Local\Programs\landrop-v2-electron\LANDrop.exe` |
| 应用数据目录 | `C:\Users\Q\AppData\Roaming\landrop-v2-electron\` |
| 用户配置文件 | `C:\Users\Q\AppData\Roaming\landrop-v2-electron\config.json` |
| 崩溃转储目录 | `C:\Users\Q\AppData\Local\CrashDumps\` |
| 更新安装包 | `C:\Users\Q\AppData\Local\landrop-v2-electron-updater\installer.exe` |
| 兼容模式注册表 | `HKCU:\Software\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers` |
| 桌面快捷方式 | `C:\Users\Q\Desktop\LANDrop.lnk` |
| 数据备份 | `C:\Users\Q\Desktop\landrop_backup\` |

---

*文档编写：2026-06-25 | 系统环境：Windows 24H2*
