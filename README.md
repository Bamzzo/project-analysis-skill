# project-analysis-skill

一个面向复杂软件项目的通用分析 Skill，用来帮助 AI 智能体系统性地阅读、拆解、理解和评估一个陌生代码库。

它不是简单的“总结项目文件”的提示词，而是一套项目分析范式：先建立项目地图，再识别入口点、运行边界、核心模块、数据/控制流、状态与契约、外部依赖、验证路径、风险和下一步行动。

## 适合什么场景

- 接手一个陌生、庞大、历史包袱重的项目
- 分析 monorepo、多包、多语言或多服务系统
- 梳理 Web、后端、前端、移动端、桌面端、CLI、SDK、插件项目
- 理解 Agent、LLM、工具调用、RAG、自动化工作流项目
- 分析数据库、迁移、ORM、数据持久化和状态一致性
- 分析数据管道、ML、评测、推理或索引项目
- 做架构审查、安全敏感审查、重构前调研或技术交接
- 规划复杂改动前的影响面、风险和验证路径

## 核心能力

- **分级分析**：支持 quick、standard、deep、audit 四种深度。
- **证据优先**：区分代码事实、文档事实、运行时验证、推断和开放问题。
- **主流程追踪**：从输入、分发、核心逻辑、外部依赖一路追到状态和输出。
- **风险识别**：关注配置、状态、副作用、测试缺口、外部依赖、安全边界等风险。
- **渐进加载**：主 Skill 保持简洁，按项目类型加载 `references/` 中的专项分析指南。
- **面向行动**：最终输出不仅说明项目是什么，还说明应该读什么、跑什么、测什么、避免什么、下一步做什么。

## 仓库结构

```text
project-analysis-skill/
├─ README.md
├─ LICENSE
├─ .gitignore
└─ project-analysis/
   ├─ SKILL.md
   ├─ agents/
   │  └─ openai.yaml
   └─ references/
      ├─ analysis-checklists.md
      ├─ output-templates.md
      ├─ agent-projects.md
      ├─ web-projects.md
      ├─ monorepos.md
      ├─ library-cli-projects.md
      ├─ infra-projects.md
      ├─ database-projects.md
      ├─ data-ml-projects.md
      ├─ mobile-desktop-projects.md
      ├─ debugging-projects.md
      └─ security-audit-projects.md
```

## 在 Codex 中安装

将 `project-analysis/` 文件夹复制到你的 Codex skills 目录。

Windows 常见位置：

```powershell
Copy-Item -Recurse .\project-analysis $env:USERPROFILE\.codex\skills\
```

macOS / Linux 常见位置：

```bash
cp -R ./project-analysis ~/.codex/skills/
```

安装后，可以这样使用：

```text
Use $project-analysis to analyze this repository and produce an evidence-backed architecture map, verification plan, risks, and recommended next actions.
```

中文也可以：

```text
请使用 $project-analysis 分析这个项目，重点梳理架构、入口点、主流程、状态契约、测试验证方式、风险和下一步建议。
```

## 在普通对话框 LLM 中使用

如果你使用的是不能直接读取本地文件夹的对话式 LLM，可以把这个 Skill 当作“分批取证工作流”使用。

第一轮建议上传：

- `project-analysis/SKILL.md`
- 项目文件树或 `rg --files` 输出
- 顶层 `README`
- 主要 manifest / config 文件，例如 `package.json`、`pyproject.toml`、`go.mod`、`Cargo.toml`、`docker-compose.yml`
- CI、测试、启动脚本配置

然后这样提问：

```text
请使用 project-analysis 方法分析这个项目。

限制条件：你不能直接访问本地文件夹，我会分批上传文件。请不要假设你没看到的内容。

本轮我会提供：
1. 文件树
2. README
3. manifest/config/scripts
4. CI 或测试配置

请先完成：
- 项目初步判断
- 技术栈和目录结构
- 可能的入口点
- 当前证据和推断的区分
- 下一批最应该上传的文件清单，按优先级排序，并解释每个文件的作用
```

之后每一轮让 LLM 输出：

```text
已观察到的事实：
文档声称但未验证：
基于结构的推断：
当前未知：
下一批需要的文件：
```

这样可以减少幻觉，让分析建立在真实证据上。

## 安全注意事项

- 不要上传 `.env`、私钥、token、证书、生产连接串或真实敏感数据。
- 不要让 AI 在不了解脚本内容时运行安装、迁移、部署、删除、写入或生产环境命令。
- 对安全审查、数据库迁移、基础设施部署等高风险场景，优先做只读分析、dry-run 或手动确认。
- 对没有实际运行验证的结论，应明确标记为“推断”或“未验证”。

## 许可证

本项目使用 MIT License。你可以自由使用、修改和分发，但请保留许可证声明。
