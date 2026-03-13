# Agents Project

## Git & GitHub

- Identity: personal
- SSH remote: git@github.com-personal:shabsi4u
- gh CLI: not available (gh CLI is authenticated to work account `shabs-nvt`)

### Remotes

| Remote   | URL                                          | Purpose                        |
|----------|----------------------------------------------|--------------------------------|
| origin   | git@github.com-personal:shabsi4u/agents.git  | Personal fork (push/PR here)   |
| upstream | https://github.com/ed-donner/agents          | Course upstream (fetch only)   |

### Local git identity

- `user.name`: shabsi4u
- `user.email`: shabareesh.r@gmail.com

### Common workflows

```bash
# Pull latest from upstream course repo
git fetch upstream
git merge upstream/main

# Push your work to your fork
git push origin main

# Create a PR: gh CLI won't work (wrong account), use this URL instead:
# https://github.com/shabsi4u/agents/pull/new/<branch>
```

### Notes

- Do NOT use `gh` CLI for PR creation or GitHub API calls — it's authenticated as `shabs-nvt` (work account) and will fail with "Could not resolve to a Repository".
- Always use the `git@github.com-personal:` SSH alias for origin to avoid authentication issues.

## Coding Standards

### Python — common mistakes to avoid

1. **Always verify function return values.** If a function accumulates results into a local variable, confirm there is an explicit `return` at the end. A missing `return` silently produces `None`, which causes `TypeError` when the caller tries to iterate or extend with it.

2. **Dict keys must be string literals.** In dict literals, bare words like `{type: "function"}` are valid Python — `type` resolves to the built-in `type` class, making the key a non-string object. JSON serialization then fails with `TypeError: keys must be str, int, float, bool or None, not type`. Always quote dict keys: `{"type": "function"}`.

3. **Trace data flow end-to-end before finishing.** For every function that produces data consumed by a caller, mentally follow the value from creation → return → use site before writing the code. Don't assume a function returns something just because it builds something.

5. **Tool schema `"name"` must exactly match the Python function name.** The agentic loop dispatches tool calls via `globals().get(tool_name)` — if the schema name and function name differ, the lookup silently returns `None`. Never use `tool if tool else {}` as a fallback; raise a `ValueError` immediately so the mismatch is caught at dev time, not masked at runtime.

4. **Always instantiate classes before calling instance methods.** `Console.print(...)` calls `print` as an unbound method on the class — it silently falls through or errors. Always use `Console().print(...)`. The bare `except Exception: print(text)` pattern is especially dangerous here: it masks the failure and produces output that looks correct but has lost all formatting.
