# 01 — Gates: the approval architecture

> The agent does the labor. The human keeps direction, cost, and taste.

A gate is a point where the agent **stops and cannot proceed** until a human
decides. Gates are not review steps that can be skipped when the work looks
good. They are the structural reason an agent can be trusted with an
expensive, public, hard-to-undo artifact.

Everything between gates is the agent's to do without asking.

---

## The pipeline

```
Gate A  topic
   │
Gate B  script  ──────────────┐
   │                          │  deliver TWO files:
   │                          │  · script (structure, emotion beats, fact table)
   │                          │  · voiceover (clean read-ready lines ONLY)
   ▼
[intake]  transcribe the recording, diff against the approved script,
          report every deviation BEFORE cutting
   │
Gate C  A-roll    pure cut. no graphics, no music, no subtitles
   │
Gate D  animation plan   per timestamp: trigger fired → treatment → media
   │
Gate E  generative spend  ★ the cost gate — see below
   │
[build]   production
   │
Gate F  QC        the checklist in framework/06-qc.md
   │
[ship]    deliver files. the agent never publishes.
   │
[relearn] diff the human's hand-polished final against what was delivered;
          extract what they changed; write it to the learning inbox
```

---

## Gate A — Topic

Who proposes depends on the format:

- **Solo / original formats:** the agent proposes a *menu* of topics against
  a stated selection rubric. The human picks or edits.
- **Interview / commissioned formats:** the topic is the human's. The agent
  does not counter-propose unless asked.

Either way the human's choice is final and is not relitigated downstream.

## Gate B — Script

Two deliverables, always separated:

| File | Contents |
|---|---|
| `SCRIPT.md` | Full structure, emotional beat markers, fact-check appendix with a source per claim |
| `VOICEOVER.md` | **Only the lines to be read aloud**, in order, labeled with which clip they sit before or after |

Splitting these is not cosmetic. A presenter reading from a document full of
production notes performs worse than one reading clean lines. The voiceover
file is a script for a human voice, not a document.

**Duration rule:** a stated target duration is a **floor**, not a target. Aim
5–10% over. Cutting is cheap; discovering you are three minutes short after
the recording session is not.

## Intake — the diff step

Before a single cut is made:

1. Transcribe the delivered recording.
2. Diff it against the approved script.
3. Report every deviation.

**A dropped fact is a blocker.** A rephrasing is a note. The distinction
matters because the fact-check appendix from Gate B is void if the sentence
it defends never made it into the recording.

**The recording, as delivered, is ground truth.** The agent solves problems in
the edit, not by asking for a re-record. This is the correct constraint when
the scarce resource is the presenter's time and energy — and it forces better
editorial engineering. If a line is unusable, cut around it or write VO
coverage; do not send the human back to the microphone.

## Gate C — A-roll

A pure cut. No graphics, no music, no subtitles — nothing that disguises a
weak structure as a finished video.

**Over-include.** Keep whole conversational exchanges rather than tight
selects. It is far faster for the human to trim than to ask for material to
be restored from a cut the agent has already committed to. *Keep more, edit
less.*

If the human returns a re-cut A-roll, **that version becomes ground truth**
and the agent's cut is discarded without argument.

## Gate D — Animation plan

A table, approved before anything is rendered. One row per graphic:

| Timecode | Trigger that fired | Treatment | Media | Subtitle keywords |
|---|---|---|---|---|

This gate exists because rendering is the expensive, slow step. Catching *"that
beat doesn't need a card"* costs one line of review here and an hour of
re-render later. Approval should be fast — if the plan needs long discussion,
Gate B or C failed.

## Gate E — Generative spend ★

**The gate most teams don't build, and the one that matters most.**

Generative models produce assets faster than a human can review them and bill
for every attempt, including the bad ones. Without a gate, cost and visual
drift both compound silently.

The rule:

> **No AI image or video is generated without explicit, per-batch human
> approval.**

And the order is locked:

```
1. finish ALL real-footage B-roll
2. finish ALL animation and cards
3. identify what is still genuinely missing
4. submit a request: prompt table + shot count + budget
5. human approves the batch  ← the gate
6. generate
7. human reviews EVERY generated asset individually
8. only approved assets touch the timeline
```

Steps 1–3 are the point. Most "we need AI footage here" turns out to be
"we haven't finished looking for real footage." Forcing generation to the end
of the process collapses the volume requested, and what is requested is
better specified.

Unapproved output is never used and never quietly recycled into a later
episode.

**Why order the pipeline this way:** generation is typically the only *metered*
operation in an AI editing stack — cutting, motion graphics, effects and
export are usually free. Gating the one metered operation converts an
unbounded API bill into a reviewed line item, without slowing anything else
down.

### Budget the retry rate
Generation failure is normal, not exceptional. Budget **1.5–2× the shot count**
you intend to keep. A plan that assumes every generation succeeds is not a
plan.

### Media-mix priority
Generative output should be seasoning, not structure. Default priority:

```
cards + real footage  >  AI stills (+ camera move)  >  AI video
```

AI video is reserved for the handful of shots that genuinely earn it. A show
built primarily from generated footage inherits that medium's credibility
problem, which is expensive to buy back.

## Gate F — QC

See [`06-qc.md`](06-qc.md). Quality gates are never skipped for speed. Renders
can run in the background while the next deliverable is authored; the
checklist cannot be parallelized away.

## Ship and relearn

The agent **delivers files. It does not publish.** Publishing is an
irreversible, public, account-bearing action and stays with the human,
permanently — this is not a maturity threshold the agent graduates past.

After the human's hand-polished final exists, diff it against what was
delivered. Every change they made is a rule the system did not yet know.
Those go to the learning inbox — see [`02-learning-loop.md`](02-learning-loop.md).

---

## Designing your own gates

Three tests. A step deserves to be a gate when:

1. **Reversal is expensive.** Wrong topic wastes a week; wrong transition
   wastes a minute. Only the first is a gate.
2. **The agent cannot self-evaluate.** An agent can verify frame rate. It
   cannot verify that a joke lands or that a comparison is fair.
3. **It spends or publishes.** Money and public surface are always gates.

And the inverse — **do not** gate what the agent can check itself. Gates that
fire on things a checklist could catch train the human to approve without
reading, which silently disables the gates that matter.
