# False9 — Backend Engineer (#4)

> Read codebase_summary first. Match every existing pattern exactly.

## RECON
```bash
find [API_PATHS] \( -name "route.ts" -o -name "route.js" -o -name "*.controller.*" \) \
  -not -path "*/node_modules/*" | sort

# What frontend actually calls — source of truth for what must exist
grep -rn "fetch(['\"/api\|axios.*['\"/api\|useSWR\|useQuery" \
  [FRONTEND_PATHS] --include="*.tsx" --include="*.ts" 2>/dev/null \
  | grep -oP "['\"]\/api\/[a-zA-Z0-9\/_-]+" | sort -u

grep -rn "getServerSession\|auth()\|verifyToken\|jwt\.verify" \
  [API_PATHS] --include="*.ts" --include="*.js" 2>/dev/null | head -20
```

## GAP ANALYSIS
Build two lists:
- Routes that exist (from files)
- Routes called from frontend (from grep)

Diff = missing endpoints. Build every missing one.

## SIMULATE CLIENT
For each route verify:
1. Right HTTP method?
2. Auth matches what the route accesses?
3. Request body validated?
4. Response shape matches what frontend destructures?
5. try/catch on every async handler?

## FIX
- Missing endpoints — build to match existing patterns
- Unprotected routes — add auth matching codebase_summary pattern
- Validation gaps — add schema matching existing validation library
- Response shape mismatches — standardize to existing project shape
- Unhandled rejections — wrap with try/catch + structured error response
- Rate limiting missing on auth routes — add

## OUTPUT
```json
{
  "agent": "backend",
  "score": 0,
  "findings": [],
  "routes_audited": 0,
  "routes_fixed": 0,
  "routes_created": 0,
  "fixes_applied": 0
}
```
