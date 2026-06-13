# Claude Code 侧栏输入框光标不可见 — 修复报告

## 问题现象

在 VSCode / Qoder 中使用 Claude Code 侧栏插件时，输入框可以打字，但看不到光标（闪烁的竖线），不知道自己输到哪了。

## 原理分析

### 光标颜色是怎么决定的？

Claude Code 插件的输入框是一个 "webview"——本质上是插件内部嵌的一个小网页。这个网页的样式由插件自带的 CSS 文件控制。

关键的 CSS 规则在插件的 `webview/index.css` 里：

```css
.messageInput_cKsPxg {
  color: #0000;                              /* 文字颜色：全透明（不显示） */
  caret-color: var(--app-input-foreground);  /* 光标颜色：跟随变量 */
}
```

其中 `--app-input-foreground` 又在 CSS 开头定义了：

```css
html {
  --app-input-foreground: var(--vscode-input-foreground);
}
```

所以链条是这样的：

```
光标颜色 → --app-input-foreground → --vscode-input-foreground → VSCode 主题的 input.foreground 设置项
```

### 为什么看不到？

如果你的 VSCode 主题里 `input.foreground`（输入框文字颜色）和输入框背景色太接近，光标就融入背景了，肉眼看不见。

Qoder 的情况更特殊——它是一个 VSCode 的魔改版，webview 里可能没有正确传递 `--vscode-input-foreground` 这个变量，导致变量值为空或者默认为黑色，在深色背景上自然看不见。

## 修复方法

### 方法一：改 VSCode / Qoder 设置（推荐，不改插件文件）

在 `settings.json` 里加一段，强制指定输入框前景色：

```json
"workbench.colorCustomizations": {
  "input.foreground": "#e0e0e0"
}
```

- **VSCode**：有效，已验证。改完重启即可。
- **Qoder**：无效。Qoder 的 webview 没有正确读取这个设置项。

设置文件位置：

- VSCode：`C:\Users\<你的用户名>\AppData\Roaming\Code\User\settings.json`
- Qoder：`C:\Users\<你的用户名>\AppData\Roaming\Qoder\User\settings.json`

### 方法二：直接改插件 CSS（万能，但插件更新后会丢失）

把光标颜色从"跟随变量"改成硬编码的颜色值。

**步骤：**

1. 找到插件的 CSS 文件：
   - VSCode：`C:\Users\<你的用户名>\.vscode\extensions\anthropic.claude-code-<版本号>\webview\index.css`
   - Qoder 用户对应路径是 `.qoder\extensions\`。

2. 用文本编辑器打开 `index.css`（这个文件是压缩成一行的大文件，很正常）。

3. 全局搜索替换：
   - 查找：`caret-color:var(--app-input-foreground)`
   - 替换为：`caret-color:#e0e0e0`

4. 保存，重启编辑器。

**注意事项：**

- 插件更新后这个文件会被覆盖，需要重新改。
- `#e0e0e0` 是浅灰色，深色主题下可见。如果你用浅色主题，改成 `#333333` 之类的深色。
- 这个文件里只有一处 `caret-color:var(--app-input-foreground)`，替换不会影响其他东西。

## 总结

|          | VSCode | Qoder |
|----------|--------|-------|
| 改 settings.json | 有效 | 无效 |
| 改插件 CSS       | 有效 | 有效 |

根本原因是插件把光标颜色绑定到了一个编辑器主题变量上，但这个变量在某些主题或魔改编辑器下解析出来的值和背景色撞了。本质上是 Anthropic 那边应该加个 fallback 值，比如：

```css
caret-color: var(--vscode-input-foreground, #e0e0e0);
```
