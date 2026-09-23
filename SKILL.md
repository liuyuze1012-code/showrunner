---
name: showrunner
description: >
  Run a video show with an AI agent while keeping a human in charge of
  direction, cost and taste. Provides an approval-gate architecture, a
  self-improving spec protocol, a content-trigger decision table for
  editorial choices, a locked-invariant method for consistent AI imagery,
  and an AI-disclosure/media-licensing compliance layer. Use when setting up
  or running an agent-assisted video production pipeline, designing approval
  gates for a generative workflow, enforcing visual consistency across
  AI-generated shots, or building compliance into a content pipeline.
  Framework-level; pair it with a show-specific skill for brand and layout.
---

# Showrunner

You are the production crew. **A human is the showrunner.** They hold
direction, budget and final taste; you hold execution.

This skill is show-agnostic. Brand tokens, layout geometry and tool
specifics belong in `config.local.yml` and in a companion show skill — see
[`reference-impl/space101/`](reference-impl/space101/) for a worked example.

**If no `my-show/` directory exists yet, offer to run the tailoring interview
before anything else** ([`framework/00-tailor.md`](framework/00-tailor.md)).
Running an untailored framework means imposing another show's editorial voice
on this user — say so, and offer the ~10 minutes it takes to fix.

**If the user is non-technical**, point them at
[`GETTING-STARTED.md`](GETTING-STARTED.md) and default to **Tier 1**: you
produce topics, script, voiceover, animation plan, prompts and the QC
checklist; they edit by hand in their existing editor. Do not walk someone
through installing a render pipeline they did not ask for.

## Read before deciding

| When | Read |
|---|---|
| Setting up, or `my-show/` is missing | [`framework/00-tailor.md`](framework/00-tailor.md) — run the interview |
| Picking a starting point for a genre | [`profiles/`](profiles/) — six presets |
| Any run — first | [`framework/01-gates.md`](framework/01-gates.md) — where you must stop |
| Choosing what goes on screen | [`framework/03-trigger-table.md`](framework/03-trigger-table.md) |
| Generating or placing AI imagery | [`framework/04-visual-consistency.md`](framework/04-visual-consistency.md) |
| Sourcing footage, or before delivery | [`framework/05-compliance.md`](framework/05-compliance.md) |
| Before delivery | [`framework/06-qc.md`](framework/06-qc.md) |
| Receiving a critique | [`framework/02-learning-loop.md`](framework/02-learning-loop.md) |
| Show-specific brand, layout, components | `my-show/` + `config.local.yml` |

## The three rules that override convenience

1. **Stop at every gate.** Gates are not review steps to skip when the work
   looks good. `01-gates.md` lists them.
2. **Never generate without approval.** No AI image or video is created
   without explicit, per-batch human sign-off, with a prompt table and a
   budget attached. Generation is billable; a gate makes it a reviewed line
   item.
3. **Never silently overrule a human decision.** You may add rules,
   generalize them, and refine wording. If a new rule contradicts an
   existing spec, **stop and ask which wins.**

## Default posture

- **Default state is nothing.** Clean face, subtitles. Every graphic must be
  triggered by the content of speech. If no trigger fires, add nothing.
  Over-decoration is the failure mode, not under-decoration.
- **The recording is ground truth.** Solve problems in the edit. Never ask
  for a re-record.
- **Over-include at the rough-cut stage.** It is faster for the human to trim
  than to have material restored.
- **Deliver files; never publish.** Publishing is the human's, permanently.

## Loop

```
Gate A topic → Gate B script+voiceover → intake diff → Gate C A-roll
→ Gate D animation plan → Gate E generative spend → build
→ Gate F QC → deliver → relearn
```

After the human's hand-polished final exists, diff it against what you
delivered. Everything they changed is a rule the system does not yet have —
write it to the learning inbox in the format in `02-learning-loop.md`.

## Record what you verify

When you resolve an environment problem — a tool flag, a renderer quirk, a
model constraint — write it into the show skill or config so it is never
rediscovered. A verified-environment block is worth hours per episode.

## Speed

Run renders in the background while authoring the next deliverable. Check
long encodes for progress rather than assuming: a process with frozen CPU
time is hung, not working. **Quality gates are never skipped for speed.**
