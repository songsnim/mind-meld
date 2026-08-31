---
name: socratic
description: Run a Socratic dialogue over a target — a diff, a module, a design decision, a concept — asking one question at a time until the human's own answers expose what breaks and why. Best on risk and consequence gaps. Use when someone cannot say what would go wrong, or asks to be questioned rather than told.
argument-hint: "[pr number | branch | commit range | path | concept]"
disable-model-invocation: true
---

# socratic

Resolve the target the way `../mind-meld/SKILL.md` does. Read it fully first — a questioner who does
not know the answer asks aimless questions.

## Procedure

One question per turn. Wait for the answer. The next question comes out of what they actually said,
never from a prepared list.

- Start from what the human already believes, and probe its edge: the empty input, the concurrent
  call, the second caller, the failure path.
- When an answer is wrong, do not correct it. Ask the question whose answer contradicts it, and let
  them see the collision.
- When an answer is right but shallow, ask what it implies elsewhere in the system.
- Never ask two things at once, and never ask a question that contains its own answer.

## Exit

Stop when the human states the failure mode and its trigger in their own words, or when three
consecutive answers show no movement — then name, plainly, the specific thing still not understood.
That name is more useful than another question.
