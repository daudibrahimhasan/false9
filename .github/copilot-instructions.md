# False9 — GitHub Copilot Integration

This project uses the False9 multi-agent audit and completion system.

## Agents

The agent definitions in `.github/copilot/` define specialized AI agents that can be loaded as custom instructions for code review, security scanning, performance auditing, and more.

## Usage

Load any agent markdown file as a custom instruction or workspace prompt in GitHub Copilot Chat.

### Available Agents

- `f9-manager.md` — Orchestration and project recon
- `f9-code-quality.md` — Code quality analysis
- `f9-backend.md` — Backend API auditing
- `f9-database.md` — Database query optimization
- `f9-security.md` — Security vulnerability scanning
- `f9-frontend.md` — Frontend completion and wiring
- `f9-performance.md` — Performance profiling
- `f9-testing.md` — Test quality analysis
- `f9-llm-validator.md` — LLM feature validation
- `f9-devops.md` — DevOps and deploy readiness
- `f9-innovation.md` — Quick win identification
- `f9-synthesizer.md` — Final report generation

## Commands

- `f9-audit` — Full engineering audit
- `f9-complete` — Intent reconstruction + completion + audit
