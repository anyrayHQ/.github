# Security Policy

Anyray is built to sit on the path of an organization's most sensitive traffic — employees'
source code and proprietary data — so we take security seriously. This is the default policy for
all [Anyray](https://github.com/anyrayHQ) repositories.

## Reporting a vulnerability

**Please do not open a public issue, pull request, or discussion for security vulnerabilities.**

Report it privately by **email** → **[support@anyray.ai](mailto:support@anyray.ai)** with the
subject line `SECURITY:` and a description of the issue.

Please include, where you can:

- the affected component (gateway, optimizer, console, `anyray-connect`, control plane) and
  version or commit,
- a description of the issue and its impact,
- steps to reproduce or a proof of concept,
- any suggested remediation.

⚠️ **Do not include real prompt/response content, provider API keys, `ANYRAY_*` secrets, content
keys, or admin tokens** in your report. A redacted reproduction is enough.

## What to expect

- **Acknowledgement** within **3 business days**.
- An initial assessment and severity triage shortly after.
- Regular updates as we work on a fix, and credit for the report once a fix ships (unless you'd
  prefer to remain anonymous).

We ask that you give us a reasonable window to release a fix before any public disclosure. We
will coordinate disclosure timing with you.

## Supported versions

| Version | Supported |
| ------- | --------- |
| 1.x     | ✅ |
| < 1.0   | ❌ |

Security fixes land on the latest `1.x` release line.

## Scope & safe harbor

In scope: code in Anyray-owned repositories and the default self-hosted deployment. Because
Anyray is **self-hosted**, the security of any given deployment also depends on how the operator
configures it — see the hardening guidance in
[docs.anyray.ai/operate/security](https://docs.anyray.ai/operate/security) (content modes,
the single admin key, public-exposure setup, and the L7 abuse controls).

We support good-faith security research. If you make a good-faith effort to comply with this
policy — avoiding privacy violations, data destruction, and service disruption, and using only
your own test deployments — we will not pursue or support legal action against you for that
research.

## Our security posture

For background on why Anyray is designed to be low-risk on the request path:

- **Content never leaves** — self-hosted, zero egress by default; content encrypted at rest
  (AES-256-GCM).
- **Metadata-only logs and traces** — humans see ciphertext, never message bodies.
- **The optimizer is credential-free and fails open** — it never takes custody of provider keys
  or content, and a broken optimizer can never alter inference.

See the [data boundary](https://docs.anyray.ai/operate/data-boundary) and
[security](https://docs.anyray.ai/operate/security) docs for the full model.
