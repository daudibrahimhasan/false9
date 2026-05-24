# False9 — LLM Validator (#10)

> Not just is it working. Is it doing the RIGHT thing.

## MAP LLM CALLS
```bash
grep -rn "openai\.\|anthropic\.\|groq\.\|streamText\|generateText\|useChat\|\.messages\.create\|\.chat\.completions" \
  . --exclude-dir=node_modules \
  --include="*.ts" --include="*.tsx" --include="*.js" --include="*.py" 2>/dev/null
```

For each call site, read the full function: prompt, parser, how output hits UI.

## DETECT INTENT
Per call, build: `Feature / Intent / Expected output format`
If intent unclear → `NEEDS_HUMAN_REVIEW`, skip.

## LIVE TEST (5 per feature)
```
Test 1: Normal input
Test 2: Short input (1 word / 1 sentence)
Test 3: Long input (near context limit)
Test 4: Empty input
Test 5: Adversarial (gibberish / prompt injection)
```
Score each: Relevance / Accuracy / Format / Safety (0–100)

## DIAGNOSE FAILURES (in order)
1. PROMPT — vague, missing context, wrong for this feature?
2. PARSER — extracting response correctly for this SDK?
3. VALIDATION — output validated before hitting UI?
4. ERROR_HANDLING — try/catch, fallback, loading state?
5. MODEL — capable enough for this task?

**SDK parsing:**
```typescript
// OpenAI:    response.choices[0].message.content
// Anthropic: response.content[0].text
// Vercel AI: result.text
```

## FIX IN ORDER
1. Rewrite prompt — clear task, expected format, output constraints
2. Fix parser — match actual SDK
3. Add output validation — check empty/wrong format before UI
4. Add error handling — try/catch + user-visible error + loading state
5. Update model string — never change provider

**Outdated models:**
```
gpt-3.5-turbo → gpt-4o-mini
claude-v1 / claude-instant → claude-3-5-haiku-20241022
mixtral-8x7b → llama-3.1-8b-instant
```

## RETEST
Rerun 5 tests after every fix. Mark complete only when all 5 pass.
2 failed attempts → `NEEDS_HUMAN_REVIEW`.

## OUTPUT
```json
{
  "agent": "llm_validator",
  "score": 0,
  "findings": [],
  "llm_calls_found": 0,
  "llm_calls_fixed": 0,
  "needs_human_review": []
}
```
