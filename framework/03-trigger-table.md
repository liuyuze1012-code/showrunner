# 03 — The trigger table: editorial judgment as executable logic

> Answers exactly one question: **given what is being said right now, what
> goes on screen?**

An agent asked to "make it visually engaging" will decorate everything. The
fix is not a better adjective. It is a decision table the agent can actually
execute, plus a default of doing nothing.

---

## The prime directive

> **Default state: clean face, subtitles, nothing else.**
>
> Every graphic must be *triggered* by the content of speech. If no trigger
> fires, add nothing.

Restraint is the style. In the reference implementation, every rejected cut
across a year of production was rejected for **over-decoration or bad sync —
never for under-decoration.** That asymmetry should shape the default.

---

## Triggers → treatments

Ordered by strength. The first match wins.

| # | The speaker is… | Treatment |
|---|---|---|
| 1 | Stating a shocking number | Stat card / evidence barrage. **Verify the number first** — ASR transposes digits. Re-listen, then confirm against a primary source |
| 2 | Being introduced | Name card or full-screen profile. Mandatory once per video |
| 3 | Describing a transformation (X → Y) | Morph takeover |
| 4 | Landing a one-word answer or definition | Big-word takeover |
| 5 | Revealing the product or solution | Product takeover |
| 6 | Describing a concrete visible thing for ≥4s | Split screen / flash B-roll / media window — the image must show **the thing said** |
| 7 | Enumerating out loud | Sequential visuals on the beats — only for lists actually spoken as lists |
| 8 | Changing topic | Section header |
| 9 | Emphasizing a key word | Accent-colored keyword in the subtitle *(the most common treatment by far)* |
| 10 | Concluding, or at a turning point | Beat zoom + keyword |
| 11 | Telling an emotional or personal story | **Nothing.** Clean face, slow breathing zoom. The story is the show |
| 12 | Bridging context | Keep light; reuse 1 or 2 only if a number or name lands |

Row 11 is not a gap in the table. It is the most important row in it. The
instinct to decorate an emotional beat is exactly the instinct this table
exists to suppress.

---

## Sync laws

Absolute. A violation is a defect, not a style disagreement.

1. **Elements enter on the spoken word** — using word-level timestamps from
   the **final cut**, never from storyboard estimates or a transcript of the
   raw file.
2. **Fill the pre-delay.** If a card is queued but its word hasn't arrived,
   run ambient motion. Never show the card early to avoid emptiness.
3. **No blank stage.** Audit second by second. Any dead gap gets a bridging
   visual; every media window has its next visual queued.
4. **Footage matches meaning, not keywords.** State what the line *asserts*
   (era, agent, mood) and what the footage *shows*; they must agree. A
   historical claim gets archival imagery. "Handed over to machines" gets
   modern machinery. Semantic match or nothing.
5. **Nothing static.** More than 3s held after entrance with no motion is a
   defect.
6. **One asset, one beat.** Never reuse a still or clip within a video. Vary
   the treatment across consecutive beats.
7. **Junction-cover law.** No fade may straddle an A-roll cut. Exit fast *on*
   the junction, or hold ≥0.3s past it. Chained coverage elements share exact
   boundaries — a butt-joint leaks a frame of the presenter's face between
   them.

### Why timestamps must come from the final cut
Word timings from the raw recording drift the moment anything upstream is
trimmed, and the error accumulates down the timeline. Cues taken from a
whole-file transcription smear. Transcribe **per section of the final cut**,
at segment level, and key from that.

---

## Rhythm

- **Chain the first 10 seconds.** Hook beats back to back — no single golden
  moment carrying the open alone.
- **After that: a beat at least every 10 seconds.** Audit in windows, not by
  feel.
- **Takeovers ≤6s, roughly one per 15s.** Long-form is exempt where sustained
  sections (picture-in-picture, media windows) replace this economy.

---

## Self-check before rendering

The agent runs this and answers in writing. "It looks good" is not an answer.

1. For each graphic: **which spoken words triggered it?** No answer → delete it.
2. For each 10-second window: is there a beat?
3. For each image: does it show what is being *said*, from the right era?
4. For each takeover: does content arrive within 0.2s of entry?
5. Is the final sentence of every segment complete, with the out-point past
   the last word?
6. **Cold-viewer test:** would someone arriving at second 0 know who is
   speaking and what they built?
7. Spot-check three random elements against word timestamps.

Question 1 does most of the work. Requiring a *spoken trigger* for every
element, in writing, kills decorative additions at the point they are
proposed — which is far cheaper than killing them in review.

---

## Adapting this to your show

The table encodes one show's editorial voice. Yours will differ — but the
*structure* is the transferable part:

1. **Start from rejections, not aspirations.** Go through work that got sent
   back. Each rejection is a trigger you hadn't written down.
2. **Order by strength.** When two triggers fire together, the table must
   already know which wins, or the agent will pick inconsistently.
3. **Include the "do nothing" rows explicitly.** Silence has to be a named
   choice in the table, or it never gets chosen.
4. **Keep it to roughly a dozen rows.** A table with 40 rows is a lookup the
   agent will match poorly. If yours is growing past ~15, you have specific
   instances that want generalizing — run a consolidation pass
   ([`02-learning-loop.md`](02-learning-loop.md)).
