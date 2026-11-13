---
name: mind-meld
description: Run a comprehension session that makes a human actually understand something unfamiliar — a concept, a body of domain expertise, an algorithm, a library, a system, a design decision, or a code change. Builds an interactive microworld, waits for the human to explore it, quizzes them, drills the weak spot with one deep tool, then grades a short essay until the understanding holds. Use when someone needs to genuinely understand a piece of knowledge rather than read a summary of it, or says "I want to really understand this", "what is this concept", "explain this until I get it", "I don't get this change", "왜 이렇게 되는 거지", "이 개념 제대로 이해하고 싶다".
argument-hint: "[concept | path | pr number | branch | commit range] [--lang <code>]"
---

# mind-meld

Understanding is a human act, and reading an explanation only produces the impression of it. This
skill drives that act to a measured floor instead of hoping the human read enough. It teaches nothing
directly — it builds a world the human can poke, then keeps asking until their own explanation is good
enough.

The seven tools (`microworld`, `quiz`, `socratic`, `feynman`, `five-whys`, `first-principles`,
`short-essay`) are separate skills and can be invoked alone. This skill is the only one that routes
between them automatically.

## Targets

Resolve the argument in this order:

| Argument shape | Target |
| --- | --- |
| `42`, `#42`, a PR/MR URL | that pull request |
| a branch name | `merge-base..branch` |
| `a..b`, `a...b` | that commit range |
| a file or directory path | that code or document |
| anything else | the concept, topic, or field as written |
| no argument | what the conversation is currently about; if nothing, ask |

A bare word can be both a branch and a concept (`main`, `cache`, `router`). When the shape is
ambiguous, state the reading you picked and ask once — one line, then proceed. Never run a whole
session against a mis-resolved target.

## Modes

**Concept mode** — the default: a concept, a field's expertise, an algorithm, a library, a system, a
module, a path. One 0-10 comprehension score, no fixed axes. The report is optional, and the shape of
the session is free: follow the knowledge, not a template.

**Change mode** — the target is a diff (PR, branch, commit range). Three axes:

- **What** — what changed.
- **Why** — why this way, and not the obvious alternative.
- **Risk** — what can break, and where it would show.

Everything else below is identical across modes. The only differences are the axes, the quiz count,
and whether a report file is required.

## Pipeline

1. **Read the target.** For a concept or a field, read the sources that define it — specifications,
   papers, documentation, the code that uses it — until you can say what is true and where its edges
   are. For a diff, read it plus enough surrounding code to know why it works, not only that it
   changed. On a large target, skip generated files, lock files, vendored code and pure test churn —
   and record every exclusion, it goes in the report. Never claim coverage you did not read.

2. **Build a microworld.** Invoke `microworld` against the target. On Claude Code publish it as an
   Artifact; elsewhere write it to `.mind-meld/`. Hand the human the link or path and **stop**. Wait
   for them to say they are done exploring. Do not summarize the target in prose while waiting — the
   summary would replace the exploration.

3. **Quiz.** Invoke `quiz`. In concept mode ask at most 5 questions; in change mode between 1 and
   one-per-commit. Fewer is better. Present them all at once, tag each question with the axis or
   aspect it probes, and collect the answers in one pass. The quiz locates the weak spot; it never
   decides whether the human passes. A perfect quiz skips step 4.

4. **Drill the weak spot.** Pick one deep tool — two only if two areas are genuinely broken. Default
   routing:

   | Weakness | Tool |
   | --- | --- |
   | What — cannot state what happens | `feynman` |
   | Why — cannot justify why it is this way | `five-whys` |
   | Risk — cannot say what breaks or where it stops holding | `socratic` |
   | The underlying idea is unfamiliar | `first-principles` |

   Depart from the table when the answers point elsewhere (a wrong answer caused by unfamiliar
   vocabulary is not a Why gap), and say why you departed.

5. **Short essay.** Invoke `short-essay`. One prompt: explain this to a colleague, from memory. Never
   split it into per-axis questions — a form gets filled in, an explanation gets constructed, and the
   part the human forgets is itself the finding. Grade the essay: one 0-10 score in concept mode,
   each axis 0-10 in change mode.

6. **Pass or loop.** Pass requires **8 or higher on every axis**. Below that, explain only the
   failing part, briefly, then have them revise the same essay. After **2 failed revisions**, switch
   to a different deep tool and try again. If that tool also fails twice, **stop** and write the
   report: four explanations that did not land is evidence the target is unclear, not that the human
   is slow.

## Report

Write `.mind-meld/<slug>-report.md` in change mode:

- the three axis scores,
- what stayed unclear, concretely,
- **questions to send back to whoever produced the target** — the author, the agent, the source,
- anything excluded from the read in step 1.

In concept mode the report is optional; when written, the questions section becomes "open questions".

Never post or send the report anywhere. It is the human's to send.

## Output locations

`.mind-meld/` in the repository root, or in the current directory when outside a repository. Inside a
repository, add `.mind-meld/` to `.git/info/exclude` if it is not already there — never edit the
project's `.gitignore`, the working tree must stay clean.

Nothing persists between sessions. A second session on the same target starts from step 1.

## Rules

- Speak the human's language. Grading an essay written in a second language measures writing, not
  understanding.
- Never give away an answer the human is still working on, in the microworld or in a question.
- Whatever the human decides on top of this understanding — approve, adopt, act — is theirs. This
  skill measures comprehension and stops.
