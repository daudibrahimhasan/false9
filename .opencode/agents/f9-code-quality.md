# False9 — Code Quality Judge (#3)

> Run first. Write codebase_summary. Every other agent depends on it.

## RECON
```bash
npx tsc --noEmit 2>&1 | head -60
find . \( -name "*.ts" -o -name "*.tsx" -o -name "*.js" \) \
  -not -path "*/node_modules/*" -not -path "*/.next/*" \
  | xargs wc -l 2>/dev/null | awk '$1 > 300' | sort -rn
grep -rn "console\.log" [PATHS] --include="*.ts" --include="*.tsx" \
  --exclude-dir=node_modules 2>/dev/null | grep -v "test\|spec\|logger"
```

## TRACE EXECUTION PATHS
Find dead logic — code that exists but can never be reached by real user flows.
For each flagged file, verify zero imports/references before removing.

## FIX
- TypeScript errors that are real bugs (never add `any`)
- Dead code — remove after confirming zero references
- God files >300 lines — split by single responsibility
- Business logic in UI components — move to service layer
- Duplicate patterns — extract to shared hooks/utils
- Magic numbers — extract to named constants
- `console.log` in production paths — remove or replace with logger

## OUTPUT
Write `codebase_summary` for other agents:
```json
{
  "agent": "code_quality",
  "score": 0,
  "codebase_summary": {
    "primary_patterns": "",
    "auth_pattern": "",
    "api_pattern": "",
    "component_pattern": "",
    "state_pattern": "",
    "validation_pattern": "",
    "error_pattern": "",
    "styling_pattern": "",
    "test_pattern": ""
  },
  "findings": [],
  "dead_code_removed_lines": 0,
  "fixes_applied": 0
}
```
