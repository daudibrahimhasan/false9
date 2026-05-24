# False9 — DevOps Engineer (#11)

> Simulate a cold deploy. Find every step that would fail. Fix it.

## RECON
```bash
find . -maxdepth 2 \
  \( -name "Dockerfile*" -o -name "docker-compose*" -o -name ".env*" \
     -o -name "*.yaml" -o -name "*.yml" -o -name "vercel.json" -o -name "fly.toml" \) \
  -not -path "*/node_modules/*" 2>/dev/null

cat package.json 2>/dev/null | python3 -c "
import json,sys; p=json.load(sys.stdin); print(json.dumps(p.get('scripts',{}), indent=2))"

grep -rn "process\.env\." . --exclude-dir=node_modules \
  --include="*.ts" --include="*.tsx" --include="*.js" 2>/dev/null \
  | grep -oP "process\.env\.\K[A-Z_]+" | sort -u
```

## COLD DEPLOY SIMULATION
Walk through step by step:
```
1. git clone          → any missing setup docs?
2. npm install        → native deps needing system packages?
3. Set env vars       → all vars documented in .env.example?
4. npm run build      → builds on clean machine?
5. npm run start      → port configurable? migrations run first?
6. Health check       → /health endpoint exists?
7. First request      → DB ready? migrations applied?
```
Flag every step that would fail.

## FIX
- No Dockerfile → generate for detected stack
- No .env.example → scan all `process.env.*` references, generate with grouped docs
- No health check → create `/api/health` with DB connectivity check
- No structured logging → add `lib/logger.ts`
- No .dockerignore → generate
- Migrations not in start script → add `prisma migrate deploy` before start
- Missing build script → add

## OUTPUT
```json
{
  "agent": "devops",
  "score": 0,
  "findings": [],
  "fixes_applied": 0
}
```
