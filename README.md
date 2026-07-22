# FosterMatch

Matches shelter animals to foster homes, and shows its reasoning.

A single-file demo: [`index.html`](index.html). No build step, no dependencies — open it in
a browser, or deploy the repo as-is to any static host.

## What it does

**Describe your home in plain language.** The matcher pulls structured constraints straight
out of the text and fills the form in front of you, so every answer is auditable and
correctable. Ambiguous descriptions get up to three clarifying questions back.

**Matching runs in two stages, deliberately kept apart:**

- **Gates** — hard constraints (species, resident pets, kids, yard, duration, medical,
  hours alone, capacity). Any failure disqualifies. These are never traded off against a
  high score.
- **Score** — a weighted 0–100 fit, decomposed into named factors so a coordinator can
  audit the ranking rather than trust it.

Preferences read from free text adjust the score as their own capped layer, weighted by
how emphatically they were stated — "I'd *really* love a senior" counts for more than
"maybe a senior, I guess".

**It shows its work.** A live reasoning stream replays the actual gate and factor
evaluation. Every score decomposes into the factors that produced it, and the prose
explaining a match is generated from those same factors, so the words and the number
can never disagree.

## The three views

| Tab | For |
| --- | --- |
| **I want to foster** | Public intake, ranked matches, animal profiles, AI-drafted application |
| **Messages** | Foster ↔ shelter inbox; applications open their own conversation |
| **Shelter board** | Coordinator queue, ranked fosters per animal, placement offers, recruitment advice when nothing fits |

## Notes

The matcher is a **rule-based engine** — regex extraction plus a weighted scoring model —
not a language model. It runs entirely in the browser. Calling it "AI" is fair, and the
page is unusually honest about it: every gate and score contribution is visible.

Everything is **simulated**. All animals, fosters, replies and messages are invented, and
nothing reaches a real shelter. Animal photographs are stock images used as placeholders —
they are *not* the animals described, and none of the medical or behavioural notes relate
to the animals pictured. Photo sources: dog.ceo, TheCatAPI, Wikimedia Commons.

State persists to `localStorage`; reset from the shelter board.

## Accessibility

Keyboard focus is visible throughout, and `prefers-reduced-motion` is respected — the
walking-cat animation is removed entirely and the reasoning stream renders at once instead
of typing out.
