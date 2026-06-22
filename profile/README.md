# Anyray

**Anyray is a self-hosted, pre-model middleware that optimizes coding-agent costs and
performance.** Anyray excels at engineering tasks, compressing and optimizing payloads without
degrading the output.

Your developers (Claude Code and other AI assistants), internal agents, and SDK apps generate LLM
cost across laptops and clusters. Anyray lets you see and attribute it (by team, app, model, and
provider) and cut it — **without asking anyone to change how they work**, and using **only cost
metadata, never prompt or response content**.

## Architecture

Anyray runs entirely on your own infrastructure as two services: a **gateway** that sits in
front of your LLM providers behind an OpenAI-compatible endpoint, and an **optimizer** the
gateway calls as a before-request hook. Four properties define how it behaves on the request
path:

- **Deterministic.** Optimizations are rule-based transforms — no extra model in the loop —
  and each is applied only when it stays within a measured quality bound.
- **Self-hosted.** Your prompt/response content never leaves your environment: traces and the
  spend store hold metadata only, content is encrypted at rest, and you can run with zero content
  retention. The only egress is the content-free usage rollup every deployment sends to Anyray for
  metering — never content.
- **Fail-safe.** The optimizer is a fail-open hook with a hard 800 ms timeout — on any error or
  timeout the gateway forwards the original request unchanged. A broken or slow optimizer can
  never break or alter inference.
- **Drop-in.** The gateway is OpenAI-compatible — point your SDK's base URL at it and nothing
  else in your app or workflow changes.

## Quick start

The whole system comes up from a single `docker compose up -d` against the compose file in the
install repo [`anyrayHQ/install`](https://github.com/anyrayHQ/install), from published images, in
**your** environment. Nothing is phoned home.

```bash
git clone anyrayHQ/install
./setup.sh
docker compose up -d
```

The gateway, console, optimizer, and Postgres (spend + traces) are running in your environment.
Redirect worker endpoints to the gateway base URL (`OPENAI_BASE_URL` / `ANTHROPIC_BASE_URL` → the
gateway on `:8787`). No app changes, no CA/TLS-MITM.

## How well does it work?

Reproducible, content-free measurements of the optimizer's input-token savings — on the
token-waste patterns developers and coding agents produce every day, run against your own
optimizer. Across 19 workloads it removes **~78% of input tokens** — suite-level reductions of
**49–86%**, no provider calls required. See [`anyrayHQ/benchmarks`](https://github.com/anyrayHQ/benchmarks).

## The mental model in one line

You `docker compose up` the stack in your environment, redirect traffic to the Anyray gateway, and
the optimizer makes each request cheaper while failing open — with your data never leaving.

## Explore

| | |
| --- | --- |
| 📚 **Documentation** | [docs.anyray.ai](https://docs.anyray.ai) |
| 🧰 **Install repo** | [`anyrayHQ/install`](https://github.com/anyrayHQ/install) — Docker Compose, cloud templates, and gateway adapters |
| 🔐 **Security & data boundary** | [Security](https://docs.anyray.ai/operate/security) · [Data boundary](https://docs.anyray.ai/operate/data-boundary) |

---

<sub>Found a security issue? See our [security policy](https://github.com/anyrayHQ/.github/blob/main/SECURITY.md). Everything else: [open an issue](https://github.com/anyrayHQ/install/issues) or read the [contributing guide](https://github.com/anyrayHQ/.github/blob/main/CONTRIBUTING.md).</sub>
