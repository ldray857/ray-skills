# ray-skills: Windows 环境 Agent 优质 Skills 与 MCP 精选实战指南

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Platform: Windows](https://img.shields.io/badge/Platform-Windows%2010%20%2F%2011-0078D6.svg)](https://microsoft.com/windows)
[![Agent: Antigravity | Claude | Cline](https://img.shields.io/badge/Agent-Antigravity%20%7C%20Claude%20%7C%20Cline-8A2BE2.svg)](#)

本项目是一套面向 **Windows 开发者与 Agent 用户** 精心整理与调优的智能体扩展资源库，涵盖 **核心 Skills（智能体技能）**、**优选 MCP（模型上下文协议）服务器** 以及专门针对 **Windows 操作系统运行 Agent 的实战避坑与配置指南**。

适用于 Google Antigravity、Claude Desktop、Cline、Roo Code、Cursor 等支持 Skills 或 MCP 协议的主流智能体应用。

---

## 目录

- [一、项目结构](#一项目结构)
- [二、精选 Skills 清单与解析](#二精选-skills-清单与解析)
  - [1. 系统安全与防灾](#1-系统安全与防灾)
  - [2. 任务规划与生态扩展](#2-任务规划与生态扩展)
  - [3. 文案润色与去 AI 感](#3-文案润色与去-ai-感)
  - [4. Office 与电子文档处理](#4-office-与电子文档处理)
  - [5. 前端架构与 UI/UX 体验](#5-前端架构与-uiux-体验)
  - [6. Python 与深度学习工程](#6-python-与深度学习工程)
- [三、Windows 优选 MCP 推荐与配置模版](#三windows-优选-mcp-推荐与配置模版)
  - [1. 代码架构分析: codegraph](#1-代码架构分析-codegraph)
  - [2. Windows 全盘秒级检索: everything-mcp](#2-windows-全盘秒级检索-everything-mcp)
  - [3. 文件系统访问: @modelcontextprotocol/server-filesystem](#3-文件系统访问-modelcontextprotocolserver-filesystem)
  - [4. 客户端配置模板示例](#4-客户端配置模板示例)
- [四、Windows 运行 Agent 实战避坑指南](#四windows-运行-agent-实战避坑指南)
  - [1. 路径反斜杠转义与正斜杠推荐](#1-路径反斜杠转义与正斜杠推荐)
  - [2. 终端编码与 UTF-8 强制规范](#2-终端编码与-utf-8-强制规范)
  - [3. PowerShell 执行策略配置](#3-powershell-执行策略配置)
  - [4. POSIX Shell 钩子脚本在 Windows 上的适配](#4-posix-shell-钩子脚本在-windows-上的适配)
- [五、安装与使用方式](#五安装与使用方式)
- [六、开源协议与版权致谢](#六开源协议与版权致谢)

---

## 一、项目结构

```text
ray-skills/
|-- accidental-data-loss-prevention/  # [安全防灾] 高危删除/截断操作确认拦截器
|-- find-skills/                       # [通用扩展] 开放技能生态检索与安装工具
|-- frontend-design/                   # [前端设计] 高审美、反平庸的前端界面指导规范
|-- humanizer/                         # [写作润色] 英文去 AI 味与自然书写转换
|-- humanizer-zh/                      # [写作润色] 中文去模板化与通畅表达优化
|-- pdf/                               # [文档处理] PDF 提取、表单填写与页面操作工具
|-- performance/                       # [前端调优] Web 性能审计与 Core Web Vitals 优化
|-- planning-with-files/               # [长程规划] 磁盘持久化多步骤研发任务规划
|-- pytorch-patterns/                  # [深度学习] PyTorch 训练、数据管道与可复现模式
|-- skill-creator/                     # [技能开发] 编写、评测与调优 Agent Skill 标准套件
|-- ui-ux-pro-max/                     # [全栈界面] UI/UX 风格、调色板、无障碍系统规范
|-- .gitattributes                     # 跨平台换行符规范配置
|-- .gitignore                         # Windows/Python/Node 缓存与忽略规则
|-- LICENSE                            # MIT 开源协议与第三方致谢
`-- README.md                          # 本说明文档
```

---

## 二、精选 Skills 清单与解析

### 1. 系统安全与防灾

- **accidental-data-loss-prevention**
  - **来源**：Google Internal / Antigravity Built-in
  - **功能**：高危删除与破坏性操作拦截器。在智能体尝试执行如 `DROP TABLE`、`TRUNCATE`、无条件 `DELETE`、云存储清空或本地系统级递归强制删除命令前，强制中断执行并向用户请求显式授权确认。
  - **Windows 场景价值**：Windows 下 PowerShell 的 `Remove-Item -Recurse -Force` 不经过回收站，一旦 Agent 误判可能造成灾难性数据丢失，本技能是 Windows 平台保命必备。

### 2. 任务规划与生态扩展

- **planning-with-files**
  - **来源**：[othmanadi/planning-with-files](https://github.com/othmanadi/planning-with-files)
  - **功能**：通过在工作区根目录持久化维护 `task_plan.md`、`findings.md` 和 `progress.md`，实现多轮对话中的状态记忆与计划跟踪。适用于 5 步以上工具调用的复杂工程研发。
- **skill-creator**
  - **来源**：[anthropics/skills](https://github.com/anthropics/skills)
  - **功能**：标准化创建、改进与优化 Agent Skill 的完整指南，包含编写符合规范的 `SKILL.md`、编写自动化 Evals 评测集及优化描述词触发率。
- **find-skills**
  - **来源**：[vercel-labs/skills](https://github.com/vercel-labs/skills)
  - **功能**：快速检索 skills.sh 开放生态中的现成技能，方便通过 `npx skills add` 快速扩充 Agent 功能。

### 3. 文案润色与去 AI 感

- **humanizer**
  - **来源**：[blader/humanizer](https://github.com/blader/humanizer)
  - **功能**：消除英文生成内容中的典型 AI 腔调（如 not-X-but-Y、机械的三段式、滥用破折号、空洞套话），重构为贴合自然母语者的写作风格。
- **humanizer-zh**
  - **来源**：[op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh)
  - **功能**：消除中文文本中的空话、套话、层级并列过多及机械翻译腔，保留事实与作者立场，使中文输出流畅通顺。

### 4. Office 与电子文档处理

- **pdf**（本项目已包含完整工具链）
  - **来源**：[anthropics/skills](https://github.com/anthropics/skills)
  - **功能**：PDF 结构化内容提取、复杂表格解析、页面合并与分割、表单填充、文档水印及附带的 Python 处理脚本。
- **官方生态推荐（外部拓展）**：
  - **docx**（Word 文档生成与修改，保留格式与修订）
  - **xlsx**（Excel 表格构建、复杂公式运算与清洗）
  - **pptx**（PowerPoint 自动排版、大纲生成与幻灯片构建）
  - 以上三项可直接参考或从 [anthropics/skills](https://github.com/anthropics/skills) 获取。

### 5. 前端架构与 UI/UX 体验

- **ui-ux-pro-max**
  - **来源**：[nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)
  - **功能**：全栈设计系统智库。内置数十种设计风格体系、色彩调色板规范、字体排版指南、WCAG 2.1 无障碍标准与图表规范，避免 AI 生成千篇一律的粗糙界面。
- **frontend-design**
  - **来源**：[anthropics/skills](https://github.com/anthropics/skills)
  - **功能**：指导智能体建立具备高辨识度与现代美感的前端架构，重点在微交互、视效层次与品牌一致性。
- **performance**
  - **来源**：[addyosmani/web-quality-skills](https://github.com/addyosmani/web-quality-skills)
  - **功能**：Web 性能审计调优，提供 Core Web Vitals 指标深度分析与首屏渲染优化方案。

### 6. Python 与深度学习工程

- **pytorch-patterns**
  - **功能**：PyTorch 深度学习开发规约。涵盖跨硬件无缝适配（Device-agnostic）、多随机数种子设定（全面可复现性）、显存管理与梯度优化、标准化训练循环及数据加载最佳实践。

---

## 三、Windows 优选 MCP 推荐与配置模版

MCP（Model Context Protocol）是连接大模型与本地系统的标准桥梁。在 Windows 系统下，推荐配置以下三大核心 MCP：

### 1. 代码架构分析: codegraph

- **仓库**：[colbymchenry/codegraph](https://github.com/colbymchenry/codegraph)
- **定位**：代码语义分析与调用图谱服务。
- **特点**：基于 AST 解析代码符号依赖，支持在无需让 Agent 通读全部源码的情况下，秒级查询函数定义、调用者（callers）、被调用者（callees）以及改动影响面（impact analysis），极大地节省 Token 并提升定位准确度。

### 2. Windows 全盘秒级检索: everything-mcp

- **定位**：基于 Windows 平台标杆搜索神器 **Voidtools Everything** 的 MCP 服务。
- **特点**：Windows 传统的文件遍历工具在目录深度大时非常耗时，通过 Everything 的本地索引服务，Agent 可以在几十毫秒内定位全盘任意文件、路径或正则表达式匹配项。

### 3. 文件系统访问: @modelcontextprotocol/server-filesystem

- **定位**：官方本地文件读写与目录管理服务。
- **特点**：允许 Agent 安全地在允许的本地工作区进行目录树浏览、文件读写与差异审查。

### 4. 客户端配置模板示例

以下为 Windows 环境下的标准配置片段，适用于 Claude Desktop（`%APPDATA%\Claude\claude_desktop_config.json`）、Antigravity 或支持 MCP 的扩展应用：

```json
{
  "mcpServers": {
    "codegraph": {
      "command": "cmd.exe",
      "args": ["/c", "npx", "-y", "@colbymchenry/codegraph"]
    },
    "everything": {
      "command": "cmd.exe",
      "args": ["/c", "npx", "-y", "everything-mcp"]
    },
    "filesystem": {
      "command": "cmd.exe",
      "args": [
        "/c",
        "npx",
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "D:/PClog",
        "D:/workspace"
      ]
    }
  }
}
```

---

## 四、Windows 运行 Agent 实战避坑指南

### 1. 路径反斜杠转义与正斜杠推荐

- **陷阱**：Windows 原生使用反斜杠 `\`。在 JSON 配置文件中，单个反斜杠会被解析为转义符，导致路径失效（例如 `D:\tools` 会被解析为制表符）。
- **规范**：
  - **推荐写法**：在所有配置文件与代码中，统一使用正斜杠 `/`（例如 `D:/PClog/ray-skills`），现代 Windows API 与主流运行库（Node.js / Python / Go）均完全支持。
  - **JSON 转义写法**：若必须使用反斜杠，务必双写转义（`D:\\PClog\\ray-skills`）。

### 2. 终端编码与 UTF-8 强制规范

- **陷阱**：中文版 Windows 的 CMD / PowerShell 默认代码页通常为 `936 (GBK)`，当 Agent 捕获终端输出或执行包含中文的文件读写时，极易产生乱码甚至解析崩溃。
- **对策**：
  - 设置 Python 环境变量启用全局 UTF-8：`$env:PYTHONUTF8=1`
  - 在 PowerShell 会话前可设置代码页：`[Console]::OutputEncoding = [System.Text.Encoding]::UTF8` 或 `chcp 65001`
  - 源码文件严格保存为无 BOM 的 UTF-8 格式。

### 3. PowerShell 执行策略配置

- **陷阱**：在未配置策略的 Windows 系统中，执行 `npx`、`.ps1` 脚本时常遇到 `UnauthorizedAccess` 或脚本禁止运行报错。
- **对策**：使用当前用户作用域放宽策略（无需管理员权限）：
  ```powershell
  Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
  ```

### 4. POSIX Shell 钩子脚本在 Windows 上的适配

- **陷阱**：部分开源技能（如 `planning-with-files`）内置了生命周期钩子脚本（`.sh` 格式），在 Windows 纯 PowerShell 环境下直接调用可能报错找不到 `sh`。
- **对策**：
  - 确保安装了 Git for Windows，并将 `C:\Program Files\Git\bin`（或 `usr\bin`）加入系统 PATH，以便命令行中可识别 `sh`。
  - 或在不支持 Bash Hook 的平台中，直接依靠技能说明中的文件规约手动维护规划文件。

---

## 五、安装与使用方式

### 方式一：直接载入本地目录（推荐）

1. 将本仓库克隆至你的本地目录：
   ```powershell
   git clone https://github.com/ldray857/ray-skills.git D:/PClog/ray-skills
   ```
2. 将需要的技能目录（如 `planning-with-files`、`pdf` 等）复制到你所用 Agent 的技能存放目录：
   - **Antigravity / Gemini CLI**：`%USERPROFILE%\.gemini\antigravity\skills\`
   - **Claude Desktop / Claude Code**：`%USERPROFILE%\.claude\skills\`
   - **项目级局部启用**：直接将对应目录放置在项目根目录下的 `.agent/skills/` 或 `.claude/skills/` 中。

### 方式二：通过开放生态动态安装

使用 `find-skills` 发现并安装对应工具：
```powershell
npx skills add <skill-name>
```

---

## 六、开源协议与版权致谢

- 本项目本身的整理汇编、文档指南及相关配置文件采用 [MIT License](LICENSE) 协议开源。
- 仓库内收录的各个第三方 Skills 均严格保留原作者的版权声明与开源协议：
  - Anthropic 官方技能 (`frontend-design`, `pdf`, `skill-creator`) 遵循 Apache-2.0 协议；
  - Google 官方技能 (`accidental-data-loss-prevention`) 遵循 Apache-2.0 协议；
  - 社区开源技能 (`humanizer`, `humanizer-zh`, `planning-with-files`, `ui-ux-pro-max` 等) 遵循各自独立的 MIT / Apache-2.0 协议。

感谢所有上游开源创作者为 AI Agent 生态繁荣做出的贡献。
