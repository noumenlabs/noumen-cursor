---
name: second-opinion
description: Get a second opinion on code from another AI model through Noumen, or compare how several models review the same change. Use before merging a risky change, when stuck on a bug, to review a smart contract, or when the user asks what another model thinks.
---

# Second opinion with Noumen models

`ask` and `compare` need a Noumen API key in `NOUMEN_API_KEY`. Each call is billed per token to that key.

## When to use

- The user asks for a review, a second opinion, or "what would another model say".
- A change is risky: security-sensitive code, a migration, a smart contract, concurrency, money handling.
- You have tried twice to fix a bug and want an independent look.

## Instructions

1. Pick a model. Call `list_models` with `capability: "tools"` or `"reasoning"` and choose one whose `context_length` fits the code you will send. Prefer a different model family from your own.
2. Build a self-contained prompt: the question, the relevant code or diff, the error message and what you already tried. The model sees nothing else. Redact secrets.
3. Call `ask` with `model` and `prompt`. Add `system` for the reviewer's role, `reasoning_effort` for hard problems, and `max_tokens` to cap the cost.
4. For several views, call `compare` with two to four models and the same prompt.
5. Weigh the answer against the code: verify every claim before acting on it, and say where you disagree.
6. Tell the user the model, the tokens and the estimated cost from the result. `balance` shows what is left on the key.

## Prompt template for a review

```
Review this change for correctness bugs, security problems and edge cases. List each issue with the line, why it is wrong and the fix. Say "no issues" if there are none.

Context: <what the code does and where it runs>

<diff or code>
```

## Without a key

`ask` returns how to get one: a free 24-hour demo key at https://www.noumen.xyz/docs#try, or a prepaid key in the Noumen app under API access. Set `NOUMEN_API_KEY` and restart the editor.
