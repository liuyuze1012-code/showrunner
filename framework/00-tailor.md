# 00 — Tailor: fit this framework to a show

> **Agent:** read this file when the user asks to set up, tailor, configure or
> customize Showrunner for their show. Conduct the interview, then generate
> their files.

Out of the box this framework carries one show's editorial voice. That voice
is almost certainly wrong for the person in front of you. This protocol
replaces it with theirs.

**Output:** a `my-show/` directory and a `config.local.yml`, both owned and
editable by the user.

---

## How to run the interview

**Ask in small batches — three or four questions at a time, not fifteen at
once.** Use plain language. The user may be non-technical; never assume they
know what a trigger table, an accent token or a J-cut is.

Rules:

- **"I don't know" is a valid answer.** Propose a sensible default, explain
  the tradeoff in one sentence, and move on. Never block.
- **Infer instead of asking.** If they say "product reviews for a YouTube
  audience," you already know the length range, the aspect ratio and roughly
  which triggers matter. Confirm, don't interrogate.
- **Ask for examples, not descriptions.** "Name two channels whose style you
  like" tells you more than any adjective they could offer.
- **Never ask about brand colors as hex codes.** Ask what feeling they want,
  or what their existing logo uses, and propose the values yourself.

---

## The interview

### Part 1 — What are you making

1. **Describe your show in one sentence**, as if to a stranger.
2. **What kind of video is it?** Offer the profiles in
   [`../profiles/`](../profiles/) and pick the closest — explainer / video
   essay, news breakdown, interview or podcast cutdown, product review,
   tutorial, documentary short. *"Something else"* is fine; build from the
   closest one.
3. **How long, and how often?**
4. **Where does it get published?** (Determines aspect ratio, safe areas,
   disclosure rules, subtitle style.)
5. **What language?**

### Part 2 — Who it's for, and what it promises

6. **Who watches, and what do they get from it?**
7. **What is your show's promise in one sentence?** — the thing you would never
   violate. *This is the most important answer in the interview.*
   Examples: *"We don't sell anxiety, we show evidence." · "Always practical,
   never theoretical." · "The fun version of a boring subject."*
   Everything downstream should be derivable from it. If they can't answer,
   come back to it after Part 4 — it's often easier once they've described
   what they hate.
8. **Name two or three channels whose style you like**, and one you actively
   don't. The negative example is usually more informative.

### Part 3 — On screen

9. **Are you on camera?** Presenter-led, voiceover-only, or mixed. (Governs
   whether the default state is a face, and whether "show nothing" is
   available as a treatment.)
10. **What should it feel like?** Two or three adjectives. Propose colors and
    fonts from the answer; don't ask for hex codes.
11. **Do you have a logo, brand colors, or existing videos to match?**
12. **How much motion do you want?** Offer three settings:
    - **Restrained** — graphics only when the content demands it *(recommended;
      the framework default)*
    - **Standard** — a visual beat roughly every 10 seconds
    - **Dense** — near-continuous motion *(fast-cut social style)*

### Part 4 — How you want to work

13. **Which gates do you want?** Explain them in one line each. Default them
    all on, but note that people who only want scripts can keep Gate B alone.
14. **Will you use AI-generated images or video?** If yes: what monthly budget,
    and confirm Gate E is on. If no, skip generation entirely and say so in
    their config.
15. **What's your editing setup?** Determines Tier 1 (they edit by hand) versus
    Tier 2 (the agent drives the tools). Don't push Tier 2 on someone who isn't
    asking for it.
16. **Anything that must never happen in your videos?** Topics, words, visual
    clichés, competitor mentions. These become hard rules.

---

## Then: build their trigger table

Do not hand over the reference table unchanged. Build theirs:

1. **Start from the profile preset** in [`../profiles/`](../profiles/).
2. **Cut rows that don't apply.** A tutorial channel has no "guest being
   introduced" row. Fewer rows execute better.
3. **Add rows from their answers.** If they said "I always want the price on
   screen when I mention it," that's a trigger.
4. **Keep the do-nothing rows.** Every table needs at least one, or silence
   never gets chosen. If they're presenter-led, the emotional-story row stays.
5. **Order by strength**, so the agent knows which wins when two fire.
6. **Cap it at roughly a dozen rows.** Longer tables match worse.

Show them the finished table in plain language and ask what's missing. This
is the deliverable they will feel most.

---

## Files to generate

Write these. Tell the user what each one is and that they can edit any of them.

```
config.local.yml            filled from the interview (gitignored)
my-show/
├── SKILL.md                their show's entry point
├── trigger-table.md        their table, derived above
├── format.md               structure, length, opening/closing patterns
├── brand.md                colors, fonts, on-screen furniture
└── learnings.md            empty inbox, using the standard template
```

### `my-show/SKILL.md`
Frontmatter with a `name` and a `description` that triggers on *their* show's
name and content type. Body: the promise sentence from Q7, the gate
configuration, hard rules from Q16, and links into `framework/`. Keep it
short — it routes, it doesn't duplicate.

### `my-show/format.md`
Their structure: opening pattern, section rhythm, closing pattern, target
length, and what the show never does. If they named reference channels, encode
what's actually transferable from them — structure and pacing, not personality.

### `my-show/brand.md`
Concrete tokens: background, **one** accent, text colors, fonts, corner tags,
safe areas for their platform. Enforce the single-accent rule and explain in
one line why it matters.

---

## Close the session

Tell them, briefly:

1. **What you built**, and that all of it is editable plain text.
2. **How to start their first video** —
   *"Use my show skill. I want to make a video about X. Start at Gate A."*
3. **How to teach it** — say *"add that to the learnings inbox"* after any
   correction. This is the step that makes it improve, and the one people skip.
4. **That they can re-run this interview** whenever the show changes; it
   updates rather than starting over.

Do not dump the generated files into chat. Write them, then summarize.

---

## Re-running

If `my-show/` already exists: read it first, ask what's changed, and **edit in
place.** Never silently discard rules the user has accumulated — their
`learnings.md` and any hand-written trigger rows are the most valuable files
in the directory. If a new answer contradicts an existing rule, say so and ask
which wins ([`02-learning-loop.md`](02-learning-loop.md)).
