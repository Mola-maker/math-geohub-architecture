# Math GeoHub Architecture

[中文](#中文) · [English](#english)

## 中文

这是一个面向主流 AI Agent 的可移植架构插件，把 [Math GeoHub](https://github.com/Mola-maker/mathhub) 中经过真实产品迭代形成的三组方法论封装为 Agent Skills：

- `build-semantic-canvas`：建立单一持久真源、无损语法投影、revision-bound 语义文档、稳定实体身份与统一 transaction broker。
- `guard-agentic-canvas-writes`：把模型意图、只读工具、权限回执、原子提交、持久事件和提交后验证分开，避免过期写入与“模型说完成就算完成”。
- `design-dual-render-pipeline`：把低延迟交互渲染与隔离的精确渲染分开，并用 source/profile attestation、队列 fencing 和产物安全边界连接两者。

插件是纯技能包：没有 MCP Server、可执行脚本、网络请求、遥测、账号或密钥。

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
gemini extensions install https://github.com/Mola-maker/math-geohub-architecture --ref v1.0.0
```

#### Cursor

在 `Customize → Plugins` 中从此 Git 仓库安装；本地验证可把仓库放入 `~/.cursor/plugins/local/math-geohub-architecture` 后重载窗口。

#### ChatGPT / Codex

插件已包含 `.codex-plugin/plugin.json`，可通过 ChatGPT/Codex 插件目录的仓库市场源安装。添加市场：

```bash
codex plugin marketplace add Mola-maker/math-geohub-architecture --ref v1.0.0
```

然后重启桌面应用，在 Plugins Directory 的 `math-geohub` 来源中安装 `math-geohub-architecture`。

### 示例请求

- “为这个带代码编辑器的几何画板设计单一真源和语义投影架构。”
- “审计这个 Agent 写入流程，找出 stale basis、越权范围和虚假完成状态。”
- “规划 SVG 交互预览 + 服务端精确 PDF 编译的双渲染管线。”

## English

Math GeoHub Architecture is a portable, skills-only plugin that turns production architecture lessons from [Math GeoHub](https://github.com/Mola-maker/mathhub) into reusable workflows for AI agents.

It helps teams design source-authoritative semantic canvases, guard agent-authored mutations with current-state authority and post-commit verification, and separate responsive interactive rendering from isolated exact rendering.

The package follows Agent Plugins 1.0 and also includes native manifests for ChatGPT/Codex, Claude Code, and Gemini CLI. It contains no MCP server, executable code, telemetry, credentials, or network access.

See the Chinese section above for install commands. Detailed privacy and terms are available on the [project site](https://mola-maker.github.io/math-geohub-architecture/).

## License

[MIT](LICENSE)
