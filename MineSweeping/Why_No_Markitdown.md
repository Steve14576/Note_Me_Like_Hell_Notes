# office-doc-skill 设计决策与经验沉淀

## 一、核心哲学：读求准，分析求轻，写求准

整个 skill 的设计围绕一个认知展开：

- **读阶段追求"准"**：用原生库读结构化对象（段落/表格/单元格/形状），保留完整信息。markitdown 转 MD 是有损中间层（丢嵌套层级、丢格式元数据），只在批量只读分析时当捷径用。
- **改阶段分两种**：精确修改在原生对象上操作（保结构保样式）；只读分析提取文本后做字符串/LLM 操作。
- **写阶段追求"准"**：原生库在原对象上改后保存，或新建。不再从 MD 解析重建。

这个取舍来自一个关键洞察：**MD 是有损中间层，精确修改不该过它；但 agent 能自己写原生遍历，skill 教对错案例即可。** markitdown 的窄价值只剩批量只读分析。

---

###### 二、为什么主路径选原生库，markitdown 降为可选

### markitdown 曾是默认入口，现在降级——因为它是"有损中间层"

markitdown 是微软开源、维护多年的通用转换器，内部确实兜了不少边缘 case：

| 格式  | markitdown 内部实现                     | 兜了什么                                |
| ----- | --------------------------------------- | --------------------------------------- |
| .docx | mammoth → HTML → MD                   | 文本框、目录、批注区域、MathML          |
| .xlsx | pandas + openpyxl，**全部 sheet** | 空行过滤、多 sheet 分节、None→空字符串 |
| .pptx | python-pptx 直调                        | 表格、图表数据、组形状递归、演讲者备注  |
| .pdf  | pdfplumber + pdfminer                   | 无边框表格识别、列聚类                  |

但实测暴露了它的本质问题——**MD 是有损中间层**：

- **丢嵌套列表层级**：List Bullet 2 被拍平成平级 `*`，手写完整遍历反而能保缩进
- **丢格式元数据**：字体、颜色、对齐、列宽转 MD 全消失
- **丢结构定位**：单元格坐标、形状层级被扁平化，精确修改场景帮倒忙
- **PDF 多栏乱序**：坐标启发式算法对多栏混排可能读乱

而且 examples 自己就叛变了：Example 2（Excel 改数据）、Example 4（PDF 表格）都绕过 markitdown 直接走原生库——真要精确操作，markitdown 帮不上忙。

### 为什么原生库更适合当主路径

- **结构化对象 > 扁平文本**：原生库给 paragraph/table/cell/shape 对象，信息量大于 MD
- **agent 能自己写遍历**：现代 LLM 写 python-docx 遍历 paragraphs+tables 完全没问题，skill 教对错案例即可，不需要 markitdown 替它嚼碎
- **精确修改不过有损中间层**：在原对象上改后保存，结构样式都保住

### markitdown 降为"批量只读分析可选捷径"

它只剩一个场景站得住：批量只读分析（Example 5：50 份简历找关键词）。这种"只要文本、不要结构、不写回"的懒人快读，markitdown 一行 `convert` 省得每种格式写遍历。

**0.1.x extras 坑仍在**：裸 `pip install markitdown` 能 import 但 `convert()` 抛 `MissingDependencyException`，必须 `markitdown[docx,xlsx,pptx,pdf]`。

### PDF 用原生

PDF 文本用 PyMuPDF (`fitz`) 直读，表格用 pdfplumber。不走 markitdown。

---

## 三、为什么不用 LibreOffice 大一统

LibreOffice 在命令行下只有一种能力：**整个文件格式互转**。`soffice --headless --convert-to docx old.doc` ——仅此而已。

它没有细粒度 API。你不能让它"读第三段加粗"、"提取表格数据"、"替换所有占位符"。UNO API 理论上可以，但复杂度是 python-docx 的 10 倍，没人这么用。

更致命的：每个文件启动一次 soffice 进程（2-3 秒），并发会 profile lock 冲突，Docker/服务器部署要装 300MB GUI 套件+虚拟显示。

**LibreOffice 的定位：兜底老格式。** .doc / .ppt / .odt 这些 Python 库不碰的古董，用它转成 .docx 再进入正常流程。

---

## 四、写回为什么必须用原生库

markitdown 是单向的。它能把 .docx → MD，但**不能把 MD → .docx**。LibreOffice 也不能——它都不认识 .md。

所以 markitdown + LibreOffice 的组合，只能做"读→分析"的只读链路。一旦要改完再写回原格式，就必须走原生库：

| 写回目标 | 工具                             |
| -------- | -------------------------------- |
| .docx    | python-docx                      |
| .xlsx    | openpyxl / xlsxwriter / pandas   |
| .pptx    | python-pptx                      |
| .pdf     | PyMuPDF（操作原文件，不经过 MD） |

---

## 五、格式元数据的取舍

### 什么是格式元数据？

一段 "Hello" 在 .docx 里包含两层信息：

```
内容层："Hello"                           ← 你要改的
元数据层：字体=Arial, 14pt, 加粗, 蓝色     ← 文档的衣服
         行距1.5, 首行缩进2字符
         段落样式=Heading1
```

markitdown 脱掉衣服，只留内容。原生库能看到衣服。

### 什么时候要衣服？

| 场景                   | 要元数据吗 |
| ---------------------- | :--------: |
| 改一个数字、替换公司名 | ❌ 不关心 |
| 翻译内容               | ❌ 不关心 |
| 搜索关键词             | ❌ 不关心 |
| 用户说"保持原格式不变" |   ✅ 要   |

### 保形写回的方案

Phase 1 可选做一次"格式快照"——用原生库读一遍，记录每个段落的样式信息。Phase 3 写回时用快照还原样式。

这是按需激活的，不是默认路径。开销只在用户明确要"保留格式"时才产生。

---

## 六、技术栈选型理由

| 领域     | 选了                  | 没选                   | 理由                                      |
| -------- | --------------------- | ---------------------- | ----------------------------------------- |
| Excel 读 | openpyxl / pandas     | —                     | pandas 保留数据类型，openpyxl 保留样式    |
| Excel 写 | openpyxl + xlsxwriter | xlwt                   | xlsxwriter 图表/条件格式最强，xlwt 已淘汰 |
| Word     | python-docx           | mammoth / textract     | 唯一能读写 .docx 的 Py 库                 |
| PPT      | python-pptx           | —                     | 唯一选择                                  |
| PDF 主力 | PyMuPDF (fitz)        | pypdf / pikepdf        | C 后端，速度碾压纯 Python                 |
| PDF 表格 | pdfplumber            | camelot / tabula       | 纯 Python，不需要 Java/Ghostscript        |
| 格式转换 | markitdown            | docling / unstructured | 轻量，不依赖 GPU                          |
| 老格式   | LibreOffice headless  | —                     | Python 库不碰 .doc/.ppt                   |

每个领域只选一个最优解，不做备胎堆砌。

---

## 七、任务分流工作流

```
精确修改/写回   ──→  原生库读改写 (对象级, 不过 MD)
只读分析/翻译    ──→  原生库读内容 / 提取文本
批量只读分析     ──→  markitdown 可选捷径 (省遍历)

特殊情况：
- PDF → PyMuPDF 读文本 / pdfplumber 读表格, 不走 markitdown
- 用户要"保持格式" → 原生库做格式快照, 写回时还原
- 老 .doc/.ppt → LibreOffice 转 .docx 再进原生库
- 扫描件 → OCR（easyocr/PaddleOCR）
```

---

## 八、跨平台坑点

### Windows GBK 编码

Windows 终端默认 GBK，Python print Office 文档内容（含中文、特殊符号）会崩：

- **不打印到终端**，写入 UTF-8 文件
- Python 脚本用 `encoding="utf-8"` 读写
- .md 文件统一 UTF-8

### Windows 不支持 emoji

终端 print emoji → `UnicodeEncodeError`：

- 用纯 ASCII 标记替代：`[OK]` 而非 `✅`，`[MISSING]` 而非 `❌`

### PowerShell 引号

含双引号的 Python 命令在 PowerShell 中失败：

- `python -c "..."` → `python -c '...'`（外层单引号）

### Read 工具不支持 Office

Qoder 的 `Read` 工具对 .docx/.xlsx/.pptx 返回 40400：

- Office 文件只能用 Python 脚本读，不能直接 Read

---

## 九、依赖管理规范

项目有 `pyproject.toml`：

1. `uv venv --python 3.13` 创建虚拟环境
2. `uv sync` 安装依赖
3. `uv run python script.py` 运行
4. 添加新依赖用 `uv add <package>`

临时系统级：`uv pip install --system <package>`（仅无 pyproject 时）

---

## 十、Skill 文件结构

```
office-doc-skill/
├── SKILL.md           ← Agent 主指令：SOP、边界应对、对错示例
├── examples.md        ← 端到端链路示例（翻译/改数据/替换/PDF表格/批量分析）
├── DESIGN.md          ← 本文档：设计决策与经验沉淀
└── scripts/
    └── validate_env.py ← 环境自检脚本
```
