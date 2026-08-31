---
name: short-essay
description: Have the human write one short explanation of a target from memory — a diff, a module, a concept — then grade it to measure comprehension, and drive revisions until it holds. This is the measuring instrument, and also a generation-effect exercise. Use when someone wants their understanding of a change or an idea actually checked rather than assumed.
argument-hint: "[pr number | branch | commit range | path | concept]"
disable-model-invocation: true
---

# short-essay

Resolve the target the way `../mind-meld/SKILL.md` does.

## Prompt

One prompt, always: **explain this to a colleague, from memory.**

Never split it into one question per axis. A form gets filled in; an explanation gets constructed.
Which part the human leaves out on their own is the measurement.

## Grading

Change mode — score each axis 0-10:

- **What** — is the actual change stated, correctly and specifically?
- **Why** — is the approach justified against the alternative?
- **Risk** — is a real failure mode named, with where it would show?

Concept mode — one 0-10 score for whether the explanation would let a colleague act on it.

Pass is **8 or higher on every axis**. Score honestly: a generous 8 wastes the whole session.

## Revision loop

Below the floor, explain only the failing part, briefly, then have the human revise the same essay —
not write a new one. After two failed revisions, hand back to a different deep tool
(`socratic`, `feynman`, `five-whys`, `first-principles`) rather than explaining a third time.

Report the scores and, for each axis under 8, the specific thing missing.
