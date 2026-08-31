---
name: first-principles
description: Rebuild an unfamiliar idea from its primitives — over a concept, an algorithm, a library, or the idea underneath a diff — until the human can derive the target instead of memorizing it. Best when the vocabulary itself is new. Use when someone is blocked not on a change but on the concept the change assumes.
argument-hint: "[concept | pr number | branch | commit range | path]"
disable-model-invocation: true
---

# first-principles

Resolve the target the way `../mind-meld/SKILL.md` does.

## Procedure

1. Strip the target down to the primitives it rests on — the smallest facts the human already accepts
   without proof. Name them explicitly.
2. Check each primitive with them. An unverified primitive is where every later confusion comes from.
3. Rebuild upward one step at a time, and at each step ask what has to be true for the next step to
   follow. The human takes the step; you only ask.
4. Arrive back at the target and ask them to state why it must look the way it looks.

## Rules

- No analogy until the primitives are agreed. An analogy over a shaky base hides the shakiness.
- Define every term at the moment it is first needed, never earlier.
- If a primitive turns out to be unfamiliar too, recurse into it before continuing.

## Exit

Stop when the human derives the target from the primitives unaided, or when the same primitive fails
twice — report which primitive is missing, because that, not the target, is what they need next.
