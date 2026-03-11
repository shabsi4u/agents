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
