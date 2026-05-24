# Contributing to False9

Thanks for wanting to contribute! False9 is an open-source, multi-agent framework designed to support developers across all major AI coding environments.

## Table of Contents

- [What We're Looking For](#what-were-looking-for)
- [Quick Start](#quick-start)
- [Contributing Agents](#contributing-agents)
- [Contributing Commands](#contributing-commands)
- [Mirroring to All AI Tools](#mirroring-to-all-ai-tools)
- [Pull Request Process](#pull-request-process)
- [Guidelines](#guidelines)

---

## What We're Looking For

### Domain-Specific Agents
New agents to handle specific stacks or engineering domains:
- Framework experts (Django, Rails, Spring Boot, Laravel)
- Language-specific code judges (Rust, Go, Python)
- Platform engineers (Kubernetes, AWS, Terraform, Docker)

### Strategy Refinements
Enhancements to the prompt prompts or checklists of existing agents to make their recon and fixes more robust.

---

## Quick Start

```bash
# 1. Fork and clone the repository
gh repo fork daudibrahimhasan/false9 --clone
cd false9

# 2. Create a branch for your work
git checkout -b feat/add-kubernetes-agent

# 3. Add your agent or command under `.claude/` (canonical)
# (See instructions below)

# 4. Mirror changes to all tool directories
# (See Mirroring section below)

# 5. Push and submit a Pull Request
git add .
git commit -m "feat: add kubernetes specialist agent"
git push -u origin feat/add-kubernetes-agent
```

---

## Contributing Agents

Agents are self-contained markdown templates explaining the agent's role, instructions, and schemas.

### File Naming and Location
All new agents must start with the `f9-` prefix:
```
.claude/agents/f9-your-agent-name.md
```

### Agent Markdown Structure
Each agent must declare the following three core sections:
1. **RECON**: Instructions telling the agent what to inspect (files, structures, dependencies).
2. **FIX**: Instructions on how the agent should automatically repair issues in complete mode.
3. **OUTPUT**: A strict JSON schema specifying the exact report fields it must return (for compatibility with the Synthesizer).

```markdown
# False9 — Your Agent Name Specialist

## 🎯 Role & Objective
Explain who this agent is and what domain it governs.

## 🔍 RECON (What to Scan)
Detail the file patterns and directory structures to look at.

## 🛠️ FIX (What to Repair)
Detail the rules for applying fixes.

## 📋 OUTPUT (Report Schema)
Define the output schema format. Ensure the final response outputs a clean JSON block matching:
```json
{
  "domain": "YourDomain",
  "score": 100,
  "findings": []
}
```
```

---

## Contributing Commands

Commands define actions or shortcuts that can be run from the AI coding tool's command line interface.

### File Naming and Location
```
.claude/commands/f9-your-command-name.md
```

---

## Mirroring to All AI Tools

False9 maintains subfolders for all supported AI coding apps (Cursor, Copilot, Codex, Gemini, etc.). **`.claude/` is the canonical source directory.** 

After adding or modifying any agent or command in `.claude/`, you must sync the changes to all other tool directories before committing.

### Mirroring Script (PowerShell)
Run this command from the root of the repository:
```powershell
$tools = @('.cursor', '.codex', '.codebuddy', '.gemini', '.kiro', '.opencode', '.qwen', '.trae', '.zed'); foreach ($t in $tools) { Copy-Item ".claude\agents\*" "$t\agents\" -Force; Copy-Item ".claude\commands\*" "$t\commands\" -Force }; Copy-Item ".claude\agents\*" ".github\copilot\" -Force; Copy-Item ".claude\commands\*" ".github\copilot\" -Force
```

### Mirroring Script (Bash)
```bash
tools=(".cursor" ".codex" ".codebuddy" ".gemini" ".kiro" ".opencode" ".qwen" ".trae" ".zed")
for t in "${tools[@]}"; do
  cp -r .claude/agents/* "$t/agents/"
  cp -r .claude/commands/* "$t/commands/"
done
cp -r .claude/agents/* .github/copilot/
cp -r .claude/commands/* .github/copilot/
```

---

## Pull Request Process

### 1. Commit/PR Title Format
```
feat(agents): add kubernetes specialist agent
fix(agents): improve database query rules in f9-database
docs: add guide to CONTRIBUTING.md
```

### 2. PR Checklist
- [ ] Added/modified the agent in `.claude/`
- [ ] Mirrored the changes to all other tool folders (`.cursor`, `.github`, etc.)
- [ ] Handled only a single domain/feature
- [ ] Verified that JSON output schemas are consistent with the Synthesizer
- [ ] No API keys, credentials, or personal local paths committed

---

## Guidelines

### Do
- Keep agent prompt files fully self-contained.
- Follow the JSON report structure strictly.
- Make fixes conservative to avoid breaking functional code.

### Don't
- Inflate scores in the verification checks.
- Add third-party external dependencies for agents to work.
