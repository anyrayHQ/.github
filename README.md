# `.github`

This is the **organization-level community health repository** for
[Anyray](https://github.com/anyrayHQ). The files here serve two purposes:

1. **Organization profile** — [`profile/README.md`](./profile/README.md) is rendered at the top
   of [github.com/anyrayHQ](https://github.com/anyrayHQ).
2. **Default community health files** — the templates and policies below apply to **every Anyray
   repository** that does not define its own. (A repo's own copy always wins.)

## What's in here

| Path | Applies to |
| --- | --- |
| [`profile/README.md`](./profile/README.md) | The org profile page on GitHub |
| [`CONTRIBUTING.md`](./CONTRIBUTING.md) | How to propose changes across Anyray repos |
| [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md) | Contributor Covenant — applies org-wide |
| [`SECURITY.md`](./SECURITY.md) | How to report a vulnerability |
| [`SUPPORT.md`](./SUPPORT.md) | Where to get help |
| [`.github/PULL_REQUEST_TEMPLATE.md`](./.github/PULL_REQUEST_TEMPLATE.md) | Default PR template |
| [`.github/ISSUE_TEMPLATE/`](./.github/ISSUE_TEMPLATE) | Default issue forms (bug · feature · docs) |

## Where the product lives

Anyray's code and product docs are **not** here:

- **Source** → [`anyrayHQ/monorepo`](https://github.com/anyrayHQ/monorepo) — gateway, optimizer,
  console, and the `anyray-connect` CLI.
- **Documentation** → [docs.anyray.ai](https://docs.anyray.ai).

> GitHub only reads default community health files from the **default branch** of a repo named
> exactly `.github`. Keep changes on `main`.
