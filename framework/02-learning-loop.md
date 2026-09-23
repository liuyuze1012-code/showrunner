# 02 — The learning loop

> The agent may learn. It may not silently overrule you.

A production agent gets notes every single run. Without a protocol, those
notes live in chat history and die there — the same correction gets given for
the fifth time, and the human slowly concludes the agent "doesn't learn."

This is the protocol that turns a correction into a durable rule.

---

## The loop

```
critique during a run
   │
   ▼
distill into a rule, written in three parts
   │
   ▼
append to the INBOX  (learnings.md)
   │
   ▼
consolidation pass   (inbox > ~20 entries, or on request)
   │  fold rules into the canonical specs
   │  empty the inbox
   ▼
commit to git
```

Two storage tiers, and the distinction is the whole design:

| | Inbox | Canonical specs |
|---|---|---|
| **File** | `learnings.md` | `01-gates.md`, `03-trigger-table.md`, format specs… |
| **Contains** | Raw new feedback, unintegrated | Generalized, deduplicated rules |
| **Shape** | Append-only log | Structured reference |
| **Read by agent** | Last, for anything new | First, every run |
| **Steady-state size** | Near-empty | Grows slowly, stays organized |

An inbox that is never drained becomes an archive nobody reads. Draining it is
the maintenance that keeps the system honest.

---

## Rule format

Every entry has three parts. All three are mandatory.

```markdown
## YYYY-MM-DD — <one-line title>
- **Rule:** what to do or not do. Specific enough to act on without interpreting.
- **Why:** the reasoning or the incident behind it.
- **How to apply:** when it fires, what it interacts with, what it does not cover.
```

**The "why" is not documentation courtesy.** It is what lets a future
consolidation pass decide whether a rule still applies, generalizes, or has
been superseded. A rule without its reason cannot be safely revised, so it
gets frozen forever or deleted carelessly — both bad.

Bad entry:
> Don't use static cards.

Good entry:
> - **Rule:** Every card must introduce new motion — a new line, image or
>   reveal — at least every 3–5s, timed to transcript anchors. Trim each card
>   to end 0.5–1s after its final beat. If a passage cannot earn new motion,
>   show no card at all and stay on the presenter.
> - **Why:** Static cards read as slides, and a card held past its last beat
>   goes dead on screen. Reviewer rejections have always been over-decoration
>   or bad sync, never under-decoration.
> - **How to apply:** All formats. Compatible with the trigger table — this
>   governs a card's internal life, the trigger table governs whether it
>   appears at all. A card with no second beat available is a deleted card.

---

## Consolidation

Triggered when the inbox passes roughly 20 entries, or on request.

1. Group inbox entries by which canonical spec they belong to.
2. Fold each into that spec **in its own language and structure** — not
   appended verbatim. If five entries are five instances of one principle,
   write the principle.
3. **Never delete history silently.** A rule that is replaced gets superseded
   with a dated note saying what replaced it and why. Git keeps the full
   record.
4. Empty the inbox.
5. Commit, with a message describing what was integrated.

The highest-value consolidation is the one that finds the general rule hiding
behind a pile of specific ones. In the reference implementation, one pass
collapsed 56 individual corrections into a single 12-row decision table —
after which the agent handled situations that had never been explicitly
corrected, because it was matching on the underlying trigger rather than
recalling a list of past mistakes.

That is the difference between a system that accumulates rules and one that
actually learns.

---

## The escalation rule ★

> **If a new rule contradicts an existing spec, the agent stops and asks which
> wins. It does not choose.**

This is the safety property that makes the rest of the loop acceptable.

A self-modifying instruction set with no such constraint will, over enough
iterations, quietly reverse decisions the human made deliberately — because a
contradiction resolved in the moment always looks locally reasonable. The
human then finds their own standing policy gone, with no record of when or
why.

So the agent is permitted to:

- add a rule that covers new ground
- generalize several rules into one
- refine wording within an existing rule's intent

And is **not** permitted to:

- overturn a rule a human set deliberately
- resolve a contradiction between two specs on its own
- drop a rule because it seems obsolete

Contradictions escalate. Always.

### Deliberate overrides

Sometimes the human *does* want to break a standing rule for one episode. That
is fine, and it is recorded rather than quietly executed:

```markdown
## 2026-09-14 — ⚠️ EP7 overrides "no comparative framing" (director's call)
- **Conflict:** The format spec hard-bans comparative national framing.
  For this episode the director explicitly requires it.
- **Guardrails for this episode:** anchor only to facts, timelines and
  budgets; aim criticism at pitch decks and narratives, never at a country
  or an individual; present the counterpart's material as sourced fact, not
  triumphalism; honestly disclose where both sides hold similar long-horizon
  visions — the real difference being timeline honesty.
- **Why:** pure critique left the argument without a landing.
- **Open:** whether this becomes standard policy is the director's call after
  the episode's performance data. **Until then the spec is not to be edited.**
```

Note the last line. The override is scoped to one episode and carries an
explicit prohibition on generalizing itself. The agent executes the exception
without being able to promote it into policy.

---

## Why this matters beyond video

The pattern generalizes to any long-running agent with an evolving instruction
set:

- **Two tiers** — a cheap append-only inbox, and expensive curated canon.
- **Rules carry their reasoning**, so they can be revised rather than only
  obeyed or deleted.
- **Periodic consolidation**, or the canon rots into a changelog.
- **Version control**, so "why does it believe this?" is always answerable.
- **The agent cannot silently overrule a human decision.**

Most agent memory systems implement the first point and stop. The last one is
what makes the system safe to leave running for months.
