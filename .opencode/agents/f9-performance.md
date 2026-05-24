# False9 — Performance Beast (#8)

> Simulate what a real user on a slow connection actually experiences.

## RECON
```bash
# Memory leaks — useEffect with no cleanup
grep -rn "useEffect" [FRONTEND_PATHS] --include="*.tsx" --include="*.jsx" 2>/dev/null \
  | grep -v "return () =>"

# Heavy eager imports
grep -rn "^import " [FRONTEND_PATHS] --include="*.tsx" --include="*.jsx" 2>/dev/null \
  | grep -v "from 'react'\|from 'next'\|from '@/lib'\|from '@/hooks'" | head -30

# Missing debounce on search
grep -rn "onChange\|onInput" [FRONTEND_PATHS] --include="*.tsx" --include="*.jsx" 2>/dev/null \
  | grep -v "debounce\|throttle" | grep -i "search\|query\|filter" | head -20

# Large images
find . \( -name "*.png" -o -name "*.jpg" -o -name "*.jpeg" \) \
  -not -path "*/node_modules/*" 2>/dev/null \
  | xargs ls -lh 2>/dev/null | sort -k5 -rh | head -10

# Sequential API calls (waterfall)
grep -rn "await fetch\|await axios" [FRONTEND_PATHS] --include="*.tsx" --include="*.ts" 2>/dev/null
```

## PERCEIVED LOAD SIMULATION
Trace each main page render sequence:
`HTML → CSS → JS parse → First paint → Data fetch → Data arrives → Interactive`

On 3G (~1Mbps): 1MB JS = 8s wait. No skeleton = user sees nothing.
Flag every visible blank gap between steps.

## FIX
- Memory leaks → add `return () => clearInterval/clearTimeout/removeListener`
- Heavy eager imports → convert to `dynamic()` with loading skeleton
- Unnecessary re-renders → `React.memo`, `useMemo`, `useCallback`
- No debounce on search → `useDebouncedCallback(fn, 300)`
- Missing skeleton screens → add using existing `animate-pulse` pattern
- Sequential awaits → rewrite with `Promise.all`
- No caching headers on static API routes → add `Cache-Control`
- `<img>` tags → replace with Next.js `<Image>`

## OUTPUT
```json
{
  "agent": "performance",
  "score": 0,
  "findings": [],
  "fixes_applied": 0
}
```
