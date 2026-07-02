# Security Policy

## Supported Use

This repository is a secure-reference example for token handling. It is not intended to store real secrets.

## Reporting a Vulnerability

If you discover a security issue in this repository or believe a secret has been exposed:

1. **Do not** open a public issue containing sensitive details.
2. Contact the maintainer privately through GitHub security reporting channels.
3. Include steps to reproduce, impact, and affected files/workflows.

## Response Expectations

- Initial triage target: within 7 days
- Status update target: within 14 days
- Fix/remediation timeline: based on severity and reproducibility

## Secret Exposure Playbook

If a token is accidentally committed or exposed:

1. Revoke/rotate the token immediately at the provider (Zenodo).
2. Remove exposed data from history and force-push cleaned history if needed.
3. Replace with secure secret references (environment variables or GitHub Secrets).
4. Audit recent activity for suspicious usage.
5. Document prevention steps and update repository safeguards.

## Best Practices

- Never hardcode secrets in code or docs.
- Use `.env.example` for templates only.
- Use GitHub Secrets for automation.
- Limit token scope and rotate regularly.
