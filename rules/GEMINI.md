# Agent Memory

## 最重要
- 文件读取：用户指定读取时，仅用户指定的特定目标文件或者文件夹，严禁擅自读取其他文件或者文件夹。
- 不编造内容、实验结果、引用、数据、执行记录或结论。材料不足时保留明确占位或说明缺口。
- 任务规划：处理复杂代码或大于 5 步的长步骤任务时，默认启用 planning-with-files 技能。
- 删除、覆盖、批量移动或其他难以恢复的操作（尤其是重要信息的时候）前，先确认精确目标与范围；优先采用可恢复方式，并避免对宽泛目录执行破坏性命令。


## 基础画像与交互
- 用户：（待填入），（待填入）（GitHub: （待填入），Email: （待填入））。
- 格式：UTF-8 编码，严禁使用任何颜文字与表情符号。
- 电脑硬件：（待填入） (（待填入）, （待填入）, windows11系统)。CUDA 11.8, cuDNN 8.9.7。


## 交流回答时
- 先给结果，只展开完成任务所需要的细节。
- 默认使用中文交流；代码、命令、字段名和必要的专业术语保留其常用英文形式。
- 明确区分：已完成（或已修改）、尚未完成、需要用户手动完成，有具体文件或文件生成时请给出绝对路径。


## Office操作
- 办公与电子文档规范：处理文档时必须强制遵循对应技能，严禁使用非标方案：
  - Word (.docx, .doc)：遵循 docx-gem 技能（新建用 docx-js，修改走 XML 就地编辑与 XSD 校验）；若用户仅要求生成 Word，未获明确指示时严禁擅自将其转换为 PDF。
  - PPT (.pptx, .ppt)：遵循 pptx-gem 技能进行大纲、排版与生成。
  - Excel (.xlsx, .xls, .csv)：遵循 xlsx-gem 技能进行表格构建、公式运算与清洗。
  - PDF (.pdf)：用户要求进行 PDF 编辑时，遵循 pdf 技能；用户要求 PDF 文件读取和概括时，默认使用内置工具直接；用户要求提取文字时，调用相关的技能或 Python 读取 PDF。
  - Python 环境规范：操作 Office 相关文档（Word、PPT、Excel 等）时，凡需调用 Python 环境，必须统一使用 gem 虚拟环境（D:\Anaconda\envs\gem），严禁使用 Base 或其他无关环境。


## Python 开发规范
- Conda 环境：虚拟环境位于 D:\Anaconda\envs，Base 位于 D:\Anaconda3，你默认使用名为read的环境。
- 隔离红线：
  - 严禁在 Base 环境开发或安装包，必须在独立虚拟环境中操作。
  - 严禁访问或修改 ArcGIS Pro 的python环境。


## C/C++ 开发规范
- 工具链：全面采用 MSVC (cl.exe) + vcpkg (x64-windows) + CMake + Ninja，严禁使用 MinGW / MSYS2。
  - VS 2026: D:\apps_ide\Microsoft Visual Studio\18\Community
  - vcpkg: D:\vcpkg | CMake: D:\apps_others\CMake\bin | Ninja: D:\apps_others\ninja


## 关键运行时与 D 盘索引
- 数据库与运行时：
  - PostgreSQL 16.14: D:\app_file\Postgresql（端口 5432，密码 （待填入））+ PostGIS 3.6.2。注意未激活环境时显式调用 D:\app_file\Postgresql\bin\pg_config.exe。
  - OpenJDK 17: D:\apps_others\java\
  - Node.js v26.8: C:\Program Files\nodejs
  - .NET SDK 10.0: C:\Program Files\dotnet\。
  - 排版与构建工具：Git, Pandoc (D:\app_file\Pandoc\), MiKTeX (D:\app_file\MikTex\), Ghostscript, Prince。
