# Getting started

**No coding required.** This guide assumes you have never used a terminal and
have never heard of Claude Code. Follow it in order.

Time to first result: **about 30 minutes.**

---

## What you are setting up

Showrunner is a set of written instructions that an AI assistant reads before
helping you make a video. It doesn't run on its own — think of it as a
detailed briefing document that turns a general-purpose AI into a production
crew that already knows your show.

You will:

1. Install **Claude Code** (an AI assistant that can read files on your computer)
2. Put the Showrunner folder where Claude Code can find it
3. Answer some questions about your show, so it tailors itself to you
4. Make a video

---

## Choose your tier first

This matters. Pick honestly.

### Tier 1 — Director mode · *no technical setup*

The AI plans and writes; **you edit by hand** in whatever you already use
(CapCut, Premiere, Final Cut, DaVinci Resolve, iMovie).

You get:
- Topic proposals against a selection rubric
- A full script, plus a clean read-aloud voiceover file
- A shot-by-shot animation plan — *at 1:32, show this, because he says this*
- Fact-checking with sources
- Subtitle text
- A QC checklist to run before you publish
- AI image prompts (you paste them into whatever image tool you use)

**Requirements: Claude Code. That's it.** Start here. Most of the value in
this framework is editorial judgment, and none of that needs a pipeline.

### Tier 2 — Full pipeline · *technical*

The AI also drives the editor and renders the video.

Additionally requires: a video editor an AI agent can control, `ffmpeg` built
with `libass` and `drawtext`, a speech-to-text tool, and headless Chrome for
rendering graphics. Setup is a few hours and involves the terminal.

**Don't start here.** Run Tier 1 for one video first. You'll know whether the
pipeline is worth building once you've seen what the director layer does.

> The rest of this guide covers **Tier 1**.

---

## Step 1 — Install Claude Code

**Easiest way: the desktop app.** No terminal.

1. Go to **[claude.ai/download](https://claude.ai/download)**
2. Download for Mac or Windows, install it like any other app
3. Open it and sign in (you'll need a Claude account — a paid plan is required
   for meaningful usage)
4. Find the **Code** tab

That's the whole install.

<details>
<summary>Prefer the terminal? (optional)</summary>

macOS / Linux:
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Windows PowerShell:
```powershell
irm https://claude.ai/install.ps1 | iex
```

Then run `claude` in any folder.
</details>

---

## Step 2 — Download Showrunner

1. Go to the repository page
2. Click the green **Code** button → **Download ZIP**
3. Unzip it. You'll get a folder called `showrunner-main`
4. **Rename that folder to just `showrunner`** (remove `-main`)

---

## Step 3 — Put it where Claude can find it

Skills live in a hidden folder called `.claude` in your home directory. The
leading dot makes it invisible in the file browser by default — here's how to
get to it.

### On Mac

1. Open **Finder**
2. Menu bar → **Go** → **Go to Folder…** (or press `Cmd + Shift + G`)
3. Type exactly:
   ```
   ~/.claude/skills
   ```
4. Press Enter
   - *Folder doesn't exist?* Go to `~/.claude` instead, and create a new
     folder inside it named `skills`. If `~/.claude` doesn't exist either,
     open Claude Code once and it will be created.
5. Drag your `showrunner` folder into `skills`

Final result should be:
```
~/.claude/skills/showrunner/README.md
~/.claude/skills/showrunner/SKILL.md
~/.claude/skills/showrunner/framework/...
```

### On Windows

1. Open **File Explorer**
2. Click the address bar and type:
   ```
   %USERPROFILE%\.claude\skills
   ```
3. Press Enter (create the `skills` folder if it isn't there)
4. Move your `showrunner` folder into it

---

## Step 4 — Tailor it to your show

This is the important step. Out of the box, Showrunner carries one show's
editorial voice — a Chinese-language space and technology explainer series.
**That is almost certainly not your show.**

Open Claude Code and type exactly this:

```
Use the showrunner skill and run the tailoring interview to set up my show.
```

Claude will interview you — about 15 questions covering what you make, who
watches, your visual style, your budget, and how you want to work. Answer in
plain language. "I don't know" is a valid answer; it will suggest something.

When it's finished it writes, into your showrunner folder:

| File | What it is |
|---|---|
| `config.local.yml` | Your brand colors, fonts, format, budget |
| `my-show/SKILL.md` | Your show's own skill file |
| `my-show/trigger-table.md` | **Your** rules for what goes on screen and when |
| `my-show/format.md` | Your structure, length, opening and closing patterns |
| `my-show/learnings.md` | Empty inbox, ready for feedback |

These are yours. Edit them any time — they're plain text.

> **You can re-run the interview whenever your show changes.** It reads what
> exists and updates rather than starting over.

---

## Step 5 — Make your first video

Type this:

```
Use the showrunner skill. I want to make a video about [your topic].
Start at Gate A and propose topics.
```

Claude will now stop at each gate and wait for you. When it asks for approval,
just answer in plain language — *"yes"*, *"no, make it shorter"*, *"I don't
like number 3."*

The sequence:

| Gate | Claude gives you | You do |
|---|---|---|
| **A — Topic** | A menu of angles | Pick one, or say what you'd rather do |
| **B — Script** | `SCRIPT.md` and `VOICEOVER.md` | Read the voiceover aloud. Change anything awkward |
| **Recording** | — | Record yourself reading it. Hand the file back |
| **C — Rough cut** | A cut plan, or the cut itself in Tier 2 | Approve or re-cut |
| **D — Animation plan** | A table: timecode → what appears → why | Approve, or delete rows you don't want |
| **E — AI images** | Prompts + a cost estimate | **Approve before anything is generated** |
| **F — QC** | A checklist, run against your video | Fix what it catches |

**You can stop at any gate and just take what you have.** Plenty of people
will only ever use Gate B, and that's a legitimate way to use this.

---

## What to expect on your first run

- **It will feel slow.** The gates are the point. By video three, you'll be
  approving most of them in seconds.
- **The first script will be about 70% right.** Correct it — and then read the
  next section, because those corrections are worth keeping.
- **It will refuse to generate images without permission.** Working as
  intended. See [Gate E](framework/01-gates.md#gate-e--generative-spend-).

---

## Step 6 — Teach it (this is what makes it improve)

Every time you correct something, say this afterwards:

```
Add that to the learnings inbox.
```

Claude writes the rule down, with the reason, in `my-show/learnings.md`. Next
video, it reads that file first.

After roughly 20 entries, say:

```
Run a consolidation pass on the learnings inbox.
```

It folds the accumulated notes into your permanent rules and clears the inbox.

**This is the difference between an AI that helps once and one that gets
better at your specific show every time you use it.** Skipping this step means
giving the same correction forever. Details in
[`02-learning-loop.md`](framework/02-learning-loop.md).

---

## Common problems

**"Claude doesn't seem to know about the skill."**
Check the folder path is exactly `~/.claude/skills/showrunner/` and that
`SKILL.md` sits directly inside it — not inside a second nested folder. The
most common cause is an unzipped folder containing another folder of the same
name.

**"It's making things up / getting facts wrong."**
Tell it: *"Verify every number against a primary source and cite it."* Fact
discipline is in Gate B, but say it out loud on early runs.

**"The script doesn't sound like me."**
Expected on run one. Paste in a transcript of something you've made and say
*"match this voice."* Then add that to learnings.

**"It wants to add graphics everywhere."**
Tell it to re-read [`03-trigger-table.md`](framework/03-trigger-table.md). The
default is supposed to be **nothing**.

**"I don't want to use gates, just write me a script."**
Fine. Say *"skip to Gate B."* The framework is a default, not a cage.

---

## Where to go next

| You want | Read |
|---|---|
| To understand the approval system | [`01-gates.md`](framework/01-gates.md) |
| Your graphics rules to be better | [`03-trigger-table.md`](framework/03-trigger-table.md) |
| Consistent AI-generated imagery | [`04-visual-consistency.md`](framework/04-visual-consistency.md) |
| To stay out of trouble (AI labels, footage rights) | [`05-compliance.md`](framework/05-compliance.md) |
| To see a real show built this way | [`reference-impl/space101/`](reference-impl/space101/) |
