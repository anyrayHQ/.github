<!--
Thanks for contributing to Anyray. Keep PRs focused — one logical change each.
See CONTRIBUTING.md: https://github.com/anyrayHQ/.github/blob/main/CONTRIBUTING.md
Do NOT paste prompt/response content, provider keys, ANYRAY_* secrets, content keys,
admin tokens, or .env values anywhere in this PR.
-->

## What & why

<!-- What does this change do, and why? Link the issue it closes. -->

Fixes #

## How I verified it

<!-- Commands run, tests added, manual checks. Paste metadata-only output (no message bodies). -->

## Product invariants

<!-- Anyray sits on the path of every LLM request. Confirm this change keeps the invariants (see CONTRIBUTING.md). -->

- [ ] **Content privacy** — no prompt/response content is logged, traced, or persisted as plaintext; content stays encrypted at rest.
- [ ] **Spend governance** — every request stays attributable in the content-free spend store.
- [ ] **Single admin key** — the console and every `/admin/*` API stay behind the one admin key.
- [ ] **Fail open** — the optimizer stays a best-effort hook; if it's slow or down, the gateway forwards the original request untouched.
- [ ] N/A — this change doesn't touch the request path.

## Checklist

- [ ] Branched off `main`; one logical change per PR.
- [ ] Followed the conventions of the repository I'm changing.
- [ ] Ran the repo's checks/tests (see its README) and they pass.
- [ ] For deployment changes, the stack still comes up with `docker compose up -d`.
- [ ] Updated any affected documentation.
- [ ] Added tests where it makes sense.
