# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

If you discover a security vulnerability in False9, please report it responsibly.

**Do not open a public GitHub issue for security vulnerabilities.**

Instead, email **<daudibrahimhasan@gmail.com>** with:

- A description of the vulnerability
- Steps to reproduce
- The affected version(s)
- Any potential impact assessment

You can expect:

- **Acknowledgment** within 48 hours
- **Status update** within 7 days
- **Fix or mitigation** within 30 days for critical issues

If the vulnerability is accepted, we will:

- Credit you in the release notes (unless you prefer anonymity)
- Fix the issue in a timely manner
- Coordinate disclosure timing with you

If the vulnerability is declined, we will explain why and provide guidance on whether it should be reported elsewhere.

## Scope

This policy covers:

- All agent definitions under `.claude/agents/` and mirrored directories (`.cursor/agents/`, `.codex/agents/`, `.codebuddy/agents/`, `.gemini/agents/`, `.github/copilot/`, `.kiro/agents/`, `.opencode/agents/`, `.qwen/agents/`, `.trae/agents/`, `.zed/agents/`)
- All commands under `.claude/commands/` and mirrored directories (`.cursor/commands/`, etc.)
- The orchestrator templates and custom hook configurations
- Hook scripts and settings shipped within this repository

## Operational Guidance

### Secrets Handling

Configuration templates for custom agents and settings must never hardcode API keys, personal access tokens (PATs), or credentials. Always resolve secrets from environment variables or a local credentials manager. If a secret is accidentally committed, rotate it immediately and rewrite git history; do not rely on a plain revert.

### Local Client Auditing

Custom scripts that execute tasks on local servers should be audited. When running commands locally or spawning local dev servers, verify active listening ports:

```bash
# Windows
netstat -ano | findstr :18801
# macOS / Linux
lsof -iTCP:18801 -sTCP:LISTEN
```

### Triage: Suspicious Client-Side Prompts

False9 runs inside various AI coding tools (Claude Code, Cursor, Copilot, etc.). Many of these environments inject ephemeral client-side system reminders into the model's context (e.g. date-changed notices, file-modified notices, directory checks). These prompts:
- are injected dynamically per turn by the parent CLI/harness;
- are **not persisted** as repository payloads.

Before treating context anomalies as an attack, verify:
1. Is the string actually in a file under this repository? `git grep -in "pattern"`
2. Is the content contextually consistent with your parent AI tool's normal operation guidelines?

Only escalate to the parent tool vendor (e.g. Anthropic, GitHub, VS Code) if a pattern is traced back to a specific tool result payload that is not attributable to the target file being read.

## Security Resources

- **OWASP MCP Top 10**: [owasp.org/www-project-mcp-top-10](https://owasp.org/www-project-mcp-top-10/)
- **OWASP Agentic Applications Top 10**: [genai.owasp.org](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
