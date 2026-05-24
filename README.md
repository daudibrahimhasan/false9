<div align="center">

<br>

# False9

**The dream team you never had.**

An autonomous multi-agent system that audits, fixes, and completes<br>your software projects from any AI-powered coding environment.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Agents](https://img.shields.io/badge/Agents-12-orange)](.claude/agents)
[![Tools](https://img.shields.io/badge/Works%20With-12%2B%20Tools-brightgreen)](#-compatibility)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Security Policy](https://img.shields.io/badge/Security-Policy-brightgreen.svg)](SECURITY.md)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.0-4baaaa.svg)](CODE_OF_CONDUCT.md)

[Getting Started](#-getting-started) · [How It Works](#-how-it-works) · [The Squad](#-the-squad) · [Examples](#-example-output) · [Contributing](CONTRIBUTING.md) · [Security](SECURITY.md) · [Code of Conduct](CODE_OF_CONDUCT.md)

</div>

---

## Why This Exists

I had 28 projects. Some half-built. Some 10% done. 
Some fully built but broken in ways I couldn't track down alone.

I needed a team. So I built one.

**False9 is that team.** *The dream team you never had.*

Named after the football tactic where a striker drops deep to orchestrate play from every position on the pitch, False9 has no fixed role — it analyzes the entire playing field and deploys a specialized squad of domain experts in parallel.

---

## ✨ Features

- **🔍 Full-Stack Audit** — One command triggers 11 specialized agents across your entire codebase
- **🧠 Intent Reconstruction** — Reads your README, TODOs, git history, route patterns, and `.env` templates to understand what you *meant* to build
- **⚡ Parallel Execution** — All agents run simultaneously, not sequentially
- **🔒 Security-First** — Traces actual data flow, catches IDOR, logic-level auth bypass, and leaked secrets
- **🤖 LLM Validation** — Doesn't just check if your AI features run — tests if they produce the *right* output
- **📊 Scored Report** — Every domain scored 0–100 with a production-readiness percentage
- **🛠️ Auto-Fix** — In `--complete` mode, agents don't just find problems — they fix them
- **🔄 Cross-Reference Escalation** — Issues flagged by multiple agents are automatically escalated in severity
- **✅ Fix Verification** — Scores only improve when fixes are verified, never inflated

---

## 🚀 Getting Started

### Prerequisites

Any AI coding agent that supports custom agent definitions. See [Compatibility](#-compatibility) below.

### Installation

Clone the repository:

```bash
git clone https://github.com/daudibrahimhasan/false9.git
```

Copy the agents and commands into your tool's configuration directory:

```bash
# Copy commands
cp -r false9/.claude/commands/f9-* ~/.claude/commands/

# Copy agents
cp -r false9/.claude/agents/f9-* ~/.claude/agents/
```

That's it. No dependencies. No build step. No config files.

### Quick Start

Open **any project** in your AI coding tool and run:

```
/f9-audit
```

Your project will be analyzed, issues will be identified and fixed, and a comprehensive report will be generated at `false9_report.md`.

---

## 🔌 Compatibility

False9 works with any AI coding environment that supports custom agents or system prompts.

| Tool | Status | Notes |
|:---|:---:|:---|
| **Claude Code** | ✅ | Native support — drop-in `.claude/` directory |
| **Cursor** | ✅ | Use as custom agent instructions via `.cursorrules` or agent config |
| **VS Code / GitHub Copilot** | ✅ | Load agents as custom instructions or workspace prompts |
| **Codex** | ✅ | Pass agent definitions as system prompts |
| **Codex Plugin** | ✅ | Compatible with plugin agent architecture |
| **CodeBuddy** | ✅ | Import agent markdown files as custom personas |
| **Gemini** | ✅ | Use with Gemini Code Assist or custom agent configs |
| **Kiro** | ✅ | Load as agent specifications |
| **OpenCode** | ✅ | Compatible with custom agent definitions |
| **Qwen** | ✅ | Pass agent prompts as system instructions |
| **Trae** | ✅ | Use as custom AI agent configurations |
| **Zed** | ✅ | Load via assistant configuration |

> **Note:** The `.claude/` directory structure is the canonical format. Most tools can consume these markdown files directly or with minimal adaptation.

### 📖 How to Load & Use Them

Depending on which AI tool you are using, False9 will load automatically or can be manually referenced:

*   **Claude Code**:
    *   **How it works**: Auto-detects the `.claude/` directory at your project root.
    *   **To run**: Type `/f9-audit` or `/f9-complete` directly in the Claude Code terminal.
*   **Cursor**:
    *   **How it works**: Uses the `.cursorrules` file at the root to guide the model.
    *   **To run**: Open Cursor Chat or Composer (`Ctrl+L` / `Ctrl+I`) and mention an agent file (e.g., `"audit with @.cursor/agents/f9-security.md"`).
*   **VS Code / GitHub Copilot**:
    *   **How it works**: Copilot Chat automatically reads the workspace instructions in `.github/copilot-instructions.md`.
    *   **To run**: In the chat panel, reference any specific agent file using the `#file` or `@file` selector (e.g., `"refer to #.github/copilot/f9-performance.md"`).
*   **Codex / Codex Plugin**:
    *   **How it works**: Looks for rules defined in `.codex/AGENTS.md`.
    *   **To run**: Load the agent templates from `.codex/agents/` to configure the system instructions.
*   **Zed**:
    *   **How it works**: Uses instructions in `.zed/`.
    *   **To run**: Paste or refer the assistant panel to the agent prompts in `.zed/agents/` to assign roles.
*   **Gemini / Trae / CodeBuddy / Kiro / OpenCode / Qwen**:
    *   **How it works**: Specialized dot-folders (`.gemini/`, `.trae/`, etc.) mirror the agent personas.
    *   **To run**: Import the corresponding agent markdown file from the tool's folder as a custom persona, custom prompt, or system instruction in your tool's settings.

---

## 🎯 Execution Modes

### Audit Mode

```
/f9-audit
```

Deploys the full squad to evaluate your codebase. Identifies issues across all domains, applies fixes, and compiles a scored audit report. Best for existing projects you want to harden.

### Complete Mode

```
/f9-complete
```

Everything in audit mode, plus **intent reconstruction**. The Manager analyzes your git history, README, TODOs, route patterns, and environment templates to build an Intent Map — a blueprint of what your project is *supposed* to be. Agents then complete unfinished features, wire disconnected UI elements, and build missing endpoints. Best for half-finished projects.

---

<div align="center">

## ⚙️ How It Works

```
               ┌─────────────────────┐
               │     /f9-audit or     │
               │     /f9-complete     │
               └──────────┬──────────┘
                          │
               ┌──────────▼──────────┐
               │   Manager (#1)       │
               │   Project Recon      │
               │   Stack Detection    │
               │   Intent Map*        │
               └──────────┬──────────┘
                          │
    ┌─────────────────────┼─────────────────────┐
    │                     │                     │
┌───▼────────────┐ ┌──────▼─────────┐ ┌─────────▼──────┐
│ Code Quality   │ │ Backend        │ │ Database       │
│ Security       │ │ Frontend       │ │ Performance    │
│ Testing        │ │ LLM Validator  │ │ DevOps         │
│ Innovation     │ │                │ │                │
└───┬────────────┘ └──────┬─────────┘ └─────────┬──────┘
    │                     │                     │
    └─────────────────────┼─────────────────────┘
                          │
               ┌──────────▼──────────┐
               │  Synthesizer (#12)   │
               │  Cross-reference     │
               │  Verify fixes        │
               │  Generate report     │
               └──────────┬──────────┘
                          │
               ┌──────────▼──────────┐
               │  false9_report.md    │
               │  Terminal Scorecard  │
               └─────────────────────┘

         * Intent Map is --complete mode only
```

</div>

### Phase 1 — Recon

The **Manager** performs a lightning-fast analysis of your project: stack, frameworks, database, LLM integrations. It intelligently skips irrelevant agents (no database → skip Database Specialist; no LLM calls → skip LLM Validator).

### Phase 2 — Intent Reconstruction *(complete mode only)*

The Manager inspects git logs, README, TODOs/FIXMEs, route names, component stubs, nav links pointing to missing pages, frontend fetch calls with no matching backend route, and `.env.example` keys. It builds an **Intent Map**: what's done, what's unfinished, what's missing-but-implied.

### Phase 3 — Parallel Agent Execution

All relevant agents spawn **simultaneously**. Each operates independently within its domain:

- Reads the codebase summary and relevant code paths
- Diagnoses structural issues, bugs, and gaps
- Applies targeted fixes without interfering with other agents
- Reports findings with severity ratings

### Phase 4 — Synthesis & Verification

The **Synthesizer** reads all agent findings, cross-references them (escalating severity for files flagged by multiple agents), verifies that fixes actually resolve the underlying issues, and compiles the final scorecard and `false9_report.md`.

---

## 👥 The Squad

| # | Agent | Domain | Strategy |
|:---:|:---|:---|:---|
| **1** | **Manager** | Orchestration | Recon, intent maps, spawns everyone simultaneously. Never audits code itself. |
| **2** | **Code Quality Judge** | Structure & Patterns | TypeScript errors, dead code, god files, code smells. Writes `codebase_summary` that all other agents depend on. |
| **3** | **Backend Engineer** | APIs & Validation | Diffs frontend fetch calls against existing routes. Builds every missing endpoint. Simulates a client for each route. |
| **4** | **Database Specialist** | Queries & Scale | Every query evaluated at 100K rows. Indexes, transaction boundaries, N+1 detection. |
| **5** | **Security Guard** | Vulnerabilities & Data Flow | Traces `Input → Handler → Validation → DB → Response`. IDOR checks, secret scanning, auth bypass detection. Zero tolerance for critical issues. |
| **6** | **Frontend Architect** | UI Completion | Completes stub components, wires disconnected buttons/forms to APIs, replaces placeholder content. Never touches design decisions. |
| **7** | **Performance Beast** | Speed & Efficiency | Simulates slow 3G connections. Memory leaks, heavy imports, missing debounce, waterfall API calls, skeleton screens. |
| **8** | **Testing Captain** | Test Quality | For each test: *"If I deleted this feature, would this test fail?"* Rewrites snapshot abuse, fixes flaky tests, adds behavioral assertions. |
| **9** | **LLM Validator** | AI Feature Correctness | 5-test suite per LLM call (normal, short, long, empty, adversarial). Scores relevance, accuracy, format, safety. Fixes prompts, parsers, and error handling. |
| **10** | **DevOps Engineer** | Deploy Readiness | Simulates a cold deploy step-by-step: clone → install → env → build → start → health check. Finds every step that would fail. |
| **11** | **Innovation Consultant** | Opportunity Mining | Finds features that are 80% built, installed-but-unused libraries, data models with untapped potential. Only suggests quick wins. |
| **12** | **Synthesizer** | Final Report | Cross-references all findings. Verifies fixes. Escalates overlapping issues. Writes `false9_report.md` and terminal scorecard. |

---

## 📊 Example Output

After a run completes, you'll see this in your terminal:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  FALSE9 AUDIT COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  Code Quality    81/100  ✅
  Backend         79/100  ✅
  Database        78/100  ✅
  Security        71/100  ⚠️
  Frontend        84/100  ✅
  Performance     72/100  ✅
  Testing         58/100  🚨
  LLM Validator   91/100  ✅
  DevOps          65/100  ⚠️

  OVERALL: 76/100
  Production Ready: 71%

  Critical fixed:  3
  High fixed:      8

  Full report → false9_report.md
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

The full report (`false9_report.md`) includes:

- **Scorecard** — Per-domain scores with status indicators
- **Critical Fixed** — Security vulnerabilities, data leaks, auth bypasses resolved
- **High Fixed** — Missing endpoints, broken integrations, dead code removed
- **Cross-Cutting Issues** — Problems flagged by multiple agents (auto-escalated)
- **Needs Human Review** — Decisions that require human judgment
- **Innovation Opportunities** — Quick wins and revenue gaps
- **Before vs After** — Concrete metrics showing improvement

---

## 🏗️ Project Structure

```
false9/
├── README.md
├── LICENSE
├── .cursorrules                  # Cursor rules file
│
├── .claude/                      # Claude Code (canonical)
│   ├── commands/
│   │   ├── f9-audit.md
│   │   └── f9-complete.md
│   └── agents/
│       ├── f9-manager.md         # The Brain — orchestration & recon
│       ├── f9-code-quality.md    # Code Quality Judge
│       ├── f9-backend.md         # Backend Engineer
│       ├── f9-database.md        # Database Specialist
│       ├── f9-security.md        # Security Guard
│       ├── f9-frontend.md        # Frontend Architect
│       ├── f9-performance.md     # Performance Beast
│       ├── f9-testing.md         # Testing Captain
│       ├── f9-llm-validator.md   # LLM Validator
│       ├── f9-devops.md          # DevOps Engineer
│       ├── f9-innovation.md      # Innovation Consultant
│       └── f9-synthesizer.md     # Synthesizer — final report
│
├── .cursor/                      # Cursor
│   ├── agents/
│   └── commands/
├── .codex/                       # Codex / Codex Plugin
│   ├── AGENTS.md
│   ├── agents/
│   └── commands/
├── .codebuddy/                   # CodeBuddy
│   ├── agents/
│   └── commands/
├── .gemini/                      # Gemini
│   ├── agents/
│   └── commands/
├── .github/                      # VS Code / GitHub Copilot
│   ├── copilot-instructions.md
│   └── copilot/
├── .kiro/                        # Kiro
│   ├── agents/
│   └── commands/
├── .opencode/                    # OpenCode
│   ├── agents/
│   └── commands/
├── .qwen/                        # Qwen
│   ├── agents/
│   └── commands/
├── .trae/                        # Trae
│   ├── agents/
│   └── commands/
├── .vscode/                      # VS Code settings
│   └── settings.json
└── .zed/                         # Zed
    ├── agents/
    └── commands/
```

> **All tool directories contain the same 12 agents and 2 commands.** The `.claude/` directory is the canonical source. All others are mirrored copies in the format each tool expects.

---

## 💡 What Makes False9 Different

Most tools check if your code **runs**. False9 checks if it does the **right thing**.

| Traditional Tools | False9 |
|:---|:---|
| Lints syntax errors | Traces execution paths and finds dead logic |
| Runs `npm audit` | Traces data flow from input to database to response |
| Checks if API returns 200 | Verifies response shape matches what the frontend destructures |
| Measures test coverage % | Asks *"if I deleted this feature, would any test fail?"* |
| Checks if LLM call succeeds | Runs 5-point test suite including adversarial inputs |
| Validates Dockerfile syntax | Simulates a full cold deploy and finds which step breaks |
| Suggests "add tests" | Writes behavioral tests for auth flows, form submissions, and error states |

---

## 🗺️ Roadmap

- [ ] **VS Code Extension** — Run False9 directly from the editor
- [ ] **CI/CD Integration** — GitHub Action for automated audits on every PR
- [ ] **Custom Agent SDK** — Build and plug in your own domain-specific agents
- [ ] **Multi-Language Support** — Python, Go, Rust backend detection
- [ ] **Dashboard** — Visual audit history and trend tracking
- [ ] **Team Mode** — Assign human reviewers to flagged issues

---

## 🤝 Contributing

Contributions are welcome! False9 is designed to be extended.

### Adding a New Agent

1. Create a new file in `.claude/agents/` following the naming convention `f9-{domain}.md`
2. Define: **RECON** (what to scan), **FIX** (what to repair), **OUTPUT** (structured JSON report)
3. Add the agent to the spawn list in `f9-manager.md`
4. Add the agent's domain to the Synthesizer's verification pass
5. Submit a PR

### Guidelines

- Each agent must be fully self-contained — no dependencies between agents
- Follow the existing output JSON schema for compatibility with the Synthesizer
- Agents should fix issues, not just report them
- Never inflate scores — only count verified fixes

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<div align="center">

**False9** — *The dream team you never had.*

Built by [Daud Ibrahim Hasan](https://github.com/daudibrahimhasan)

</div>