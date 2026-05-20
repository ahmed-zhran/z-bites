# 📦 CLI Agents Documentation

This document provides a concise overview of all supported CLI agents included in the **install-cli-agents** script. Each entry lists the agent name, the trigger command used to invoke it, and a brief description of its purpose.

| # | Agent Name | Trigger Command | Description |
|---|------------|----------------|-------------|
| 1 | **OpenCode** | `opencode` | AI coding assistant focusing on code generation and completion.
| 2 | **NanoCoder** | `nanocoder` | Lightweight coding assistant with fast response times.
| 3 | **Codebuff** | `codebuff` | Provides intelligent code suggestions and refactoring.
| 4 | **Goose** | `goose` | CLI tool for generating boilerplate code and project scaffolding.
| 5 | **Crush** | `crush` | Terminal UI library for building interactive applications.
| 6 | **Mistral Vibe** | `vibe` | Conversational AI model optimized for creative tasks.
| 7 | **GSD‑2** | `gsd` | General‑purpose coding assistant based on recent LLMs.
| 8 | **GSD‑OpenCode** | `gsd‑opencode` | Bridge between GSD‑2 and OpenCode capabilities.
| 9 | **Get Shit Done** | `get‑shit‑done‑cc` | Fast, no‑frills code generation CLI.
|10 | **Qwen Code** | `qwen` | Code‑focused model from Alibaba’s Qwen series.
|11 | **OpenAI Codex** | `codex` | Official OpenAI Codex CLI for code generation.
|12 | **GitHub Copilot CLI** | `github‑copilot` | GitHub’s AI pair‑programmer for the terminal.
|13 | **PI** | `pi` | Personalised AI assistant for coding tasks.
|14 | **Hermes** | `hermes` | Advanced LLM from NousResearch with strong reasoning.
|15 | **Antigravity** | `antigravity` | Powerful agentic AI coding assistant (Google DeepMind).
|16 | **Claude Code** | `claude` | Anthropic’s code‑centric model for secure generation.
|17 | **Gemini CLI** | `gemini` | Google Gemini‑based CLI for multimodal AI assistance.

---

## Usage Example
```bash
# Install all agents (idempotent)
./install-cli-agents

# Verify installation status
./list-cli-agents
```

The `install-cli-agents` script also provides a helper function `git_sync` that can be called manually to automatically stage, commit, and push any changes made to this repository:
```bash
git_sync "Your commit message"
```

---

*Generated on $(date '+%Y-%m-%d').*
