---
name: microworld
description: Build a single self-contained interactive HTML microworld that faithfully embodies the mechanism of a target — a diff, a module, an algorithm, a system, or a concept — so a human can explore it and come away understanding how it actually behaves. Use when someone needs to see a mechanism run rather than read about it, or asks for an interactive explanation, simulator, or playground for a change or an idea.
argument-hint: "[pr number | branch | commit range | path | concept]"
disable-model-invocation: true
---

# microworld

Resolve the target the way `../mind-meld/SKILL.md` does. Read the target properly before building —
the microworld is only worth anything if its rules are the target's real rules.

## Goal

Build a dynamically and visually interactive microworld that faithfully represents the inherent
mechanism of the given artifact (concept, experiment, system, or idea), so that the user can
understand the whole idea, behavior, and mechanism of that artifact.

## Rules

- **Low floor, high ceiling.** Easy for a beginner to start, yet complex enough to allow advanced
  exploration.
- **Embodiment of powerful ideas.** Abstract concepts are embedded in the environment's rules and
  objects, not written on top of them as captions.
- **Immediate feedback.** Instant, non-judgmental visual response, so an error becomes a learning
  opportunity rather than a failure.
- **Composability and modularity.** Simple primitives can be combined and abstracted to build
  complex structures.
- **Learner agency.** Driven by the user's own goals and exploration, not by pre-programmed
  instruction.
- **Open-ended.** The microworld has no intent to guide the user. It just represents the world. That
  the user comes to understand it faithfully is a side effect — actually the main goal, but a hidden
  one.
- **Easy to understand.** Kind enough for a middle-school student. Every piece of jargon or technical
  terminology carries an explanation that appears on hover.

## Output

One self-contained HTML file. On Claude Code publish it as an Artifact; elsewhere write it to
`.mind-meld/<slug>.html` and print the path.

Do not put quiz answers, a verdict, or a prose summary of the change in the page. The page is the
world; the understanding is the human's to build.
