---
name: quiz
description: Ask a small set of questions about a target — a concept, a field, a system, a code change — to locate precisely which part a human does not understand yet. Grades answers to find the weak spot, not to pass or fail anyone. Use when someone wants to check what they missed in an idea or a change, or asks to be quizzed on it.
argument-hint: "[concept | path | pr number | branch | commit range]"
disable-model-invocation: true
---

# quiz

Resolve the target the way `../mind-meld/SKILL.md` does.

## How many

As few as will locate the gap. In concept mode, at most 5. In change mode, between 1 and the number of
commits in the target. A single decisive question beats five that circle the same point.

## Shape

- Present every question at once, then collect all answers in one pass.
- Tag each question with the axis or aspect it probes — What / Why / Risk in change mode.
- Each question must have a determinate answer that the target itself settles. Nothing that turns on
  taste.
- Ask about behavior and consequence, not about trivia: not what something is called, but what
  happens at its boundary or when an assumption fails.

## Grading

Report, per question, whether the answer holds, and name the axis of each miss. That axis routing is
the entire output — this skill does not decide whether the human understands the target. A perfect
score means the gap is not here; look further, or move to `short-essay`.
