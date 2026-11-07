# ray-skills

收集整理的一些在 Windows 环境下运行 AI 常用 Skills 和 MCP 配置。

---

## 目录结构

```text
|-- u-skills/                         # 推荐的skills
|-- rules/                            # 一些Agent 的全局规则文件
|-- .gitattributes                     # 换行符规则配置
|-- .gitignore                         # 缓存与临时文件过滤
|-- LICENSE                            # MIT 开源协议与第三方致谢
`-- README.md                          # 说明文档
```

---

## 包含的 Skills

仓库共包含 17 个技能，按使用场景分类如下：

### 1. 安全防误删
- **accidental-data-loss-prevention**
  在高危删除操作（如 `DROP TABLE`、`TRUNCATE`、无条件 `DELETE` 或全盘递归删除）前拦截并要求人工确认，防止 Agent 误删关键文件或数据库。
  来源：[GoogleCloudPlatform/data-agent-kit-plugin](https://github.com/GoogleCloudPlatform/data-agent-kit-plugin)

### 2. 任务规划与技能开发
- **planning-with-files**
  在工作目录生成并维护 `task_plan.md`、`findings.md` 和 `progress.md`，用于多步骤复杂任务的状态跟踪，防止 Agent 在长会话中遗忘进度。
  来源：[OthmanAdi/planning-with-files](https://github.com/OthmanAdi/planning-with-files)
- **skill-creator**
  用于创建、评测和优化 Skill，包含标准目录规范、评测集（evals）与描述词优化流程。
  来源：[anthropics/skills](https://github.com/anthropics/skills) (`skills/skill-creator`)
- **find-skills**
  通过 `skills.sh` 检索和安装社区已有的 Agent 技能。
  来源：[vercel-labs/skills](https://github.com/vercel-labs/skills) (`skills/find-skills`)

### 3. 文本与去 AI 味
- **humanizer**
  针对英文文本，去除常见模板化句式和空话，使语言更符合自然母语习惯。
  来源：[blader/humanizer](https://github.com/blader/humanizer)
- **humanizer-zh**
  针对中文文本，消除翻译腔、官话套话和机械并列，使文笔自然通畅。
  来源：[op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh)

### 4. Office 与文档处理
微调后的 Office 文档处理技能（源自 Anthropic 官方 Skills）：

- **docx-gem**
  Word（.docx / .dotx）新建与就地修改，内置 XML 节点级编辑与 XSD 模式校验。
  来源：基于 [anthropics/skills](https://github.com/anthropics/skills) (`skills/docx`) 定制微调
- **xlsx-gem**
  Excel（.xlsx / .csv）表格处理，支持公式计算、格式化、复杂数据清洗与重新计算。
  来源：基于 [anthropics/skills](https://github.com/anthropics/skills) (`skills/xlsx`) 定制微调
- **pptx-gem**
  PowerPoint（.pptx）演示文稿生成与修改，包含大纲排版、幻灯片布局与主题设置。
  来源：基于 [anthropics/skills](https://github.com/anthropics/skills) (`skills/pptx`) 定制微调
- **pdf-gem**
  基于坐标与视觉校验的 PDF 表单填写与字段定位工具。
  来源：基于 [anthropics/skills](https://github.com/anthropics/skills) (`skills/pdf`) 定制微调

### 5. 前端与界面设计
- **ui-ux-pro-max**
  UI/UX 设计参考规范，整理了调色板、字体排版、主流前端框架组件与无障碍（WCAG）设计建议。
  来源：[nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)
- **frontend-design**
  前端界面设计指导，用于构建层次清晰、细节精致的 Web 页面。
  来源：[anthropics/skills](https://github.com/anthropics/skills) (`skills/frontend-design`)
- **performance**
  Web 性能分析与优化指南，关注首屏渲染与 Core Web Vitals 指标。
  来源：[addyosmani/web-quality-skills](https://github.com/addyosmani/web-quality-skills) (`skills/performance`)

### 6. Python 与科研工程
- **geomaster**
  GIS 与遥感科研工作流，支持 GDAL、Rasterio、坐标系转换、时空数据与遥感影像处理。
  来源：[K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) (`skills/geomaster`)
- **python-code-style**
  Python 代码风格、格式化规范、命名约定与文档编写标准。
  来源：[wshobson/agents](https://github.com/wshobson/agents) (`plugins/python-development/skills/python-code-style`)
- **python-testing-patterns**
  基于 pytest 的单元测试编写策略、Fixtures 组织与 Mock 测试模式。
  来源：[wshobson/agents](https://github.com/wshobson/agents) (`plugins/python-development/skills/python-testing-patterns`)
- **pytorch-patterns**
  PyTorch 深度学习开发模式，包含随机种子设定、设备无关代码写法、显存控制与标准训练循环。
  来源：[wshobson/agents](https://github.com/wshobson/agents) (`plugins/python-development/skills/pytorch-patterns`)



## 常用 MCP 配置


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
