# Security Policy

## Supported Versions

Cinnamon Terminal follows a CalVer release scheme with LTS releases.
Only the following versions receive security updates:

| Version | Supported          |
|---------|--------------------|
| Latest LTS | ✅ Supported |
| Latest standard release | ✅ Supported |
| Older LTS (< 2 releases ago) | ⚠️ Critical CVEs only |
| Anything else | ❌ Not supported |

LTS releases receive security backports for **18 months** from their release date.
Standard releases are supported until the next release.

## Reporting a Vulnerability

If you discover a security vulnerability in Cinnamon Terminal, please report it
privately. **Do not disclose it publicly until we have had a chance to address it.**

### How to Report

1. **Email:** security@acreetionos.org
2. **PGP Key:** [Download our PGP key](https://acreetionos.org/.well-known/pgp-key.asc)
   - Fingerprint: `XXXX XXXX XXXX XXXX XXXX  XXXX XXXX XXXX XXXX XXXX`
   - Key ID: `0xXXXXXXXXXXXXXXXX`
   - Always encrypt sensitive reports.

If you do not receive a response within **48 hours**, please escalate to:
- **natalie@acreetionos.org** (project maintainer)
- Or file a **confidential issue** on the [GitLab repository](https://gitlab.acreetionos.org/acreetionos-code/cinnamon-terminal/-/issues/new)
  with the `~security` label and **check "This issue is confidential"**.

### What to Include

Please provide as much of the following as possible:

- Description of the vulnerability
- Steps to reproduce (PoC preferred)
- Affected versions
- Potential impact
- Suggested fix (if known)
- Your name/alias for credit (optional)

### Response Timeline

| Timeframe | Action |
|-----------|--------|
| 0–24 hours | Acknowledgment of receipt |
| 24–72 hours | Initial triage and severity assessment |
| 1–7 days | Fix in development (depending on severity) |
| 7–30 days | Patch released for supported versions |
| Post-release | CVE assignment and public disclosure |

### Disclosure Policy

- We will notify you before public disclosure
- We will credit you in the release notes and CVE (unless you prefer anonymity)
- We aim to coordinate disclosure within 30 days of the initial report

## Security Measures

This project employs the following security practices:

- **Signed commits:** All commits to `master` must be GPG-signed
- **Static analysis:** clang-tidy and SAST scanning run on every commit
- **Dynamic analysis:** AddressSanitizer and UndefinedBehaviorSanitizer builds in CI
- **Dependency scanning:** Automated scanning for known vulnerabilities
- **Branch protection:** `master` requires MRs with pipeline success
- **Code review:** Every merge requires at least 1 approval
- **Push mirrors:** Read-only; no code flows back upstream

## Known Security Issues

See [GitLab Issues labeled ~security](https://gitlab.acreetionos.org/acreetionos-code/cinnamon-terminal/-/issues?label_name%5B%5D=security)
for publicly disclosed issues.
