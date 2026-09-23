# 04 — Visual consistency: making AI imagery look like one show

> AI B-roll usually looks cheap for one reason: every shot drifts. Lock the
> invariants, vary exactly one slot.

Generated imagery is easy to produce and hard to make *cohere*. A set of
individually impressive shots that don't share a world reads worse than
simpler footage that does. This is a set-design problem, not a prompt-quality
problem.

---

## The locked-invariant pattern

Write **one** prompt template for the whole show. Freeze every element that
defines the look. Leave one or two variable slots for what the shot is
actually about.

```
[SUBJECT: a hero object performing an action].
<style>. <material>. <palette — desaturated, one named accent only>,
everything greyscale EXCEPT one single accent which is [ACCENT_OBJECT].
<background — always the same>. <lighting — always the same>,
<grain / texture>. <camera angle — always the same>, hero object centered,
<aspect ratio>.
```

Only `[SUBJECT]` and `[ACCENT_OBJECT]` change between shots. **Every other
word is copied verbatim, every time.** Not paraphrased. Copied.

### The invariants, and why each one is load-bearing

| Locked | Breaks if varied |
|---|---|
| **Palette** | The single strongest cue that two shots are the same world |
| **Background** | A changing background reads as a changing location |
| **Lighting** | Direction and softness shifts are read as different scenes |
| **Grain / texture** | Ties shots to one medium; without it they look like different render engines |
| **Camera angle** | Consistent angle implies a consistent observer |
| **Aspect ratio** | Confirm against the finished video before generating — a wrong-aspect batch is a total loss |

### The single accent

One saturated accent in an otherwise desaturated frame does three jobs at
once:

1. **Eye anchor across hard cuts.** The viewer's eye tracks the accent from
   shot to shot instead of re-scanning each frame. This is what makes rapid
   cutting readable without dissolves.
2. **Set glue.** A recurring color is the cheapest possible continuity.
3. **Brand carry.** Use the show's accent color and the B-roll reinforces the
   brand for free.

Move the accent's *position* between shots. A stationary accent is decoration;
a traveling one is a through-line.

### Recurring motifs
Beyond the accent, let one or two hero objects recur across the set. A viewer
who sees the same object in shots 1, 4 and 9 reads the set as a narrative
rather than a slideshow.

---

## Shot discipline

- **One concept per shot.** The image illustrates the *sentence*, strictly.
- **2–3 seconds each.** Generated stills do not survive long holds.
- **Hard cuts, no dissolves.** The accent does the continuity work; a dissolve
  blurs the one element carrying it.
- **Never reuse a shot** — including a frame grab from a generated clip.
- **Always moving.** A generated still gets a slow push (≈100% → 105%) or a
  diagonal drift. Static generated stills look like stock images.

---

## Stills versus video

Default to **stills plus a camera move.** Image-to-video should be reserved
for shots that genuinely earn motion.

| | Generated still + move | Generated video |
|---|---|---|
| Cost | Low | High, and retries are expensive |
| Consistency | Controllable | Drifts more |
| Duration | Any (the move sets it) | Fixed by the model |
| Best for | Most of the set | A handful of hero shots |

When you do go to video: keep the subject nearly still and animate only one
thing — usually the accent — with an otherwise locked-off camera. Subjects in
motion is where generative video visibly fails.

```
extremely subtle motion, slow gentle push-in, the <accent> <rises / orbits /
sweeps / pulses>, everything else holds still, locked-off camera
```

Practical limits worth planning around: batch concurrency is usually capped
(3 is a common ceiling); clip length is fixed by the model, so a longer
timeline slot is filled by slowing playback rather than by generating longer.

---

## Two modes of generated imagery

Separate them by *job*, and know which one you're requesting:

**Evidence mode** — miniatures, dioramas, cutaways, physical-object
metaphors. Makes an abstract claim feel like a thing you could touch. Best for
data, mechanisms, and scale.

**Concept mode** — semi-photorealistic imagery for what cannot be filmed:
abstract metaphor, hypothetical futures, invisible processes, historical
reenactment.

The dividing line that matters:

> **Real footage covers what can be filmed. Generated imagery covers what
> cannot.**

If footage of the actual thing exists, use the footage. A show whose
credibility rests on verifiable evidence should not illustrate real,
filmable events with synthetic images — it trades away the exact thing that
makes it worth watching.

---

## The skin system

A related consistency problem: how do you vary the look between episodes
without diluting the brand?

Split the visual system in two:

**Constant brand layer** — never changes:
- background family, single accent color, font set, motion language

**Card surface ("skin")** — pick **one per episode**, never mix within one:

| Skin | Surface | Use for |
|---|---|---|
| Cold lab white | light | data-dense episodes |
| Deep console | dark | immersive narrative |
| Engineering blueprint | dark + line-work | mechanism teardowns, flagship episodes |

Episodes stay visually distinct, the channel stays recognizable, and skin
choice becomes an editorial decision — you are choosing how this episode
*argues*, not just how it looks.

### Grammar as argument
The strongest use of this is assigning *opposing visual grammars to opposing
arguments* within one episode. In the reference implementation, one episode
contrasted promotional claims against shipped reality by giving each its own
visual language — pitch-deck grammar (spotlight beams, glowing numerals,
scanlines) for the claims; blueprint grammar (grid, dashed planning panels,
seals, rulers, measured alignment) for the reality.

The viewer feels the argument before parsing it. Both grammars still sit
inside one brand — same accent, same fonts, same motion language — so it reads
as one show making a point, not two shows spliced together.

---

## The card motion rule

Cards are not slides.

> Every card introduces **new** motion — a new line, image, number or reveal —
> at least every **3–5 seconds**, timed to transcript anchors. Trim each card
> to end **0.5–1s after its final beat**.
>
> **If a passage cannot earn new motion, show no card at all.** Stay on the
> presenter.

That last clause is the one that gets skipped, and it is the one that keeps
quality up. A card forced in to fill a gap is always worse than the presenter's
face. Never let layout pressure produce a bad card.

### Card sizing: two options, no middle
1. **Large or information-dense → full screen.** Cover the frame completely.
2. **Small graphic or single data point → fit it into empty space** beside or
   below the presenter, who stays the main subject.

The failure mode is the middle: a card covering most of the frame with a
sliver of face showing. Decide which of the two a card is before sizing it.
There is no third option.
