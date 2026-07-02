# Secure Zenodo API Token Management (Reference Repository)

This repository is a **learning/reference project** that demonstrates secure patterns for using Zenodo API tokens.

> [!WARNING]
> **Never commit real tokens, credentials, or secrets to this repository.**

## Purpose

Use this repository to learn how to:
- Keep secrets out of source control
- Use local environment variables safely
- Store production secrets in GitHub Secrets
- Integrate with the Zenodo API without exposing tokens

## Security Principles

1. Do not hardcode tokens in code.
2. Do not commit `.env` or credential files.
3. Use GitHub Secrets for CI/CD.
4. Rotate/revoke tokens immediately if exposure is suspected.
5. Prefer least-privilege tokens where possible.

## Repository Structure

- `.env.example` — template for local development variables (safe placeholders only)
- `.github/workflows/secure-zenodo-example.yml` — GitHub Actions example using secrets
- `SECURITY.md` — vulnerability disclosure and incident response guidance
- `.gitignore` — guardrails to avoid committing secrets

## Local Setup (Secure)

1. Copy the example env file:
   - `cp .env.example .env`
2. Edit `.env` locally and add your real token value.
3. Keep `.env` private and untracked (already ignored by `.gitignore`).
4. Load values at runtime from environment variables.

## Example: Python Integration

```python
import os
import requests

token = os.getenv("ZENODO_TOKEN")
if not token:
    raise RuntimeError("ZENODO_TOKEN is not set")

resp = requests.get(
    "https://zenodo.org/api/deposit/depositions",
    params={"access_token": token},
    timeout=30,
)
resp.raise_for_status()
print(resp.json())
```

## GitHub Secrets Setup

1. Open your repository settings.
2. Go to **Secrets and variables** → **Actions**.
3. Add a secret named `ZENODO_TOKEN`.
4. Reference it in workflows as `${{ secrets.ZENODO_TOKEN }}`.

## If a Token Is Exposed

1. Revoke/rotate token immediately in Zenodo.
2. Remove leaked material from repository history.
3. Replace with new credentials.
4. Review logs/workflows for unauthorized usage.
5. Document incident and preventive actions.

See `SECURITY.md` for disclosure details.
