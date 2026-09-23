# 太空101 — Brand system

Two layers. The **constant layer** never changes. The **skin** changes once
per episode.

---

## Constant layer

Never varies, across every episode and every sub-brand.

### Palette — "Mars Ember" 火星余烬

| Token | Hex | Role |
|---|---|---|
| Warm black | `#0A0806` – `#12100E` | Base |
| Deep blueprint | `#081422` | Deep ground for blueprint treatments |
| **Ember orange** | **`#E05A2B`** | **The single accent** |
| Sand | `#D9C6A8` | Secondary text, rules |
| Warm white | `#F5EFE8` | Primary text |
| Dawn gold | `#E9B84F` | *Reserved* — finale sublimation and endcard only |

**The single-accent rule:** ember orange is the only saturated color on
screen. Dawn gold is not a second accent; it appears only at the emotional
resolution of an episode and on the endcard. Adding a third color has been
proposed and rejected every time — a one-accent frame is what makes the
accent mean something.

### Typography

| Role | Face |
|---|---|
| Headings, subtitles | Noto Serif SC |
| Body copy | LXGW WenKai TC (楷体 — a calligraphic running script) |
| Large numerals | Playfair Display |
| Calligraphic corner tag | Ma Shan Zheng |

Verify font names against your renderer's available list before building. In
HTML rendering paths, system fonts need an explicit
`@font-face { src: local('...') }` declaration or they silently fall back.

### Motion language
One entrance language per video. Cards live under the motion rule in
[`04-visual-consistency.md`](../../framework/04-visual-consistency.md): new
motion every 3–5s, trimmed to 0.5–1s past the final beat, and **no card at
all** where a passage can't earn one.

---

## The three skins

The card *surface* varies; everything above does not. **Pick one per
episode. Never mix two in one video.**

| Skin | Surface | Use for |
|---|---|---|
| ① Cold lab white 冷白实验室 | `#EDF0F3` | Data-dense episodes |
| ② Deep-space console 深空控制台 | `#141A22` + warm hairline | Immersive narrative episodes |
| ③ Engineering blueprint 工程蓝图 | `#12263E` + white line-work + dashed frames | Mechanism teardowns, flagship episodes |

Skin selection is an **editorial** decision, not a decorative one — you are
choosing how the episode *argues*. A teardown wants blueprint; a
numbers-driven investigation wants lab white.

Store each skin in your editor's style library and apply it at the start of
an episode so every component inherits it. Keep the style IDs in
`config.local.yml`, never in the repo — they are account-scoped and useless
to anyone else.

> **Rejected:** a yellow-toned paper card surface. *"Not tech enough."*
> Recorded because it was proposed twice.

---

## Two-grammar system

Within one brand, two opposing visual grammars carry two opposing arguments.
Introduced for the orbital-data-centers episode and now reusable for any
claims-versus-reality structure.

### Promotional grammar — for claims, pitches, projections
Spotlight cone (clip-path triangle gradient) · glowing Playfair numerals ·
"PITCH DECK" chrome · scanlines · spark bursts · orange punch-words.

### Blueprint grammar — for shipped reality, budgets, timelines
Blueprint grid · dashed planning panels and node diagrams · hand-drawn accent
underlines · 印章 seal stamps (**实证** *verified* / **务实** *pragmatic* /
**已实现** *delivered*) · engineering rulers · measured left alignment.

Both live inside the constant layer — same accent, same fonts, same motion
language. The viewer feels the argument before parsing it, and it still reads
as one show making a point rather than two shows spliced together.

See [`04-visual-consistency.md`](../../framework/04-visual-consistency.md#grammar-as-argument).

---

## Corner tags and safe areas

- **Left tag:** 「雏形 · <domain>101」— swapping the domain word re-brands the
  franchise (太空101 / 机器人101 / AI101).
- **Right tag:** episode number and theme. During any valuation or market
  segment it is replaced by the persistent
  **「不构成投资推荐」***(not investment advice)* tag.
- **Vertical safe areas (legacy 9:16):** key content ≥100px from the side
  edges, ≥140px from the top; the bottom 200px belongs to subtitles. Bottom
  corners need ≥190px clear of platform UI overlay.
