<div align="center">

```
╔═══════════════════════════════════════════════════════════╗
║                                                           ║
║   ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   ║
║   ░  ·  ·  ○  ·  ·  ·  · │ ·  ·  ·  ·  ●  ·  ·  ·  ░   ║
║   ░  ·  ●  ·  ·  ●  ·  · │ ·  ·  ○  ·  ·  ·  ○  ·  ░   ║
║   ░  ·  ·  ·  ·  ·  ○  · │ ·  ·  ·  ·  ·  ●  ·  ·  ░   ║
║   ░  ·  ·  ●  ·  ·  ·  · │ ·  ·  ·  ○  ·  ·  ·  ·  ░   ║
║   ░·····················(✦)·····················░   ║
║   ░  ·  ·  ○  ·  ·  ·  · │ ·  ·  ·  ·  ●  ·  ·  ·  ░   ║
║   ░  ·  ●  ·  ·  ●  ·  · │ ·  ·  ○  ·  ·  ·  ○  ·  ░   ║
║   ░  ·  ·  ·  ·  ·  ○  · │ ·  ·  ·  ·  ·  ●  ·  ·  ░   ║
║   ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   ║
║                                                           ║
║              F  A  L  S  E  9                             ║
║       Total football for your codebase.                   ║
║                                                           ║
║            ● White  ○ Red  ✦ Ball                        ║
╚═══════════════════════════════════════════════════════════╝
```

</div>

---

An autonomous AI engineering organization that lives inside Claude Code.  
Audits and completes software projects.

---

## The Problem

You have projects in various states of broken. Half made. Partially made. Full but with broken features. LLM calls not working. Placeholder content. No army to fix it.

False9 is the army.

---

## What It Does

One command. 11 agents spawn simultaneously. Every domain covered in parallel. Final scored report written to your project root.

```
/f9-audit      → full engineering review + fix everything found
/f9-complete   → reconstruct intent + complete unfinished work + audit
```

---

## The Squad

| # | Agent | Domain |
|---|-------|--------|
| 1 | Manager | Orchestrates everything |
| 2 | Code Quality Judge | Dead code, structure, patterns |
| 3 | Backend Engineer | APIs, auth, validation, missing endpoints |
| 4 | Database Specialist | Queries, indexes, transactions, scale |
| 5 | Security Guard | Secrets, injections, IDOR, data flow |
| 6 | Frontend Architect | UI completion, wiring, placeholders |
| 7 | Performance Beast | Leaks, bundles, perceived load time |
| 8 | Testing Captain | Coverage, flaky tests, behavioral assertions |
| 9 | LLM Validator | Tests AI features do the RIGHT thing |
| 10 | DevOps Engineer | Cold deploy simulation, Docker, env vars |
| 11 | Innovation Consultant | Quick wins, revenue gaps, AI opportunities |
| 12 | Synthesizer | Cross-references all findings, final report |

---

## Install

```bash
cp -r .claude/commands/f9-* ~/.claude/commands/
cp -r .claude/agents/f9-* ~/.claude/agents/
```

Requires [Claude Code](https://claude.ai/code).

---

## Usage

Open any project in Claude Code and run:

```
/f9-audit
```

or

```
/f9-complete
```

Report is written to `false9_report.md` in your project root.

---

## How It Works

```
/f9-audit
    ↓
Manager: project recon + stack detection
    ↓
11 agents spawn simultaneously
Each reads its domain, fixes what it finds, reports
    ↓
Synthesizer: cross-references all findings
Escalates issues flagged by multiple agents
Verifies fixes before scoring
    ↓
false9_report.md + terminal scorecard
```

---

## Output

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  FALSE9 AUDIT COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
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
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## What Makes It Different

Most tools check if your code runs. False9 checks if it does the right thing.

- **LLM Validator** runs live tests — not just "API returns 200" but "is this the correct output?"
- **Security Guard** traces data flow — finds IDOR and logic-level auth flaws no scanner catches
- **Backend Engineer** simulates a client — verifies response shapes match what the frontend expects
- **DevOps Engineer** simulates a cold deploy — finds exactly which step would fail
- **Synthesizer** cross-references — issues flagged by multiple agents get escalated automatically

---

*False9. Total football for your codebase.*