# Math GeoHub Architecture

[中文](#中文) · [English](#english)

## 中文

这是一个面向主流 AI Agent 的可移植工程插件，把 [Math GeoHub](https://github.com/Mola-maker/mathhub) 中经过真实产品迭代形成的方法论封装为八项 Agent Skills：

- `build-semantic-canvas`：建立单一持久真源、无损语法投影、revision-bound 语义文档、稳定实体身份与统一 transaction broker。
- `guard-agentic-canvas-writes`：把模型意图、只读工具、权限回执、原子提交、持久事件和提交后验证分开，避免过期写入与“模型说完成就算完成”。
- `design-dual-render-pipeline`：把低延迟交互渲染与隔离的精确渲染分开，并用 source/profile attestation、队列 fencing 和产物安全边界连接两者。
- `evolve-math-geohub`：按项目真实 owner、协议和迁移边界审计架构与代码复用，避免并行真源、重复 schema 和永久兼容层。
- `verify-math-geohub-change`：把改动声明映射到分层证据，并严格保留产品负责人对测试、构建、编译器和 Docker 命令的授权边界。
- `research-geometry-evidence`：用本地证据、官方文档、SHA-pinned GitHub、Consensus、Exa 与 Tavily 建立可复现科研证据账本。
- `design-geometry-search-gateway`：设计多源检索 adapter、资源预算、partial success、provenance/rights/taint 与可信 admission 边界。
- `audit-math-geohub-ux`：以真实旅程审计 Landing、两类 Studio、认证与 Console 的无障碍、恢复、响应式、性能和状态诚实性。

插件是纯技能包：没有 MCP Server、可执行脚本、遥测、账号或密钥。科研技能可以指导 Agent 使用用户已经配置并授权的 GitHub、Consensus、Exa 或 Tavily 等检索工具；插件自身不提供连接器，也不持有凭据。

### 支持的 Agent

根目录遵循 [Agent Plugins 1.0](https://agent-plugins.org/) 开放规范，可由支持该标准的 Cursor、GitHub Copilot、VS Code、ChatGPT/Codex、Kiro 等客户端读取；仓库还提供 Codex/ChatGPT、Claude Code 和 Gemini CLI 的原生清单。

### 安装

#### Claude Code

```bash
claude plugin marketplace add Mola-maker/math-geohub-architecture
claude plugin install math-geohub-architecture@math-geohub
```

#### GitHub Copilot CLI

```bash
copilot plugin marketplace add Mola-maker/math-geohub-architecture
copilot plugin install math-geohub-architecture@math-geohub
```

#### Gemini CLI

```bash
gemini extensions install https://github.com/Mola-maker/math-geohub-architecture --ref v1.1.0
```

#### Cursor

在 `Customize → Plugins` 中从此 Git 仓库安装；本地验证可把仓库放入 `~/.cursor/plugins/local/math-geohub-architecture` 后重载窗口。

#### ChatGPT / Codex

插件已包含 `.codex-plugin/plugin.json`，可通过 ChatGPT/Codex 插件目录的仓库市场源安装。添加市场：

```bash
codex plugin marketplace add Mola-maker/math-geohub-architecture --ref v1.1.0
```

然后可以运行 `codex plugin add math-geohub-architecture@math-geohub`，或重启桌面应用后在 Plugins Directory 的 `math-geohub` 来源中安装。

公共目录版本通过 OpenAI 审核和发布后，也可以直接在 ChatGPT/Codex 的通用 Plugins Directory 中搜索 `Math GeoHub Architecture` 安装。

### 示例请求

- “为这个带代码编辑器的几何画板设计单一真源和语义投影架构。”
- “审计这个 Agent 写入流程，找出 stale basis、越权范围和虚假完成状态。”
- “规划 SVG 交互预览 + 服务端精确 PDF 编译的双渲染管线。”

## English

Math GeoHub Architecture is a portable, skills-only plugin that turns production engineering lessons from [Math GeoHub](https://github.com/Mola-maker/mathhub) into reusable workflows for AI agents.

It covers source-authoritative semantic canvases, guarded agent mutations, dual rendering, project architecture and reuse, evidence-led geometry research, bounded multi-source gateways, UX acceptance, and authorization-aware verification.

The package follows Agent Plugins 1.0 and also includes native manifests for ChatGPT/Codex, Claude Code, and Gemini CLI. It contains no MCP server, executable code, telemetry, credentials, or bundled network integration; research connectors remain under the user's AI client and authorization.

See the Chinese section above for install commands. Detailed privacy and terms are available on the [project site](https://mola-maker.github.io/math-geohub-architecture/).

## License

[MIT](LICENSE)
