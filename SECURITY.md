# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| latest  | :white_check_mark: |
| < 1.0   | :x:                |

We release security patches for the latest version only. Please upgrade promptly.

## Reporting a Vulnerability

**Do not open a public issue for security vulnerabilities.**

Instead, send a detailed report to **security@zenstats.dev** (or open a private security advisory on GitHub if available).

Include:

- A clear description of the vulnerability
- Steps to reproduce (proof-of-concept code if possible)
- Affected component(s): API backend, frontend panel, Tracker JS SDK, or deployment
- Any potential impact or exploit scenarios

### What to expect

| Timeline | Step |
|----------|------|
| < 48 hours | We acknowledge receipt and begin triage |
| < 7 days | We confirm the vulnerability and assess severity |
| < 30 days | We release a patch and publish a security advisory |

We follow a coordinated disclosure process: once a patch is available, we'll publish a [GitHub Security Advisory](https://github.com/zenstats/zenstats/security/advisories) and credit the reporter (unless you prefer to remain anonymous).

## Scope

The following are **in scope** for security reports:

- **API backend** — Authentication bypass, JWT weaknesses, SQL injection, data leaks
- **Tracker JS** — XSS vectors, data exfiltration, cross-origin leaks
- **Deployment** — Container escape, default credentials, insecure configurations
- **Frontend panel** — CSRF, session fixation, stored XSS

The following are **out of scope**:

- Missing HTTP security headers (unless exploitable)
- Clickjacking on pages without sensitive actions
- Denial of service via event flooding (rate limiting is a feature, not a security boundary)
- Issues in third-party dependencies that have no known exploit

## Best Practices for Deployers

- Always set a strong `ZENSTATS_SECRET_KEY` in production (generate with `openssl rand -base64 32`)
- Change the default `DB_PASSWORD`
- Run behind HTTPS (Caddy handles this automatically)
- Keep Docker images updated to the latest tag
- Restrict network access to database ports (5432, 9000) — they should not be publicly exposed
