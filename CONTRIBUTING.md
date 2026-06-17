# Contributing to Anyray

Thanks for taking the time to contribute. This is the **default** contributing guide for all
public [Anyray](https://github.com/anyrayHQ) repositories; an individual repo may add its own
`CONTRIBUTING.md` with project-specific detail.

By participating, you agree to abide by our [Code of Conduct](./CODE_OF_CONDUCT.md).

## Where things live

Anyray ships as a self-hosted **gateway + console + optimizer**. The pieces you can see and work
with publicly are:

- **Install & deploy:** [`anyrayHQ/install`](https://github.com/anyrayHQ/install) — the Docker
  Compose stack, cloud templates (Railway, Kubernetes, …), and the gateway/host **adapters** under
  `attach/`. This is the main public repo for issues and contributions.
- **Documentation:** [docs.anyray.ai](https://docs.anyray.ai).
- **Hosted portal:** [app.anyray.ai](https://app.anyray.ai) — sign-in, the setup wizard, and billing.

The gateway/optimizer/console **core** is developed in a separate, private repository; its product
behavior is documented at [docs.anyray.ai](https://docs.anyray.ai).

## Ground rules (product invariants)

Anyray sits on the path of every LLM request, so a few invariants are **non-negotiable**. A
change that breaks one of these is a correctness bug, not a trade-off:

1. **Content privacy.** Prompt/response *content* is never shown to humans in the clear and never
   logged as plaintext. It is encrypted at rest (AES-256-GCM). Logs, traces, and the spend store
   carry **metadata only** — user, team, model, provider, tokens, cost, latency, decision.
2. **Spend governance.** Every request stays attributable into the content-free spend store.
3. **Single admin key.** The console and every `/admin/*` API stay behind the one admin key.
4. **The gateway fails open.** The optimizer is a best-effort hook on the hot path — if it's slow
   or down, the gateway forwards the original request untouched. A broken optimizer can never
   break or alter inference.

If you're contributing an adapter or anything else that runs on the request path, keep these in
mind. When in doubt, open an issue before writing code.

## Reporting bugs & requesting features

Use the issue forms in [`anyrayHQ/install`](https://github.com/anyrayHQ/install/issues):

- 🐞 **Bug report** — what you expected, what happened, and the smallest reproduction. **Never
  paste prompt or response content, provider keys, `ANYRAY_*` secrets, or `.env` values** into an
  issue.
- ✨ **Feature request** — the problem you're trying to solve, not just the solution you have in
  mind.
- 📚 **Docs issue** — for [docs.anyray.ai](https://docs.anyray.ai).

🔒 **Security vulnerabilities do not go in the issue tracker.** Follow the
[Security Policy](./SECURITY.md).

## Making a change

1. **Discuss first for anything non-trivial.** Open or comment on an issue so we agree on the
   approach before you invest time.
2. **Fork / branch.** Branch off `main`. Never commit directly to `main`, and don't force-push
   shared branches.
3. **Follow the existing conventions.** Match the style and structure of the code and config
   around you; keep changes consistent with the patterns already in the repo.
4. **Keep deployments working.** For the install repo, make sure the stack still comes up with
   `docker compose up -d`, and exercise any template or adapter you touch. A new host adapter goes
   under `attach/<host>/`, following the existing adapters.
5. **Run the repo's checks.** Run whatever lint/build/test commands the repository documents in its
   README, and make sure they pass. CI runs the same on every PR.
6. **Docs are part of the change.** If you change documented behavior — env vars or defaults,
   endpoints, CLI commands, deployment steps — update the docs (or open a docs issue) alongside it.
7. **Add tests** for new behavior and bug fixes where the repo supports them.

## Opening a pull request

- Keep PRs focused — one logical change per PR.
- Fill out the [pull request template](./.github/PULL_REQUEST_TEMPLATE.md).
- Write a clear description: what changed, why, and how you verified it.
- Make sure CI is green. Maintainers review from there.

## Commit messages

Write imperative, present-tense subjects (`add bedrock adapter`, not `added`/`adds`). Explain the
*why* in the body when it isn't obvious. Reference issues with `Fixes #123` where applicable.

## License

Each Anyray repository declares its own license in its `LICENSE` file — check the repository you're
contributing to. By submitting a contribution, you agree it may be distributed under that
repository's license.
