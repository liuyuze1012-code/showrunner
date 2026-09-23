# 05 — Compliance: disclosure, licensing, and risk

> Compliance is a design constraint, not a final review step. Retrofitting it
> costs a re-render; building it in costs nothing.

Three separate problems, often confused:

1. **AI disclosure** — telling viewers and the platform that content is synthetic
2. **Media licensing** — the right to use footage you didn't shoot
3. **Editorial risk** — phrasing that gets a video suppressed or reported

---

## 1. AI disclosure

### The rule
Where AI-content labeling is legally required, **declare it.** China's
labeling measures (《人工智能生成合成内容标识办法》, in force 1 September 2025)
require synthetic content to be identified, and major platforms implement
this as a toggle at upload plus automatic detection.

The practical calculus is one-sided:

| | Declared | Not declared |
|---|---|---|
| Detected as AI | Normal distribution | Auto-flagged "suspected AI", reach throttled |
| Not detected | Normal distribution | Compliance exposure |

**Declaring costs nothing. Concealment is the only losing move.** Platforms
have generally been promoting AI-assisted content, not suppressing it — the
penalty attaches to non-disclosure, not to the technique.

### Two layers
1. **Platform declaration** — the upload-time toggle. Non-negotiable.
2. **Per-shot on-screen chip** — a small label on each synthetic shot.

Do both. The platform toggle is a legal act; the on-screen chip is an
editorial one, and it protects credibility. A viewer who spots an unlabeled
synthetic shot in an evidence-based show discounts everything else in it.

### Implementation notes
- **Frame-match the chip to the clip's real length.** Generated clips
  frequently come back shorter or longer than requested. Measure the delivered
  asset, don't trust the request.
- **Watch for label loss on direct-to-timeline clips.** If a clip bypasses the
  wrapper that carries its chip, the chip vanishes silently. Either add a
  global fallback label or re-layer the chip on the timeline.
- **Don't strip provenance watermarks** (SynthID and equivalents). Removal is
  itself a violation in most jurisdictions.
- **Keep the declaration in the description too**, where the platform allows.

---

## 2. Media licensing

### Three tiers
Classify every asset before it touches the timeline.

| Tier | Meaning | Handling |
|---|---|---|
| 🟢 **Green** | Public domain or clearly cleared for commercial use | Use freely |
| 🟡 **Amber** | Official release requiring attribution (CC-BY etc.) | Use, and **credit in the description** |
| 🔴 **Red** | Fair-use claims, press screenshots, non-commercial licenses, corporate renders | Flag individually; the human decides case by case and accepts the risk |

### The trap that catches everyone
**Non-commercial licenses.** CC BY-**NC** material is red-tier for any
monetized channel, no matter how official the source looks. A well-known
example: SpaceX's Flickr library is CC BY-NC — widely reused, and not clear
for a channel running ads or sponsorships.

Reliably green sources include public-domain government agency imagery (NASA
and similar) and the major stock libraries that grant commercial use without
attribution. Verify per asset rather than per site; libraries mix licenses.

### The source manifest
Maintain `SOURCES.md` per episode. Required columns:

```markdown
| Asset | URL | Tier | Orientation | Covers which line | Attribution string |
```

This is not bureaucracy. It is what lets you answer a takedown in ten minutes
instead of a day, and it is the only way attribution survives contact with an
edit that reorders everything.

**Attribution goes in the published description**, assembled from the amber
and red rows at delivery time.

---

## 3. Editorial risk

### Finance-adjacent content
When an episode touches valuations, funding, IPOs or share prices, apply a
stricter standard:

1. A persistent **"not investment advice"** corner tag from frame 0 to the last
   frame, repeated in the description.
2. **Zero price predictions. Zero buy/sell implication.** Audience-facing
   segments explain how to *think* about a sector — bullish on an industry is
   not the same as right about a stock, and should be said out loud.
3. **Loaded words only inside attributed quotes.** "Bubble", "mania" and
   similar appear when quoting a named authoritative source. Original analysis
   uses neutral phrasing.
4. **Character-by-character verification** of every company name and financial
   figure on screen. One wrong digit in front of an industry audience is not a
   typo — it is the whole video's credibility.

### Sensitive events
Use official or industry-standard terminology rather than colloquial framing
("flight anomaly" / "test failure" rather than "blew up"), and pair a specific
incident with the general industry context in the same breath. This is not
euphemism — it is the register the subject-matter audience uses, and the one
least likely to be read as sensationalism.

### Comparative and political framing
Where comparative national framing is part of the argument, anchor it and fence
it:

- Compare **facts, timelines and budgets** — never national character.
- Aim criticism at **claims, pitch decks and narratives** — never at a country
  or an individual.
- Present the counterpart's material as **sourced fact**, not triumphalism.
- **Disclose honestly** where both sides hold similar positions, and name what
  the real difference is.

The platform risk is usually misjudged: praising one's own side is generally
low-risk; **inflaming antagonism between groups is the thing that gets
suppressed.** Restraint in phrasing is what keeps a comparison publishable.

### Estimates
Any number you derived rather than sourced is labeled as an estimate **in the
voiceover and on screen**. "Our estimate, not an official figure" costs two
seconds and forecloses the accusation that you fabricated data.

---

## Troubleshooting a blocked upload

Diagnose in this order — cheapest fix first:

1. **Video fingerprint.** Re-used footage can collide with existing content.
   An all-stills version with camera moves carries no video fingerprint and
   frequently passes where the original failed.
2. **Duration.** Split into parts.
3. **Phrasing.** Re-examine loaded language, incident terminology, and
   comparative framing.

---

## Building compliance into the pipeline

| Stage | Compliance action |
|---|---|
| Script | Flag claims needing a source; mark estimates; mark loaded phrasing |
| B-roll sourcing | Assign a tier and write the `SOURCES.md` row **at download time** |
| Generation gate | Every generated asset is pre-registered as requiring a chip |
| Build | Chips frame-matched; persistent tags placed |
| QC | Verify every chip; assemble the attribution string |
| Delivery | Delivery note states which platform declarations are required |

Sourcing is the step that matters most: an asset whose license is recorded at
download time is never a problem later, and an asset whose license you have to
reconstruct in QC usually is.
