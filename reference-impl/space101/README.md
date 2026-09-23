# Reference implementation — 太空101 / Space 101

A worked example of [Showrunner](../../README.md) in production.

**太空101 (Space 101)** is the solo explainer franchise of **雏形 / Prototype**,
a Chinese-language frontier-technology channel covering space systems,
robotics, AI infrastructure and semiconductors. Episodes are evidence-led
teardowns: they separate *whether the engineering works* from *whether the
narrative built on top of it holds together*.

The channel's on-air promise, and the line that governs every editorial call:

> **我们这个频道不卖焦虑，只讲证据。**
> *We don't sell anxiety on this channel. We show evidence.*

That single sentence is why the trigger table defaults to nothing, why real
footage outranks generated footage, and why every synthetic shot is labeled.
A show's constraints should fall out of its promise.

---

## Format

| | |
|---|---|
| Aspect | 16:9 · 3840×2160 · 30fps CFR |
| Length | 3–5 min short form · 10–30 min deep dive |
| Delivery | Music-free master + a music cue sheet (the director scores separately) |
| Distribution | Douyin (TikTok China) + podcast platforms |
| Sub-branding | Swap the corner tag: 太空101 / 机器人101 / AI101 (Space / Robotics / AI 101) |

A 9:16 vertical layout with a three-zone geometry (corner presenter bubble,
full-width cards, centered subtitles) is retained as legacy from earlier
episodes.

## Files

| File | Contents |
|---|---|
| [`brand.md`](brand.md) | Constant brand layer + the three-skin system |
| [`components.md`](components.md) | Ten standard animation components, the card library, and the track structure |
| [`ep7-case-study.md`](ep7-case-study.md) | One shipped 4K episode, start to finish, including what broke |

## How it maps to the framework

| Framework pattern | How this show implements it |
|---|---|
| [Gates](../../framework/01-gates.md) | Full A–F chain. Generation is hard-gated: all real B-roll and animation finish first, then a prompt table plus budget goes up for approval, then every generated asset is reviewed individually |
| [Learning loop](../../framework/02-learning-loop.md) | `learnings.md` inbox → periodic consolidation into director/style/format specs → git. One episode's comparative-framing override is recorded as a scoped exception the agent may not generalize |
| [Trigger table](../../framework/03-trigger-table.md) | 12 rows, derived from a year of rejections. Row 11 — *emotional story → show nothing* — is the one that most improved the show |
| [Visual consistency](../../framework/04-visual-consistency.md) | Locked papercraft-diorama recipe (one variable slot); three card skins, one per episode; single-accent rule enforced throughout |
| [Compliance](../../framework/05-compliance.md) | Platform AI declaration + per-shot chips; three-tier licensing with a per-episode `SOURCES.md`; finance-content risk controls |

## Division of labor

A cost-driven split worth copying:

- **Agent-drivable editor** — generation (the only metered operation),
  rough assembly, code-authored motion graphics, built-in effects, export.
  *Everything except generation is free; only generation burns credits.*
- **Local pipeline** — subtitles, sectional compositing, QC, master delivery.
  ffmpeg (a build **with** `libass` and `drawtext` — stock builds often ship
  without), `whisper.cpp`, OpenCC for script conversion, and headless Chrome
  driven by Puppeteer for deterministic HTML→frames rendering.

Deterministic rendering is the piece worth stealing: cards are HTML pages
exposing a `window.setFrame(f)` hook, screenshotted frame by frame and
assembled by ffmpeg. Motion graphics become **code** — diffable, reviewable,
version-controlled, reproducible — with no GUI animation tool in the loop.
