# Showrunner

**An approval-gate architecture for running a video show with an AI agent.**

The agent does production. A human stays the showrunner — holding direction,
cost and taste.

[![License: MIT](https://img.shields.io/badge/License-MIT-000000.svg)](LICENSE)
![Status](https://img.shields.io/badge/status-in%20production-E05A2B)

---

## The problem

Generative models can now produce video assets faster than a human can review
them, and they bill for every attempt — including the failures. Put an agent
in charge of a real show and three things go wrong at once:

- **Cost drifts.** Nobody decided to spend it; it accumulated one batch at a time.
- **Look drifts.** Every generated shot is individually plausible and collectively incoherent.
- **Judgment drifts.** The agent decorates everything, because "make it engaging" has no stopping rule.

None of these are model-quality problems, so better prompts don't fix them.
They are **process** problems. Showrunner is the process.

## New here?

**→ [GETTING-STARTED.md](GETTING-STARTED.md)** — a step-by-step guide that assumes
no terminal, no coding, and no prior knowledge of AI agents. About 30 minutes
to your first script.

You do **not** need a technical pipeline to get value from this. See
[the two tiers](#two-ways-to-use-it).

## What it actually does

Concretely, across one video, the agent:

1. **Proposes topics** against a selection rubric, and stops for your pick
2. **Researches and writes the script**, with a fact table — one verified
   number per claim, each with its source
3. **Delivers a clean voiceover file** — only the lines to read aloud, nothing else
4. **Transcribes your recording and diffs it** against the approved script, so
   a dropped fact is caught before editing, not after
5. **Plans every graphic** as a table: *timecode → what triggered it → what
   appears → which media* — approved before anything renders
6. **Writes AI image prompts** from a locked template so the whole set looks
   like one show, with a cost estimate, and generates nothing until you say yes
7. **Tiers every piece of footage** by license and maintains a source manifest
   with the attribution strings you'll need
8. **Runs a QC checklist** — reading every on-screen number aloud, auditing
   every cut for face flashes, probing the master for sync drift
9. **Writes down what you corrected**, so it doesn't need correcting again

In [Tier 2](#two-ways-to-use-it) it also drives the editor and renders. In
Tier 1 it hands you all of the above and you edit by hand.

## Is this for you?

**Works well for:**

| | Why |
|---|---|
| **Explainers and video essays** | Built from one. Argument structure is the backbone |
| **News breakdowns and commentary** | Fast turnaround, heavy fact and attribution discipline |
| **Interview and podcast cutdowns** | Selection-driven; the gates map cleanly onto rough-cut passes |
| **Product reviews** | Criteria-locked, with disclosure as a blocking QC item |
| **Tutorials** | Step-numbered, exact-string accuracy, executable verification |
| **Documentary shorts** | Chapter structure and J-cut transitions |

Full presets for each: **[`profiles/`](profiles/)**.

The common thread: **scripted or semi-scripted, information-carrying, and
part of a series.** Content where being *right* matters, where there are
recurring visual decisions worth systematizing, and where the same mistakes
would otherwise recur every episode.

**Works poorly for:**

| | Why |
|---|---|
| Vlogs and lifestyle | Unscripted. There's no script to gate, and the appeal is spontaneity |
| Comedy sketch | Timing is performance, not content-triggered |
| Music videos, narrative fiction | Driven by the edit's rhythm, not by what's being said |
| Livestreams | No post-production stage to gate |
| **One-off videos** | The system pays back over a series. For a single video it's overhead |
| Personality-first content | If people watch for *you*, the systematized part isn't the bottleneck |

**The honest test:** if you're making your first video, this is too much
machinery. If you're making your tenth and keep re-deciding the same things —
or keep giving an AI the same correction — that's exactly what this fixes.

## Two ways to use it

| | **Tier 1 · Director mode** | **Tier 2 · Full pipeline** |
|---|---|---|
| Agent does | Topics, script, voiceover, animation plan, prompts, QC checklist | All of that, plus driving the editor and rendering |
| You do | Edit by hand in CapCut / Premiere / Resolve | Review and approve |
| Needs | **Just Claude Code** | Agent-drivable editor, ffmpeg with `libass`, ASR, headless Chrome |
| Setup | ~30 min | A few hours |

**Start at Tier 1.** Most of the value here is editorial judgment, and none of
it requires a pipeline.

## Tailor it to your show

The framework ships carrying one show's voice, which is almost certainly not
yours. Fix that in one command:

```
Use the showrunner skill and run the tailoring interview to set up my show.
```

The agent interviews you — what you make, who watches, what your show promises,
how much motion you want, what must never happen — then writes **your** config,
**your** trigger table, **your** format spec and **your** brand tokens into a
`my-show/` directory. All plain text, all editable, re-runnable whenever the
show changes.

Protocol: [`framework/00-tailor.md`](framework/00-tailor.md).

## The five patterns

Six specification documents an AI coding agent loads as operating
instructions. They encode five transferable patterns:

| | Pattern | Solves |
|---|---|---|
| **0** | [Tailoring](framework/00-tailor.md) | Fitting all of the below to *your* show, via an interview |
| **1** | [Approval gates](framework/01-gates.md) | Where the agent must stop — including a **hard gate on generative spend** |
| **2** | [Learning loop](framework/02-learning-loop.md) | Turning corrections into durable rules, without the agent overruling you |
| **3** | [Trigger table](framework/03-trigger-table.md) | Editorial judgment as an executable decision table, with a default of *nothing* |
| **4** | [Visual consistency](framework/04-visual-consistency.md) | Making a set of AI shots look like one show |
| **5** | [Compliance](framework/05-compliance.md) | AI disclosure, media licensing tiers, editorial risk |

Plus [QC](framework/06-qc.md): what a machine checks versus what a human must read aloud.

This is **not** a rendering tool, an NLE, or a model wrapper. It sits above
whatever stack you already use and decides when the human is in the loop.

## Architecture

```mermaid
flowchart TD
    A["Gate A · Topic"] --> B["Gate B · Script + Voiceover"]
    B --> I["Intake<br/><i>transcribe, diff vs script,<br/>report deviations</i>"]
    I --> C["Gate C · A-roll<br/><i>pure cut, no graphics</i>"]
    C --> D["Gate D · Animation plan<br/><i>trigger → treatment → media</i>"]
    D --> E["Gate E · Generative spend ★<br/><i>prompt table + budget</i>"]
    E --> P["Build"]
    P --> F["Gate F · QC"]
    F --> S["Deliver<br/><i>the agent never publishes</i>"]
    S --> R["Relearn<br/><i>diff the human's final</i>"]
    R -.->|new rules| B

    classDef gate fill:#12263E,stroke:#E05A2B,stroke-width:2px,color:#F5EFE8
    classDef auto fill:#1a1a1a,stroke:#555,color:#ccc
    class A,B,C,D,E,F gate
    class I,P,S,R auto
```

Dark boxes are gates: the agent **stops** and cannot proceed. Everything
between them is the agent's to do without asking.

## The gate that matters most

Most teams building agent workflows implement none of these. If you implement
exactly one, make it **Gate E**:

> No AI image or video is generated without explicit, per-batch human
> approval — and generation happens *last*, after all real footage and all
> animation are finished.

The ordering is the trick. Most "we need AI footage here" turns out to be "we
haven't finished looking for real footage yet." Forcing generation to the end
of the pipeline collapses the volume requested, and what remains is better
specified. Generation is usually the only *metered* step in an AI editing
stack — gating it converts an open-ended API bill into a reviewed line item
without slowing anything else down.

## The safety property

A self-modifying instruction set needs a constraint, or it will quietly
reverse decisions you made deliberately — each contradiction looks locally
reasonable when resolved in the moment.

> **The agent may learn. It may not silently overrule you.**
>
> It can add rules, generalize several into one, and refine wording. It
> **cannot** overturn a human decision, resolve a contradiction between specs
> on its own, or drop a rule as obsolete. Contradictions escalate — always.

Deliberate exceptions are recorded rather than quietly executed, scoped to one
episode, and carry an explicit prohibition on generalizing themselves. See
[`02-learning-loop.md`](framework/02-learning-loop.md).

## Quickstart (technical)

*Non-technical? Use [GETTING-STARTED.md](GETTING-STARTED.md) instead.*

```bash
git clone https://github.com/liuyuze1012-code/showrunner.git
cd showrunner
cp config.example.yml config.local.yml   # gitignored — your IDs stay local
```

Then:

1. **Install as an agent skill.** For Claude Code, symlink or copy into
   `~/.claude/skills/showrunner/`. Any agent that loads Markdown instructions
   works — `SKILL.md` is the entry point and routes to the rest.
2. **Run the tailoring interview** — it fills `config.local.yml` and generates
   your `my-show/` directory:
   ```
   Use the showrunner skill and run the tailoring interview to set up my show.
   ```
   Prefer to do it by hand? Pick a preset from [`profiles/`](profiles/), copy
   it into `my-show/trigger-table.md`, and edit `config.local.yml` directly.
3. **Decide your gates.** Defaults are in `config.local.yml`. Disabling one
   should be a deliberate act.
4. **Run one video and keep an inbox.** The first run generates the rules the
   framework can't know for you.

### Adapting the trigger table
The interview gives you a starting table. To improve it, don't write from
aspiration — go through work that got **rejected**. Each rejection is a trigger
you hadn't written down. Order rows by strength so the agent knows which wins
when two fire, and include the *do-nothing* rows explicitly, or silence never
gets chosen.

## Reference implementation

[`reference-impl/space101/`](reference-impl/space101/) documents
**太空101 (Space 101)** — a Chinese-language frontier-technology explainer
series — as a complete worked example: a three-skin brand system, a
ten-component motion-graphics library, a locked AI diorama recipe, and a
case-study breakdown of one shipped 4K episode.

Reference material is deliberately kept separate from `framework/`. The
framework is the part you reuse; the reference implementation is the part you
replace.

## Provenance

These patterns were extracted from a working production channel, not designed
in the abstract. The originating specification set went through **40 commits
over six weeks** and **~91 numbered production learnings**, one of which —
collapsing 56 individual corrections into a single 12-row decision table — is
the reason the trigger table exists in this form.

Where a rule looks oddly specific, it is because something broke. Those are
the valuable ones.

## Scope and limits

Worth being explicit about:

- **This is a process framework, not software.** There is nothing to execute.
  Its value is in what the agent reads before acting.
- **It assumes a capable coding agent** with filesystem and tool access.
- **The compliance layer is China-platform-weighted**, because that is where
  it was built and tested. The licensing tiers and disclosure logic generalize;
  the specific regulation cited does not.
- **Tool-agnostic by design, but not tool-free.** You need an editor an agent
  can drive, a rendering path, and ASR. Record verified values in config so
  they are never rediscovered.
- **Single-show, single-director.** Multi-stakeholder approval is not modeled.

## Contributing

Patterns that generalize are welcome — especially gate designs, compliance
rules for other jurisdictions, and trigger tables from different editorial
voices. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE) © 2026 Yuze (Gavin) Liu
