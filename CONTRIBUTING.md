# Contributing to Anyray

Thanks for taking the time to contribute. This is the **default** contributing guide for all
[Anyray](https://github.com/anyrayHQ) repositories; an individual repo may add its own
`CONTRIBUTING.md` with project-specific detail (the monorepo's `CLAUDE.md` / `AGENTS.md` carry the
authoritative per-package build and quality gates).

By participating, you agree to abide by our [Code of Conduct](./CODE_OF_CONDUCT.md).

## Where things live

- **Source:** [`anyrayHQ/monorepo`](https://github.com/anyrayHQ/monorepo) — gateway, optimizer,
  console, and the `anyray-connect` CLI, in one pnpm workspace.
- **Documentation:** [docs.anyray.ai](https://docs.anyray.ai) (source under `docs/` in the
  monorepo).

## Ground rules (product invariants)

Anyray sits on the path of every LLM request, so a few invariants are **non-negotiable**. A
change that breaks one of these is a correctness bug, not a trade-off:

1. **Content privacy.** Prompt/response *content* is never shown to humans in the clear and never
   logged as plaintext. It is encrypted at rest (AES-256-GCM). Logs, traces, and the spend store
   carry **metadata only** — user, team, model, provider, tokens, cost, latency, decision. If you
   add a log/trace/persist call, log metadata, not message bodies.
2. **Spend governance.** Every request stays attributable into the content-free spend store.
3. **Single admin key.** The console and every `/admin/*` API stay behind the one admin key.
4. **The gateway fails open.** The optimizer is a best-effort hook on the hot path — if it's slow
   or down, the gateway must forward the original request untouched. A broken optimizer can never
   break or alter inference.

When in doubt, open an issue before writing code that touches any of these.

## Reporting bugs & requesting features

Use the issue forms in the relevant repository:

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
3. **Follow the existing conventions.** ESM everywhere; camelCase filenames; Zod at boundaries;
   `try/catch` with `HTTPException` for gateway HTTP errors; Prettier formatting. Match the code
   around you.
4. **Extend via the existing seams.** New LLM provider → a new folder under
   `gateway/src/providers/`. New optimization → a new strategy registered in the optimizer
   `REGISTRY`. New tool for `anyray-connect` → a new adapter behind the `REGISTRY` seam. Don't
   special-case it in callers.
5. **Run the quality gate** for the package you changed (typecheck · lint · format · test — see
   `CLAUDE.md`/`AGENTS.md` in the monorepo). CI runs the same gates on every PR.
6. **Docs are part of the change.** If you altered a documented seam — provider/strategy ids, env
   vars or defaults, endpoints, CLI commands, billing/plan rules — update the corresponding page
   under `docs/docs/` in the **same PR**. A stale env var or id in the docs is a correctness bug.
7. **Add tests** for new behavior and bug fixes.

## Opening a pull request

- Keep PRs focused — one logical change per PR.
- Fill out the [pull request template](./.github/PULL_REQUEST_TEMPLATE.md).
- Write a clear description: what changed, why, and how you verified it.
- Make sure CI is green. Maintainers review from there.

## Commit messages

Write imperative, present-tense subjects (`add bedrock fallback`, not `added`/`adds`). Explain
the *why* in the body when it isn't obvious. Reference issues with `Fixes #123` where applicable.

## License

Anyray is MIT-licensed. Unless a repository states otherwise, contributions are accepted under
the [MIT License](https://github.com/anyrayHQ/monorepo/blob/main/gateway/LICENSE), and by
submitting a contribution you agree it may be distributed under those terms.
