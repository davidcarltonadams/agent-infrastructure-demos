# Agent Infrastructure — Interactive Demos

Four self-contained, fully synthetic pages from a personal multi-agent system
designed, built, and operated daily by [David Carlton Adams](https://davidcarltonadams.com).

**All data here is fictional.** Projects, people, feeds, messages and findings
belong to an invented world; the architecture, the gates, the formats and the
interaction patterns are the real system's.

## Demos

Live via GitHub Pages. Trace is the shortest way in; each page stands alone.

- **[Trace](./trace-demo.html)** — one forwarded email followed through one
  day: fourteen stops on the day's real schedule, nine of them on the item's
  path. Each stop names what runs (a cron job, a launchd timer, a session with
  the person present), what it reads, what it writes, and what gate stands in
  front of it; each opens to show what that surface actually displayed, in its
  own format. The page ends with what the system did not do, by design. Play
  the day or tap a stop.
- **[Flightpath](./atlas-demo.html)** — a one-true-state project layer: every
  project a card, every milestone a bar, dependency chips, collapse at every
  level. The real Flightpath is written to by exactly one validating CLI, and
  every mutation carries a logged one-line reason. Also shown: the stale strip
  (line 4 of the seven-line brief, seven signals computed from each project's
  own log), due types (external, internal, soft, nudge), a derived **heat
  index**, explicit **rank overrides**, and the **estimate ledger** with its
  calibration factor, graded against actuals.
- **[The Gazette](./gazette-demo.html)** — a daily personal newspaper
  assembled overnight from monitored feeds: classifieds ranked by fit, a
  puzzle corner, term-of-day, a graded daily course lesson, and a Docket
  digest, so nothing sits unresolved past standup. The editor that writes it
  runs with every tool denied.
- **[Gander](./horizons-demo.html)** — a timeline and what-if sandbox over the
  same state layer. Schedules are derived (dependency order, effort estimates
  and the estimate error factor, backward-packed from deadlines) where no
  explicit dates exist; drag any bar and downstream derived dates cascade live.
  "Copy scenario" exports a proposal for the validating CLI to apply later;
  playing with the plan can never mutate canonical state. One rendering engine
  serves this public synthetic page and the private authed surface.

All files are single self-contained HTML documents: no external requests, no
trackers, nothing loaded from anywhere.

## What the pages have in common

The production system these demos mirror has run daily since March 2026. Its
shape:

- **One canonical state layer, one writer.** Project state lives in one place
  and is written by one validating command-line tool. Every mutation is an
  event in an append-only log with the reason that went with it, and the whole
  day is replayable from that log and from git. Four read-only surfaces (the
  board, the timeline, the seven-line brief, the dependency graph) are
  re-rendered from the state file on every change, so they cannot disagree.
- **Untrusted input never becomes an instruction.** Email forwards, scraped
  feeds and a partner system's handback are copied to quarantine files that no
  surface renders. A model call with no tools reads only the quarantine file
  and can emit JSON text and nothing else; plain code re-words that into an
  inert card in a decision queue. The card's options come from a fixed list,
  the model's suggestions print as text, and approval is a person's own turn.
  A forged message becomes, at worst, a strange card at the next standup.
- **Anything without an undo waits for a person.** Outbound mail, shared
  calendars, invites and merges are the person's click. Three standing
  exceptions write to calendars only he reads, idempotently, never deleting.
  Reversible writes are made and logged, and the log is what gets checked:
  gate the irreversible, log the reversible.
- **Detectors run on timers and only report.** A heartbeat that pages on
  change rather than on state (sixty-six replayed pages became six). A repo
  patrol strip: dirty, unpushed, held, a live checkout behind its upstream, a
  feed gone quiet. A noon reader that nudges only when a date is about to pass
  unlogged. A staleness scan that checks each project's plan against its own
  log and prints the worst two reasons.
- **Code goes through pull requests.** Builders work in their own worktrees
  and stop at the PR body; the assistant opens, the person merges. A second
  model family reviews the trust-boundary changes, and the holes it finds
  become hook-enforced rules rather than guidelines.
- **Four classification tiers.** These demos are the public tier. Scoped
  exports are built by adding allowed fields, never by redacting, so a field
  that was not cleared is simply absent.

Built with Claude Code, hardened iteratively, and in daily use.

## Refresh log

- **2026-10-02** — Trace added. Flightpath fixture re-dated to a 2026-10-02
  snapshot, with the stale strip, due types and the calibration line. Landing
  page names each page's mechanism and carries the provenance and tier notes.
- **2026-09-17** — reader-visible rename (Atlas → Flightpath, Horizons →
  Gander), landing page restyled to match the demos, a dead header link fixed.
- **2026-08-17** — richer synthetic data: heat, rank, estimate ledgers, a
  Docket digest.
