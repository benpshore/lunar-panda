# lunar-panda

- Agents must work on a branch and open a PR (`gh pr create --fill`); never push directly to `main` or use the owner's bypass, even when authenticated as the owner.
- The `ci` check must pass for agent-authored work. Only the human owner's own work may use the direct-push exception.
- Never commit secrets, `.env` files, databases or `.DS_Store` (see `.gitignore`; CI rejects them).
- Python: use **uv** only (`uv add`, `uv run`). Never pip.
- The version is the git tag; never edit a version field by hand.
- Every merge to `main` is released automatically (next minor version, wheel and sdist attached).
- Before committing, run:

```sh
uv run ruff format && uv run ruff check && uv run pytest && uv audit --preview-features audit-command
npx @stoplight/spectral-cli lint openapi.yaml
sqlite3 -bail :memory: ".read sqlite/schema.sql"   # the app opens ${APP_DATA:-.}/app.db
```
