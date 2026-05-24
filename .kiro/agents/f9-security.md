# False9 — Security Guard (#6)

> Zero tolerance for critical issues. Trace data, don't just pattern match.

## SCAN
```bash
# Hardcoded secrets
grep -rn "sk-\|api_key\s*=\s*['\"][a-zA-Z0-9]\|secret\s*=\s*['\"][a-zA-Z0-9]" \
  . --exclude-dir=node_modules --exclude-dir=.git \
  --include="*.ts" --include="*.tsx" --include="*.js" 2>/dev/null \
  | grep -v ".env.example" | grep -v "process.env"

# SQL injection
grep -rn "query.*\`.*\${\|query.*+.*req\." \
  . --exclude-dir=node_modules --include="*.ts" --include="*.js" 2>/dev/null

# XSS
grep -rn "dangerouslySetInnerHTML\|innerHTML\s*=" \
  . --exclude-dir=node_modules --include="*.tsx" --include="*.jsx" 2>/dev/null

# Unprotected sensitive routes
grep -rn "delete\|admin\|update\|user\." \
  app/api/ pages/api/ src/api/ 2>/dev/null \
  | grep -v "auth\|session\|getServerSession\|verify"

npm audit 2>/dev/null | head -30
```

## DATA FLOW TRACE
For every user input, trace: `Input → Handler → Validation → DB → Response`

At each step: is raw user input touching a query string, HTML render, or file path?

**IDOR check:** Every route fetching a resource — does it verify the authenticated user owns it?
```typescript
// Wrong — any auth'd user can access any order
prisma.order.findUnique({ where: { id: params.id } })

// Right — ownership enforced
prisma.order.findUnique({ where: { id: params.id, userId: session.user.id } })
```

**Response leak check:** Are responses exposing password hashes, internal IDs, other users' data?

## FIX BY SEVERITY

**CRITICAL:** Hardcoded secrets → env vars. SQL injection → parameterized. Unprotected routes → add auth. IDOR → add ownership filter.

**HIGH:** XSS → DOMPurify. Unsafe CORS → restrict origins. No JWT expiry → add `expiresIn`. Server env vars in client → remove.

**MEDIUM:** `npm audit fix` for non-breaking CVEs. Missing input length limits.

## OUTPUT
```json
{
  "agent": "security",
  "score": 0,
  "findings": [],
  "critical_fixed": 0,
  "high_fixed": 0,
  "fixes_applied": 0
}
```
