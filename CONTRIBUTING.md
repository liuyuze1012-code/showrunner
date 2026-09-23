# Contributing

Showrunner is a process framework extracted from a working show. The most
useful contributions are patterns that survived contact with production —
not ideas that should work.

## What fits

- **Gate designs.** New gates, or arguments that one here is wrong. Include
  what failed without it.
- **Compliance rules for other jurisdictions.** The current layer is
  China-platform-weighted. EU AI Act labeling, US FTC disclosure and
  platform-specific requirements would all extend it usefully.
- **Trigger tables from other editorial voices.** A documentary table, a news
  table and a comedy table would show which rows are universal and which are
  house style.
- **Visual-consistency recipes.** Other locked-invariant prompt templates,
  and which invariants matter most for a given model.
- **QC automation.** Scripts for anything currently checked by eye.

## What doesn't

- Model or tool recommendations that will be stale in six months. Name a
  constraint (*"batch concurrency is usually capped"*), not a version number.
- Prompt collections without the surrounding process.
- Brand or layout specifics — those belong in your own show skill, not in
  `framework/`.

## House style

- **Every rule carries its reasoning.** A rule without a "why" can't be safely
  revised later, so it gets frozen forever or deleted carelessly. See
  [`framework/02-learning-loop.md`](framework/02-learning-loop.md).
- **Prefer the specific.** *"Three sample frames before committing an
  in-point"* beats *"check your footage."*
- **Say what broke.** Oddly specific rules are the valuable ones. Keep the
  incident.
- **English canonical.** Non-English strings stay verbatim where they are
  operationally load-bearing — prompt text, on-screen copy, font names, brand
  phrases — with a short gloss. Please don't add parallel translated files;
  they drift.

## Reference material

`reference-impl/` documents one show as a worked example. Additional reference
implementations are welcome as new directories. Please don't edit the existing
one except to fix errors — it is a record of what was actually done.

## Process

Open an issue before a large change. For a rule or pattern, a pull request
with the rule, the reasoning, and the incident behind it is enough.

By contributing you agree your work is licensed under the [MIT License](LICENSE).
