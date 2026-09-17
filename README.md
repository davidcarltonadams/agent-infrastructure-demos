# Agent Infrastructure — Interactive Demos

Three self-contained, fully synthetic demos from a personal multi-agent system
designed, built, and operated daily by [David Carlton Adams](https://davidcarltonadams.com).

**All data here is fictional.** Projects, people, feeds, and findings belong to
an invented world; the architecture, rendering, and interaction patterns are
the real system's.

## Demos

Live via GitHub Pages:

- **[Flightpath](./atlas-demo.html)** — a one-true-state project layer: every
  project a card, every milestone a bar, dependency chips, collapse at every
  level. Also shown: a derived **heat index** (hot/waiting/decision-needed/
  chill — badges here, in production just an accent color on the status
  dot), explicit **rank overrides** for pulling a project above its heat
  sort, and an **estimate ledger** per project (when the estimate was made,
  by whom, sessions/wall-days, scope) — the calibration record that keeps
  future estimates honest. The real Flightpath is written to by exactly one
  validating CLI, and every mutation carries a logged one-line reason — the
  audit trail is what keeps "canonical" honest.
- **[The Gazette](./gazette-demo.html)** — a daily personal newspaper
  assembled overnight from monitored feeds: classifieds ranked by fit,
  a puzzle corner, term-of-day, a graded daily course lesson, and a Docket
  digest — open/discuss/decided/applied decision cards surfaced into the
  paper so nothing sits unresolved past standup.
- **[Gander](./horizons-demo.html)** — a timeline + what-if sandbox over the
  same state layer Flightpath renders. Schedules are *derived* (dependency order +
  effort estimates, backward-packed from deadlines) where no explicit dates
  exist; drag any bar and downstream derived dates cascade live. The sandbox
  is client-side only by design — "copy scenario" exports a proposal for the
  validating CLI to apply later, so playing with the plan can never mutate
  canonical state (decision ≠ execution). One rendering engine serves both
  this public synthetic demo (JS inlined, self-contained) and the private
  authed surface (JS served separately to satisfy a strict CSP).

All files are single self-contained HTML documents — no external requests,
no trackers, nothing loaded from anywhere.

## The architecture behind them

The production system these demos mirror runs as several agents with
different jobs and different trust levels:

- An **internet-facing agent** scrapes for relevant material and writes
  reports it never acts on, always paraphrasing (no verbatim pass-through, to
  blunt prompt-injection).
- A **trusted core** reads those reports as untrusted data — never executing,
  never quoting directly, never writing back — and combines them with local
  state to produce daily briefings and the Gazette.
- Boundaries are enforced by design: untrusted-input quarantine, fail-closed
  authentication, localhost-only services fronted over a private overlay
  network (nothing public-facing), and a rotating integrity-audit schedule
  over the ingestion lanes.

Built with Claude Code, hardened iteratively, and in daily use.

---
Last updated: 2026-08-17 — refreshed with richer synthetic data (heat, rank,
estimate ledgers, a Docket digest) to track what the real system does today.
All content remains fictional; see the security-review checklist on the PR
that introduced this refresh.
