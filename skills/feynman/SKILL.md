---
name: feynman
description: Run the Feynman technique over a target — a diff, a module, a concept — having the human explain it in plain language, then hunting the exact points where the explanation goes vague and sending them back to the source. Best on gaps about what something actually does. Use when someone thinks they understand a change or an idea but cannot state it simply.
argument-hint: "[pr number | branch | commit range | path | concept]"
disable-model-invocation: true
---

# feynman

Resolve the target the way `../mind-meld/SKILL.md` does.

## Procedure

1. Ask the human to explain the target as if to someone who knows the language but not this codebase
   or this field. No jargon. If a term is unavoidable, they define it in the same breath.
2. Read their explanation and mark every place it goes vague: a term used as a placeholder for a
   mechanism, a step where "it handles" replaces what happens, a claim with no cause.
3. Give the marked list back — the vague spots only, not the answers — and point them at the source
   that settles each one.
4. Have them re-explain. Repeat until nothing is vague.

## Rules

- Never fill a gap for them. The whole method is that the gap becomes visible and they close it.
- Analogies count only if they carry the mechanism. An analogy that just relabels the thing is a
  vague spot.

## Exit

Stop when the explanation survives with no marked spots, or after two full rounds with the same spot
unresolved — report that spot and stop.
