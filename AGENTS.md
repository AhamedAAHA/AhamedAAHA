# AGENTS.md

## Project overview

This repository (`AhamedAAHA/AhamedAAHA`) is a **GitHub profile README**. The only tracked source file is `README.md`, which GitHub renders on the profile page. There is no application server, database, or package manifest in this repo.

## Cursor Cloud specific instructions

### Services

| Service | Required | Notes |
|---------|----------|-------|
| Local README preview (optional) | No | Use for local validation only; production rendering is on GitHub |

No long-running services are required for routine work on this repository.

### Lint / validate

There is no project-local linter configuration. For ad-hoc checks:

```bash
# Content validation (checks required profile fields)
python3 -c "
content = open('README.md').read()
assert 'Hubaib Ahamed' in content
assert 'hubaibahamedaaha@gmail.com' in content
print('README content OK')
"

# Optional markdown lint (expects HTML-heavy profile README warnings)
npx --yes markdownlint-cli README.md
```

`markdownlint` will report many `MD033` (inline HTML) and `MD012` (blank lines) findings — that is normal for GitHub profile READMEs that use HTML badges and widgets.

### Local preview (development)

To preview `README.md` in a browser without pushing to GitHub:

```bash
python3 << 'PYEOF'
from pathlib import Path
readme = Path('README.md').read_text()
html = f'''<!DOCTYPE html><html><head><meta charset="UTF-8"><title>README Preview</title></head><body>{readme}</body></html>'''
Path('/tmp/readme-preview').mkdir(parents=True, exist_ok=True)
Path('/tmp/readme-preview/index.html').write_text(html)
print('Wrote /tmp/readme-preview/index.html')
PYEOF
cd /tmp/readme-preview && python3 -m http.server 8080
```

Open `http://localhost:8080/`. External widgets (GitHub stats, profile views) load from third-party URLs and may be slow or temporarily unavailable (e.g. `github-readme-stats.vercel.app` returning 503).

### Tests / build

No automated test suite or build step exists in this repository.

### Gotchas

- **Wrong repo?** Cloud agent branch templates may reference other project names (e.g. smart-study-companion). If you expected an application codebase, confirm the correct repository was cloned.
- **Detached HEAD:** Check out `main` before creating branches: `git checkout main`.
- **No dependencies:** The VM update script is a no-op (`true`); nothing is installed from this repo on startup.
