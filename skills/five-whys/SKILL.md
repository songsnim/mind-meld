---
name: five-whys
description: Drive a chain of why-questions down from a decision to the constraint that actually forced it — over a diff, a design choice, a module, or a concept. Best on gaps about why something was done this way rather than the obvious alternative. Use when someone accepts what a change does but cannot justify the approach.
argument-hint: "[pr number | branch | commit range | path | concept]"
disable-model-invocation: true
---

# five-whys

Resolve the target the way `../mind-meld/SKILL.md` does.

## Procedure

Start from the decision as stated, then ask why, one level at a time, waiting for the human's answer
at each level. Five is the shape, not a quota — stop at the level where the answer is a real
constraint (a requirement, a performance floor, an API that cannot change, a failure that already
happened) rather than another preference.

- Each why applies to their previous answer, not to the original decision.
- When an answer is a restatement ("because that's how it works"), ask what would happen if it were
  done the other way instead. The alternative's cost is the real answer.
- When the chain bottoms out at "the agent chose it and nothing forced it", that is a finding, and it
  belongs in the report as a question for the agent.

## Exit

Stop at a constraint the human can state, or when a level repeats itself twice — then say which link
of the chain is missing.
