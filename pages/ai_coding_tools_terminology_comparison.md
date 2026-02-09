# AI Coding Tools Terminology Comparison

A comparison of terminology used across major AI coding tools (as of February 2026).

## Comparison Table

| Concept | Claude Code | OpenAI Codex | Kiro IDE | Kiro CLI | Gemini CLI | OpenCode |
|---|---|---|---|---|---|---|
| **The AI itself** | Agent / Subagent | Agent | Agent + Autonomous Agent (async) | Agent | Agent (ReAct loop) | Agent |
| **Specialized agents** | Subagents (Explore, Plan, Bash, etc.) + Custom Agents | — | Subagents + Powers (context bundles) | Subagents + Custom Agents | Sub-agents (experimental: cli_help, routing, generalist) + Jules (async) + Custom Agents | Primary Agents (Build, Plan) + Subagents (General, Explore) + Custom Agents |
| **Callable capabilities** | Tools (Read, Edit, Bash, Grep, Glob, Write, WebFetch, WebSearch, etc.) | Tools (shell, file read/write, apply patch, etc.) | Tools (built-in + MCP tools) | Built-in Tools (read, write, shell, aws, grep, glob, subagent, web search/fetch) | Tools (ReadFile, WriteFile, Edit, Shell, FindFiles, SearchText, GoogleSearch, WebFetch, SaveMemory, etc.) | Tools (bash, read, write, edit, grep, glob, list, patch, lsp, webfetch, websearch, etc.) |
| **External integrations** | MCP Servers | MCP Servers | MCP Servers (local + remote) | MCP Servers (local + remote, with MCP Registry governance) | MCP Servers (stdio + SSE transports) | MCP Servers (local + remote with OAuth) |
| **Reusable workflows / instructions** | Skills (slash commands) + Plugins | Skills + /review + /plan slash commands | Specs (SDD) + Agent Skills | Skills (progressively loaded, on-demand) | Extensions + Agent Skills (SKILL.md) + Custom Slash Commands | Skills (SKILL.md files in .opencode/skills/) |
| **Event-driven automation** | Hooks (14 events: PreToolUse, PostToolUse, SessionStart/End, UserPromptSubmit, Stop, SubagentStart/Stop, PreCompact, etc.) | — | Agent Hooks (file save/create/delete, prompt submit, agent turn, pre/post tool use) | Hooks (agentSpawn, userPromptSubmit, preToolUse, postToolUse, stop) | Hooks (SessionStart/End, BeforeModel/AfterModel, BeforeTool/AfterTool, BeforeAgent/AfterAgent, BeforeToolSelection, PreCompress) | Plugins (tool.execute.before/after, file.edited, session events, etc.) |
| **Project-level AI instructions** | CLAUDE.md (hierarchical: user/project/local) | AGENTS.md (hierarchical, with configurable fallbacks) | Steering Files (.kiro/steering/) | Steering Files (.kiro/steering/) + Agent config JSON | GEMINI.md (hierarchical, multi-file, configurable filename) | AGENTS.md (also reads CLAUDE.md for compatibility) |
| **Persistent memory** | Auto memory (~/.claude/projects/&lt;project&gt;/memory/) + Subagent memory | Thread memory (experimental) | Autonomous Agent learns from PR feedback | Knowledge management (experimental, /knowledge) | save_memory (built-in tool) + Conductor (extension) | — (available via community plugins) |
| **Bundled packages** | Plugins (commands, agents, skills, hooks, MCP, LSP) | — | Powers (MCP + steering + hooks) + Agent Skills + Open VSX plugins | Custom Agents (bundled config + tools + steering) | Extensions (MCP + context + slash commands + skills) | Plugins (JS/TS modules with hooks + custom tools) |
| **Background/async work** | Background tasks | Automations (scheduled runs in background worktrees) | Autonomous Agent (runs for days, up to 10 concurrent tasks) | Subagent parallelism | Jules (async in VM, up to 15 concurrent tasks) + Sub-agents | — (available via community plugins) |
| **Parallel execution** | Subagent parallelism | Cloud worktrees | Subagents (parallel) + Autonomous Agent (10 concurrent) | Subagents (isolated context, live progress) | Jules (15 concurrent tasks) + Sub-agents (experimental) | General subagent (limited parallelism) |
| **Planning mode** | Plan agent | /plan slash command | Spec-Driven Development + Plan Agent | Plan agent (built-in, Shift+Tab or /plan) | Plan Mode (experimental, read-only) | Plan agent (read-only, Tab to switch) |
| **Configuration** | settings.json (JSON, hierarchical scopes) | config.toml (TOML, with profiles) | .kiro/ directory (steering md, hooks, agents md, skills) | Agent config JSON + Steering Markdown | settings.json (JSON) + GEMINI.md | opencode.json (JSON/JSONC) |

## Key Takeaways

- **"Tool"** is nearly universal — it means a callable capability the agent can invoke (read files, run commands, search, etc.).
- **"Agent"** is also universal — every tool uses this for the AI that reasons and acts.
- **"Subagent"** is now shared by Claude Code, Kiro (IDE and CLI), Gemini CLI (experimental), and OpenCode — specialized agents with isolated context that can run in parallel.
- **"Skill"** has converged across nearly all tools: Claude Code, Codex, Kiro (IDE and CLI), Gemini CLI, and OpenCode all use it for reusable, on-demand task-specific workflows. Most use SKILL.md files with YAML frontmatter.
- **"Hook"** is now supported by Claude Code, Kiro (IDE and CLI), Gemini CLI, and OpenCode — though with varying event types. Claude Code and Kiro CLI share pre/post tool-use hooks; Kiro IDE added prompt submit and agent turn triggers; Gemini CLI has the most extensive hook system (11+ event types including BeforeModel, AfterModel, BeforeToolSelection).
- **"Steering"** is unique to Kiro (both IDE and CLI) — project-level guardrails and conventions for the AI, analogous to CLAUDE.md or GEMINI.md but more structured.
- **"Extension"** is Google's term (Gemini CLI) for bundled packages that combine MCP servers, context files, slash commands, and skills — more comprehensive than what others call skills or plugins.
- **Kiro CLI vs Kiro IDE** have converged significantly — both now have subagents, hooks (with 5-7 trigger types), skills, MCP support, and plan agents. The IDE additionally offers Powers (dynamic context bundles) and the Autonomous Agent for multi-day async work.
- **"Plugin"** is shared by Claude Code and OpenCode, but with different meanings — Claude Code plugins are bundled packages of commands/agents/skills/hooks/MCP/LSP, while OpenCode plugins are JS/TS modules that hook into events and can create custom tools.
- **MCP (Model Context Protocol)** has become a universal cross-tool standard adopted by all six tools compared here.
- **Plan mode** is now shared by all tools except Codex (which has /plan as a slash command): Claude Code, Kiro (IDE SDD + Plan Agent, CLI Plan Agent), Gemini CLI (experimental), and OpenCode all offer read-only planning modes.
- **Persistent memory** varies widely: Claude Code has auto memory files, Gemini CLI has a built-in save_memory tool, Kiro CLI has experimental knowledge management with semantic search, Codex has experimental thread memory, and the Kiro Autonomous Agent learns from PR feedback across sessions.

## Sources

### Claude Code
- [Claude Code Skills Docs](https://code.claude.com/docs/en/skills)
- [Claude Code Plugins](https://code.claude.com/docs/en/plugins)
- [Claude Code Settings](https://code.claude.com/docs/en/settings)
- [Claude Code Sub-agents](https://code.claude.com/docs/en/sub-agents)
- [Claude Code Hooks](https://code.claude.com/docs/en/hooks)
- [Understanding Claude Code's Full Stack](https://alexop.dev/posts/understanding-claude-code-full-stack/)

### OpenAI Codex
- [OpenAI Codex CLI](https://developers.openai.com/codex/cli/)
- [OpenAI Codex CLI Features](https://developers.openai.com/codex/cli/features/)
- [OpenAI Codex CLI Slash Commands](https://developers.openai.com/codex/cli/slash-commands/)
- [OpenAI Codex Skills](https://developers.openai.com/codex/skills)
- [OpenAI Codex Automations](https://developers.openai.com/codex/app/automations/)
- [OpenAI Codex AGENTS.md](https://developers.openai.com/codex/guides/agents-md/)
- [OpenAI Codex Config Reference](https://developers.openai.com/codex/config-reference/)
- [OpenAI Codex Config Sample](https://developers.openai.com/codex/config-sample/)
- [OpenAI Codex MCP](https://developers.openai.com/codex/mcp/)

### Kiro IDE
- [Amazon Kiro](https://kiro.dev/)
- [Kiro IDE Specs](https://kiro.dev/docs/specs/)
- [Kiro IDE Steering](https://kiro.dev/docs/steering/)
- [Kiro IDE Hooks](https://kiro.dev/docs/hooks/)
- [Kiro IDE Hook Types](https://kiro.dev/docs/hooks/types/)
- [Kiro IDE Subagents](https://kiro.dev/docs/chat/subagents/)
- [Kiro IDE Agent Skills](https://kiro.dev/docs/skills/)
- [Kiro IDE MCP](https://kiro.dev/docs/mcp/)
- [Kiro Powers](https://kiro.dev/powers/)
- [Kiro Autonomous Agent](https://kiro.dev/autonomous-agent/)
- [Kiro Spec-Driven Development](https://www.infoq.com/news/2025/08/aws-kiro-spec-driven-agent/)

### Kiro CLI
- [Kiro CLI Introduction](https://kiro.dev/blog/introducing-kiro-cli/)
- [Kiro CLI Built-in Tools](https://kiro.dev/docs/cli/reference/built-in-tools/)
- [Kiro CLI Subagents](https://kiro.dev/docs/cli/chat/subagents/)
- [Kiro CLI Hooks](https://kiro.dev/docs/cli/hooks/)
- [Kiro CLI Steering](https://kiro.dev/docs/cli/steering/)
- [Kiro CLI MCP Configuration](https://kiro.dev/docs/cli/mcp/configuration/)
- [Kiro CLI Knowledge Management (experimental)](https://kiro.dev/docs/cli/experimental/knowledge-management/)
- [Kiro CLI Skills, Custom Diff Tools (v1.24 changelog)](https://kiro.dev/changelog/cli/1-24/)
- [Kiro CLI Subagents, Plan Agent (v1.23 changelog)](https://kiro.dev/changelog/cli/1-23/)
- [Kiro CLI Custom Agents](https://kiro.dev/docs/cli/custom-agents/creating/)
- [Kiro CLI Agent Config Reference](https://kiro.dev/docs/cli/custom-agents/configuration-reference/)

### Gemini CLI
- [Gemini CLI](https://developers.google.com/gemini-code-assist/docs/gemini-cli)
- [Gemini CLI Tools](https://geminicli.com/docs/tools/)
- [Gemini CLI Hooks](https://geminicli.com/docs/hooks/)
- [Gemini CLI Hooks Reference](https://geminicli.com/docs/hooks/reference/)
- [Gemini CLI Sub-agents (experimental)](https://geminicli.com/docs/core/subagents/)
- [Gemini CLI Agent Skills](https://geminicli.com/docs/cli/skills/)
- [Gemini CLI GEMINI.md](https://geminicli.com/docs/cli/gemini-md/)
- [Gemini CLI Configuration](https://geminicli.com/docs/get-started/configuration/)
- [Gemini CLI Extensions](https://geminicli.com/extensions/)
- [Jules Extension for Gemini CLI](https://developers.googleblog.com/en/introducing-the-jules-extension-for-gemini-cli/)
- [Conductor Extension](https://developers.googleblog.com/conductor-introducing-context-driven-development-for-gemini-cli/)
- [Gemini CLI Hooks Blog Post](https://developers.googleblog.com/tailor-gemini-cli-to-your-workflow-with-hooks/)

### OpenCode
- [OpenCode AI](https://opencode.ai/)
- [OpenCode Agents](https://opencode.ai/docs/agents/)
- [OpenCode Tools](https://opencode.ai/docs/tools/)
- [OpenCode Skills](https://opencode.ai/docs/skills/)
- [OpenCode Plugins](https://opencode.ai/docs/plugins/)
- [OpenCode MCP Servers](https://opencode.ai/docs/mcp-servers/)
- [OpenCode Config](https://opencode.ai/docs/config/)
- [OpenCode Rules](https://opencode.ai/docs/rules/)
