# Polylogic AI · public surface

This repo is the public surface of **Polylogic AI**. It carries the liveness signal for the orchestrator, served as a small status page via GitHub Pages.

## What lives here

```
.github/workflows/heartbeat.yml   GitHub Actions cron, every 5 minutes,
                                  curls the orchestrator's /heartbeat
                                  endpoint and updates docs/status.json.
                                  Posts a Telegram alert on missed pings.

docs/status.json                  Latest liveness snapshot. Updated on
                                  every successful heartbeat. Served by
                                  GitHub Pages.

docs/index.html                   The status page rendered at
                                  status.polylogicai.com (CNAME).
```

## What does NOT live here

The strategic source of truth for Polylogic AI — the master spec, the system architecture, the orchestrator runbook, the worker fleet definitions, the watchdog tier, the audit canon — is **not in this repo and not on GitHub**. Polylogic AI's verifier is the published research paper, the open kernel, and the deployed product. Those live in their own canonical homes:

- **The paper**: [`doi.org/10.5281/zenodo.19571656`](https://doi.org/10.5281/zenodo.19571656) — *Engine, Rules, and Canon* by Andrew Salvo, CC BY 4.0, Bitcoin-anchored.
- **The kernel**: [`github.com/polylogicai/polybrain-kernel`](https://github.com/polylogicai/polybrain-kernel) — MIT-licensed reference implementation.
- **The deployed product**: [`polylogicai.com`](https://polylogicai.com) — try Polybrain.

The witness rule that organizes Polylogic AI's architecture is satisfied by those three artifacts. Publishing the operational playbook would only give the same competitors who can read the paper a free roadmap to copy the company. So we don't. Each Bateson logical type lives in its own structurally separate container.

## Hero line

> **Own your AI.**

## Subhead

> Polybrain is an AI agent that shows its work.

## Tagline

> YOUR MACHINE · YOUR TOOLS · YOUR LIFE

## License

The contents of this repo are CC BY 4.0. The kernel referenced above is MIT. The paper is CC BY 4.0.
