# ray-skills

收集整理的一些在 Windows 环境下运行 AI 常用 Skills 和 MCP 配置。

---

## 目录结构

```text
ray-skills/
|-- accidental-data-loss-prevention/  # 高危删除与截断操作拦截
|-- docx-gem/                         # Word 文档处理（XML 级编辑与格式校验）
|-- find-skills/                      # 社区技能生态检索与安装工具
|-- frontend-design/                  # 前端设计风格与界面规范
|-- geomaster/                        # GIS 与遥感科研工作流
|-- humanizer/                        # 英文文本去 AI 腔调与自然润色
|-- humanizer-zh/                     # 中文文本去套话与表达润色
|-- pdf/                              # PDF 提取、表单填写与页面操作
|-- pdf-gem/                          # PDF 高精度表单填写与校验工具
|-- performance/                      # 前端性能分析与 Web Vitals 优化
|-- planning-with-files/              # 本地文件长任务规划与进度跟踪
|-- pptx-gem/                         # PowerPoint 幻灯片排版与自动生成
|-- python-code-style/                # Python 代码规范与格式化标准
|-- python-testing-patterns/          # 基于 pytest 的单元测试模式
|-- pytorch-patterns/                 # PyTorch 训练模式与可复现工程规范
|-- skill-creator/                    # 编写与评测 Agent Skill 的规范工具
|-- ui-ux-pro-max/                    # UI/UX 设计库与组件规范
|-- xlsx-gem/                         # Excel/CSV 表格构建、公式运算与清洗
|-- .gitattributes                     # 换行符规则配置
|-- .gitignore                         # 缓存与临时文件过滤
|-- LICENSE                            # MIT 开源协议与第三方致谢
`-- README.md                          # 说明文档
```

---

## 包含的 Skills

仓库共包含 18 个技能，按使用场景分类如下：

### 1. 安全防误删
- **accidental-data-loss-prevention**
  在高危删除操作（如 `DROP TABLE`、`TRUNCATE`、无条件 `DELETE` 或全盘递归删除）前拦截并要求人工确认，防止 Agent 误删关键文件或数据库。

### 2. 任务规划与技能开发
- **planning-with-files**
  在工作目录生成并维护 `task_plan.md`、`findings.md` 和 `progress.md`，用于多步骤复杂任务的状态跟踪，防止 Agent 在长会话中遗忘进度。
- **skill-creator**
  用于创建、评测和优化 Skill，包含标准目录规范、评测集（evals）与描述词优化流程。
- **find-skills**
  通过 `skills.sh` 检索和安装社区已有的 Agent 技能。

### 3. 文本与去 AI 味
- **humanizer**
  针对英文文本，去除常见模板化句式和空话，使语言更符合自然母语习惯。
- **humanizer-zh**
  针对中文文本，消除翻译腔、官话套话和机械并列，使文笔自然通畅。

### 4. Office 与文档处理
- **docx-gem**
  Word（.docx / .dotx）新建与就地修改，内置 XML 节点级编辑与 XSD 模式校验。
- **xlsx-gem**
  Excel（.xlsx / .csv）表格处理，支持公式计算、格式化、复杂数据清洗与重新计算。
- **pptx-gem**
  PowerPoint（.pptx）演示文稿生成与修改，包含大纲排版、幻灯片布局与主题设置。
- **pdf**
  Anthropic 官方的 PDF 处理工具，支持文本提取、页面分割合并与表单填写。
- **pdf-gem**
  基于坐标与视觉校验的 PDF 表单填写与字段定位工具。

### 5. 前端与界面设计
- **ui-ux-pro-max**
  UI/UX 设计参考规范，整理了调色板、字体排版、主流前端框架组件与无障碍（WCAG）设计建议。
- **frontend-design**
  前端界面设计指导，用于构建层次清晰、细节精致的 Web 页面。
- **performance**
  Web 性能分析与优化指南，关注首屏渲染与 Core Web Vitals 指标。

### 6. Python 与科研工程
- **geomaster**
  GIS 与遥感科研工作流，支持 GDAL、Rasterio、坐标系转换、时空数据与遥感影像处理。
- **python-code-style**
  Python 代码风格、格式化规范、命名约定与文档编写标准。
- **python-testing-patterns**
  基于 pytest 的单元测试编写策略、Fixtures 组织与 Mock 测试模式。
- **pytorch-patterns**
  PyTorch 深度学习开发模式，包含随机种子设定、设备无关代码写法、显存控制与标准训练循环。

---

## Windows 常用 MCP 配置

在 Windows 环境下配合 Agent 使用时，以下几个 MCP 比较实用：

1. **codegraph**
   - 用于代码语义分析与调用关系查询，基于 AST 提取函数定义、调用者（callers）和引用，帮助 Agent 在代码库中快速定位，减少上下文开销。
   - 仓库：[colbymchenry/codegraph](https://github.com/colbymchenry/codegraph)


---

## Windows 环境

### 1. 路径斜杠与 JSON 转义
Windows 原生使用反斜杠 `\`，在 JSON 配置文件中如果写成单反斜杠（如 `"D:\tools"`），`\t` 会被当作制表符解析导致路径错误。
建议在所有配置文件中统一使用正斜杠 `/`（例如 `"D:/PClog/ray-skills"`），Windows 系统和 Node.js / Python 运行时均完全兼容。若使用反斜杠，需写成双反斜杠 `\\`。

### 2. 控制台编码与中文乱码
中文版 Windows 的 CMD / PowerShell 默认代码页一般是 936 (GBK)，当 Agent 执行命令或捕获脚本输出时，中文常会变成乱码。
解决方式：
- 设置 Python 环境变量强制使用 UTF-8：`$env:PYTHONUTF8 = "1"`
- 在 PowerShell 中临时切换代码页：`chcp 65001`
- 文本文件保存统一使用 UTF-8 编码（无 BOM）。

### 3. PowerShell 脚本权限限制
新装系统或未配置策略时，执行脚本或部分 npm 全局命令可能提示受受限策略阻止（`UnauthorizedAccess`）。
可在当前用户下放宽策略（不需要管理员权限）：
```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

### 4. POSIX Shell 脚本调用
部分来自 Linux/macOS 生态的 Skill 附带了 `.sh` 脚本（例如 `planning-with-files`）。在 Windows 下直接调用会报错找不到 `sh`。
如果需要运行这些脚本，可以安装 Git for Windows 并将其 `bin` 目录（包含 `sh.exe` 与 `bash.exe`）加入系统环境变量 PATH。

---

## 克隆仓库到本地

```powershell
git clone https://github.com/ldray857/ray-skills.git
```

## 许可证与致谢

- 本仓库整理与文档内容采用 [MIT License](LICENSE) 许可。
- 各 Skill 保持各自原作者的开源许可证，详细声明请查看根目录 [LICENSE](LICENSE) 以及各子目录下的说明。
