---
name: quiz
description: Ask a small set of questions about a target — a diff, a module, a concept — to locate precisely which part a human does not understand yet. Grades answers to find the weak spot, not to pass or fail anyone. Use when someone wants to check what they missed in a change or a concept, or asks to be quizzed on it.
argument-hint: "[pr number | branch | commit range | path | concept]"
disable-model-invocation: true
---

# quiz

Resolve the target the way `../mind-meld/SKILL.md` does.

## How many

As few as will locate the gap. In change mode, between 1 and the number of commits in the target. In
concept mode, at most 5. A single decisive question beats five that circle the same point.

## Shape

- Present every question at once, then collect all answers in one pass.
- Tag each question with the axis it probes — What / Why / Risk in change mode.
- Each question must have a determinate answer that the target itself settles. Nothing that turns on
  taste.
- Ask about behavior and consequence, not about trivia: not what a function is named, but what
  happens when it gets an empty list.

## Grading

Report, per question, whether the answer holds, and name the axis of each miss. That axis routing is
the entire output — this skill does not decide whether the human understands the target. A perfect
score means the gap is not here; look further, or move to `short-essay`.
