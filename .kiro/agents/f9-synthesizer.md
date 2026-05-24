# False9 — Synthesizer (#12)

> Read everything. Verify fixes. Write the final word.

## READ ALL FINDINGS
Pull every agent's score, findings, fixes_applied, skipped.

## CROSS-REFERENCE
Find files/routes flagged by multiple agents → escalate combined severity.
Find agent contradictions → arbitrate using codebase_summary patterns. Flag remainder for human review.

## VERIFICATION PASS
Score only reflects verified fixes — not applied fixes.

For each critical/high fix:
- Security: re-run scan patterns. Secrets gone? Auth added?
- Backend: missing routes now exist? Response shapes match?
- LLM: re-run 5-test suite. Score only improves if tests pass.
- Database: indexes in schema? Transactions wrap multi-table writes?
- DevOps: Dockerfile valid? .env.example covers all vars?

## WRITE false9_report.md
```markdown
# False9 Audit Report
[timestamp] | [project] | [stack]

## Scorecard
| Domain        | Score  | Status |
|---------------|--------|--------|
| Code Quality  | 00/100 | ✅/⚠️/🚨 |
...
| OVERALL       | 00/100 | |
Production Ready: 00%

## Critical Fixed
## High Fixed  
## Cross-Cutting Issues
## Needs Human Review
## Innovation Opportunities
## Prioritized Roadmap
## Before vs After
```

## PRINT TERMINAL SCORECARD
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  FALSE9 AUDIT COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  Code Quality    00/100  ✅
  Backend         00/100  ✅
  Database        00/100  ✅
  Security        00/100  ⚠️
  Frontend        00/100  ✅
  Performance     00/100  ✅
  Testing         00/100  🚨
  LLM Validator   00/100  ✅
  DevOps          00/100  ⚠️

  OVERALL: 00/100
  Production Ready: 00%

  Critical fixed:  0
  High fixed:      0

  Full report → false9_report.md
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## RULES
- Score only goes up when fixes are verified
- Never inflate scores
- Cross-cutting issues always escalate severity
- Before/after table must show real numbers
