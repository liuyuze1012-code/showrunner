# 太空101 — Component library

A **technique library, not a template set.** Each episode is designed fresh
for its content; these are the moves available when a beat calls for one.

---

## Ten standard animation components

Components 1–5 are authored as code-generated motion graphics. Components
6–10 use editor built-ins. **All are free** — only generation is metered.

| # | Component | Serves | Implementation |
|---|---|---|---|
| 1 | **Counting-roll card** | Number barrage | Large serif numerals rolling up, underline self-drawing. 3–5× per episode; highest-priority template |
| 2 | **True-proportion bars** | Number comparison | Bars grow to real proportion; the accent-colored bar lands last |
| 3 | **Promise timeline** | Slipped deadlines, evolving claims | Nodes light in sequence, lapsed items struck through, final cell in accent |
| 4 | **Orbital-transfer diagram** | Mechanism explanation | Single-coordinate SVG: orbital motion, self-drawing dashed arc, counter |
| 5 | **Quote typewriter** | Regulations, direct quotes | Character-by-character, underline sweep on the key phrase, risk words recolored |
| 6 | **Magnifier focus** | Reading a document | Built-in magnifier over a document screenshot |
| 7 | **Mosaic reveal** | The reveal beat | Built-in mosaic: obscured, then uncovered on the word |
| 8 | **CRT monitor** | Archive footage | Built-in retro CRT over historical material |
| 9 | **Zoom punctuation** | Conclusion, suspense | Punch zoom = hammer · slow push = approach |
| 10 | **Transition set** | Edit grammar | Exactly three: whip pan (between list items) · dip to black (chapter breaks) · impact shake (slams) |

**Only three transitions exist.** A fourth has never been needed, and a
limited transition vocabulary is most of what makes an edit feel authored.

**Authorization rule:** build one exemplar, get it approved, *then* batch and
template. Editable properties — text, numbers, colors — must be exposed so
reuse is a data change, not a rebuild.

---

## Card library

Validated in production. Sidebar cards are the house favorite.

1. **Sidebar over face** ★ — presenter framed right, panel on the left.
   Transparent root with a horizontal gradient fading to full transparency at
   the right edge, an 8px accent spine on the left, blueprint grid inside.
   **The face stays visible throughout.** Best for openings, thesis
   statements, and mechanism explanation while the presenter is talking.
2. **Progressive build** — the motion rule made literal: a new element every
   3–5s tracking the current sentence. Never a static poster.
3. **Two-grammar contrast** — see [`brand.md`](brand.md#two-grammar-system).
4. **Image card** — top image, number, title, description, slow camera move.
   Two or three side by side make a process or roundup.
5. **HUD / live-counter** — dark ground, hero image, rotating reticle,
   per-frame counter (**labeled as an estimate**), scatter blips.
6. **Quote pop-out** — a matted cutout of the speaker rises into the
   bottom-right corner with an accent halo.
7. **Filler furniture** — self-drawn SVG icon flows with connector arrows,
   corner brackets, oversized faint watermark type, engineering rulers. Never
   leave large dead space.

### Card sizing: two options, no middle
**Large or dense → full screen**, covering the frame completely.
**Small graphic or single data point → fit into empty space** beside or below
the presenter, who stays the main subject.

The failure mode is the middle: a card covering most of the frame with a
sliver of face. Decide which of the two it is *before* sizing it.

---

## Track structure

```
V3  Cards / motion graphics        (top)
V2  B-roll + generated imagery     (muted; fills empty passages only)
V1  A-roll + narration audio       (base)
```

B-roll occupies only passages where no card is present. Narration continues
underneath, cards cover on top, B-roll fills the gaps. Simple, and it makes
"is anything on screen right now?" answerable by looking at one track.

### Density targets
- Pure voiceover passages: a new shot every **2–3s**, ≥20 shots/minute,
  no single shot static beyond 1s.
- **Hard cuts. No reuse.** One shot, one concept, strictly tracking the
  sentence.
- Generated to real footage ≈ **2:1** in the validation episode — real footage
  reserved for emotional beats and transitions. *This ratio is being revised
  downward; see [`ep7-case-study.md`](ep7-case-study.md).*

---

## Documentary J-cut transitions (deep dives)

Marked in the script as `----transition`. At each point:

1. The chapter's final line finishes **on the presenter's face.**
2. B-roll fades up over ~1.6s.
3. **A full 2s of silence** — 4s at a major break.
4. The next chapter's first one to three lines play as voiceover over B-roll.
5. Return to face at the sentence boundary.

If the recording has no natural pause, split the audio track and insert the
silence in the edit. B-roll at a transition head can run 8–11s for breathing
room.

The silence is the whole technique. Removing it collapses a documentary
transition into an ordinary cut.
