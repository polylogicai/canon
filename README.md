# Polylogic AI · canonical/

This is the canonical source of truth for **Polylogic AI**: master spec, system architecture, worker definitions, watchdog definitions, marketplace Polybrain configurations, funnel registry, provider registry, audit canon, and integrity chain.

Every Polylogic AI public surface (the website at polylogicai.com, the polycode CLI, the Telegram bridge, the orchestrator daemon, every worker in the fleet, every marketplace Polybrain) reads from this repo at runtime or build time. If a descendant artifact disagrees with this repo, the descendant is wrong.

## Why this repo exists

A canonical source of truth must be **structurally external** to anything that reads it. Per the kernel paper's central insight — *substrate cannot witness itself* — the master spec for Polylogic AI cannot live inside the website that the spec describes, and it cannot live inside the orchestrator daemon that the spec governs. It lives in its own repo, on its own GitHub home, with its own git history, with its own integrity chain, with its own public visibility.

Multiple consumers all read from this single source:

- **The polylogicai.com website** clones this repo at Vercel build time
- **The orchestrator daemon on the VM** clones this repo at boot and pulls on changes
- **The polycode CLI** clones this repo on first run
- **Every worker in the fleet** reads its own `canonical/workers/{name}.md` file
- **Every watchdog in the tier** reads its own `canonical/watchdogs/{name}.md` file
- **The Onboarding Polybrain** reads `canonical/providers.yaml` to know how to walk users through any third-party API key acquisition
- **The funnel watchdog** reads `canonical/funnels.yaml` and cross-checks every page's `data-funnel` attribute against it

## Layout

```
canonical/
├── master-spec.md              ← the L0 source of truth, Andy-signed
├── system-architecture.md      ← the orchestrator's self-awareness file
├── workers/                    ← 42 worker .md files (markdown + YAML frontmatter)
├── watchdogs/                  ← 16 watchdog .md files
├── marketplace/                ← marketplace Polybrain config profiles
├── funnels.yaml                ← funnel registry (every public surface declared here)
├── providers.yaml              ← provider registry (Onboarding Polybrain reads at runtime)
├── canon/                      ← append-only JSONL canon files
│   ├── orchestrator.jsonl
│   ├── workers/{name}.jsonl
│   ├── watchdogs/{name}.jsonl
│   └── users/{user_id}/{polybrain_id}.jsonl
├── cursors/                    ← per-watchdog cursor files (restart-safe positions)
├── checksums.txt               ← SHA-256 of every canonical file
├── checksums.txt.ots           ← OpenTimestamps Bitcoin anchor of checksums
└── i18n/                       ← future locale layers (empty at v1.0.0, en is implicit)

audiences/                      ← BUILT from canonical at compile time, never hand-edited
├── internal/INTERNAL.md
├── agent/AGENT_BOOT.yaml
└── onboarding/ONBOARDING.md

system/                         ← build + verification scripts
├── build.mjs                   ← compiles audiences from canonical
├── verify.mjs                  ← doc-consistency check
├── enforce.mjs                 ← watchdog enforcement scan
├── live-data-refresh.mjs       ← refresh stale facts
├── spec-vs-code.mjs            ← drift check between spec and downstream code
└── checksum.mjs                ← hash + OpenTimestamps anchor

.github/workflows/
├── heartbeat.yml               ← every 5min, curls VM /heartbeat, alerts Telegram on failure, updates status.json
├── verify.yml                  ← on push, runs system/verify.mjs to catch drift
└── checksum.yml                ← daily, runs system/checksum.mjs to anchor the integrity chain
```

## Status page

`status.polylogicai.com` is served from this repo via GitHub Pages. The heartbeat workflow updates `docs/status.json` every 5 minutes with the latest tier health snapshot. Anyone can glance from any browser, anytime, without login.

## License

The contents of this repo are released under **CC BY 4.0**. Same license as the Polybrain paper at doi.org/10.5281/zenodo.19571656. The polybrain-kernel is MIT.

## Authority

This repo is authored by **Andrew Salvo** (founder of Polylogic AI, undergraduate at the Smeal College of Business at Penn State University, ajs10845@psu.edu). Every change to the master spec or the system architecture file requires Andy's signature in a canon row of type `master_spec_change`. The orchestrator and the entire workforce read this repo at boot.

## Hero line

> **Own your AI.**

## Subhead

> Polybrain is an AI agent that shows its work.

## Tagline

> YOUR MACHINE · YOUR TOOLS · YOUR LIFE
