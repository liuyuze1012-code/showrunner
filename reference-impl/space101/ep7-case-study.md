# Case study — EP7, "Orbital Data Centers"

The episode that validated the framework end to end.

| | |
|---|---|
| Topic | 太空数据中心 — orbital data centers |
| Runtime | 9 min 21 s |
| Master | 3840×2160 (4K UHD) · H.264 · AAC 48 kHz · 30 fps CFR · 2.8 GB |
| Skin | ③ Engineering blueprint |
| Deliverables | Music-free master + 3:4 and 4:3 cover variants |

---

## Editorial thesis

The episode separates two claims that promoters deliberately blur:

> **Whether the engineering is possible**, and **whether the grand narrative
> built on top of it is logically coherent.**

It grants the genuine engineering achievement first, then walks the hidden
premises of the pitch one layer at a time — the thermal crux being that
vacuum has no atmosphere, therefore no convective cooling, therefore the heat
rejection problem that the pitch quietly omits. It closes on a factual
comparison: promotional beats rendered in pitch-deck grammar, shipped-capability
beats in blueprint grammar.

**Register:** *engineering versus narrative.* Attack the logic chain, never
the person. Concede real achievements before dismantling the story. End
genuinely open — *"nobody can settle this today; but the vision shouldn't be
assumed correct by default."* Stated positions, not rhetorical questions; a
single mirror question at the very end, offering two concrete options.

## Structural method — the "slide" technique

Every sentence carries one job: **make the viewer want the next sentence.**
Each line leaves an information gap that the next line fills while opening a
new one. Question → answer → new question.

Written in two passes:

1. Write the complete answer out in full.
2. **Re-order it** into a question-answer chain, so each node produces the
   next question on its own.

Information is sequenced along the *viewer's* path of reasoning, not the
author's knowledge tree. The constraint: suspense must never be cheap — every
step delivers real value, or it is manipulation and the audience feels it.

Self-check: any sentence that delivers its information completely, leaving no
gap, gets rewritten.

## Scoped rule override

The format spec bans comparative national framing. The director overrode it
for this episode, and the override was **recorded rather than quietly
executed** — with guardrails (anchor to facts, timelines and budgets; aim
criticism at pitch decks, never at a country or individual; honestly disclose
that both sides hold long-horizon visions, the real difference being timeline
honesty) and an explicit note that **the spec is not to be edited** until the
performance data comes in.

This is the escalation rule from
[`02-learning-loop.md`](../../framework/02-learning-loop.md#deliberate-overrides)
working as designed: the agent executed the exception without being able to
promote it into policy.

---

## The locked diorama recipe

The approved AI B-roll style. **Only `[SUBJECT]` and `[RED OBJECT]` change.
Every other word is copied verbatim.**

```
[SUBJECT: a hero object performing an action]. Miniature papercraft diorama,
matte low-poly painted-cardboard museum model, desaturated warm grey-beige
palette, everything greyscale EXCEPT one single red accent which is
[RED OBJECT: e.g. a red arrow / a red ring / a red block]. Blurred grey
factory-workshop skyline in the background. Soft even studio lighting, subtle
vignette, retro print-grain texture. Slight low camera angle, three-quarter
view, hero object centered, horizontal 16:9 widescreen.
```

**Invariant across the whole set:** palette, the single red, the blurred
factory background, soft lighting, grain, low angle. Only the hero object
changes. One or two recurring motifs glue the set together, and the moving red
is the eye anchor across hard cuts — **no dissolves.** Each shot 2–3s, one
concept, strictly following its sentence.

### Pipeline
1. `submit_image` — gpt-image-2.5-flare, **16:9**, high quality.
2. Poll for the output asset. Generated images are **cloud** assets and
   therefore support per-instance property overrides; locally-pushed images do
   not (no remote URL) — a constraint that shapes the whole asset strategy.
3. Wrap in a Ken Burns motion graphic: image property, `objectFit: cover`,
   scale 1.0 → 1.05, pan direction, and the **「AI·示意」** *(AI illustration)*
   disclosure chip.
4. Place on the muted B-roll track, in empty passages only. Hard cuts, ~2s.

### Animating the red
`submit_video` — seedance-2-5, first frame = the approved still, 4s, 720p, 16:9:

```
extremely subtle motion, slow gentle push-in, the red [...] animates
(rises / orbits / sweeps / pulses), everything else holds still, locked-off
```

Concurrency ≤3, so batch. Clips are fixed at 4s; longer slots are filled by
slowing playback rather than generating longer.

### First validated sequence
Frames 1920–2210, the physics crux (*no weather → no way to shed heat*), four
shots: sunlight ring → vacuum dot → thermometer → overheating lava cracks.

---

## What broke — technical gotchas

Recorded because each one cost real time.

**Renderer blanking.** Stacked `drop-shadow`/`blur` filter chains plus a very
large world plus many images plus matted cutouts **blanks the front-end
renderer** through cumulative compositing. The roundup component had to ship
as v9 (portrait badges) rather than v13 (full-body cutouts) — v13 renders
black. *Avoid filter chains; a single blurred background is fine.*

**Video inside a motion graphic renders black.** A `<Video>` element nested in
a motion graphic blanks on the front end. Generated clips go **directly onto
the timeline** — which means they lose the wrapper that carries their AI
disclosure chip, so the chip must be re-layered or covered by a global
fallback.

**Local images can't take property overrides.** No remote URL. Consequence:
per-speaker quote cards are baked as one dedicated component per person
rather than one generic component driven by an image property.

**Motion-graphic validator constraints.** Properties must be read as
`props.X`, not via aliases. Every declared property and every imported color
variable must actually be used. `interpolate` output ranges must be literal
arrays — no `.map()`.

**Aspect ratio.** Confirm the finished video's aspect *before* generating.
A batch generated 9:16 for a 16:9 episode is a total loss.

**Preview thumbnails don't render AI effects.** Acceptance requires a real
local export and frame extraction, never the preview.

**Verify in-points.** Three sample frames before committing an in-point on any
video asset. Black fade-ins, color bars, slates, camera-label cards and
blooper footage have all shipped into rough cuts.

## Sourcing and licensing

- Stock footage pages sat behind Cloudflare, so `curl` on the page HTML
  failed. The agent drove a real browser to reach the direct asset URLs, then
  fetched those.
- 🟢 Pexels, Pixabay, NASA — commercial use, no attribution required.
- 🔴 **SpaceX Flickr is CC BY-NC** — red tier for a monetized channel.
- 🟡 Speaker portraits from Wikimedia under **CC-BY**, matted with `rembg`
  (`u2net_human_seg`); attribution goes in the published description.
- Proper nouns get dedicated footage (a named rocket, a named station). Free
  footage is scarce for some companies — plan around it rather than
  substituting something generic.

---

## Retrospective

**What worked.** The locked diorama recipe delivered genuine set coherence —
the reason to copy the pattern rather than the specific style. Sidebar cards
became the house move: the presenter stays present while information builds
beside them, which suits an evidence-led show far better than full-screen
takeovers. The two-grammar system made the central argument legible before the
words landed.

**What to change.** **This episode used too much generated imagery.** It was
accepted to validate the style, but the standing priority is now explicit:

```
cards + real footage  >  AI stills (+ camera move)  >  AI video
```

Generated diorama shots are **seasoning — atmosphere, punctuation, and the
shots that genuinely cannot be filmed.** They are not the backbone. A show
whose credibility rests on verifiable evidence should not be built primarily
from synthetic images; that trades away the exact thing that makes it worth
watching.

The generation gate held throughout — nothing was generated without an
approved prompt table and budget, and every asset was reviewed before it
touched the timeline. The gate worked. The editorial judgment about *how much
to ask for* is the part that needed correcting, which is precisely the kind of
rule the learning loop exists to capture.
