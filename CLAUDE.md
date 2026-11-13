# CLAUDE.md

## What this repo is

`mind-meld` is a tool suite of Agent Skills that makes a human actually understand unfamiliar
knowledge — a concept, a field's expertise, an algorithm, a library, a system, a design decision, or
a code change. No venue is assumed: a pull request is one valid target among many, not the default.

The problem it attacks: reading an explanation produces the impression of understanding, not the
understanding. Summaries do not fix it. So the loop is the product: build a world, quiz, drill, then
**measure** the human's own explanation and repeat while it sits below the floor.

Named after Star Trek's Vulcan mind meld — a way into another mind (an expert's, an author's, an
agent's).

## Layout

```
.claude-plugin/{plugin,marketplace}.json   Claude Code plugin + self-hosted marketplace
README.md                                  English source; five per-host install blocks
docs/i18n/README.{ko,zh,ja,es,pt,ru}.md    translations of README.md
skills/mind-meld/SKILL.md                  orchestrator — the only auto-triggering skill
skills/{microworld,quiz,socratic,feynman,five-whys,first-principles,short-essay}/SKILL.md
```

Eight skills, markdown only. `skills/mind-meld/SKILL.md` holds the canonical target-resolution
table, mode split, routing table, thresholds, report shape, and output locations; the seven tool
skills reference it (`../mind-meld/SKILL.md`) instead of restating those rules.

## The design, and why

- **Eight separate skill directories**, not one skill with modes. The seven tools are individually
  invocable (`/microworld src/x.ts`), but all carry `disable-model-invocation: true` — automatic
  routing is the orchestrator's monopoly, so a request for an explanation is never ambushed by a
  Socratic dialogue. No name prefixes: Claude namespaces plugin skills as `mind-meld:socratic`, and
  the other hosts assume one suite per user.
- **Fixed pipeline**: microworld → wait for the human → quiz → one deep tool (two only if two axes
  broke) → short-essay → pass or loop. The orchestrator's discretion is which deep tool, not which
  order.
- **Quiz locates, essay measures.** A quiz cannot probe Why or Risk, so it only tags the weak axis
  and routes; a perfect quiz skips the deep tool. Pass/fail belongs to `short-essay` alone.
- **One essay prompt** ("explain this to a colleague, from memory"), never split per axis: a form
  gets filled in, an explanation gets constructed, and the axis the human omits is itself the
  finding.
- **Floor is 8/10 on every axis.** Concept mode is the default: a single score, no forced template
  or required report — follow the knowledge. Change mode (a diff) adds the axes What / Why / Risk.
- **Loop caps**: 2 failed revisions switch the deep tool; 2 more failures end the session. Four
  explanations that did not land is evidence the target is unclear, so the output becomes questions
  for whoever produced the target, not a fifth explanation.
- **Stateless.** No scores remembered between sessions — the dependency was not worth the memory.
- **Output** goes to `.mind-meld/`, registered in `.git/info/exclude`, never the project's
  `.gitignore`: the working tree must stay clean. Reports are never posted or sent anywhere; the
  human sends them, and whatever the human decides on top of the understanding is theirs — this
  suite measures comprehension and stops.
- **No argument** means whatever the conversation is about, else ask — not the working diff.
- **Large targets**: read the core, skip generated/lock/vendored/test churn, and list every
  exclusion in the report.
- **Ambiguous targets** (`main`, `cache`) get one confirmation line, then proceed.
- **Deliberately absent**: microworld fidelity verification (owner's call — the known risk is a human
  passing while confidently wrong; add `file:line` provenance or a verification pass if it
  misfires), scripts, CI, tests, a tool registry for an eighth tool, agent-session-log input.

## Conventions

- Every `SKILL.md` is **English**, no exceptions. Sessions speak the user's language at runtime —
  grading an essay in a second language measures writing, not understanding.
- `README.md` is the English source of truth; `docs/i18n/*` are hand-maintained translations. A
  change to the README's install blocks or pipeline description goes into all seven files.
- No scripts, no dependencies, no build, no CI. Frontmatter typos surface the moment a host fails to
  load a skill. Verify ad hoc (name matches directory, description length, `disable-model-invocation`
  present on the seven tools) with a throwaway script — do not commit one.
- Supported hosts are Claude Code (`/plugin marketplace add songsnim/mind-meld`), Codex
  (`~/.codex/skills/`), and opencode (`~/.config/opencode/skills/`) — the three whose skill
  discovery paths are verified. Install parity across them is a hard constraint: all three read the
  same Agent Skills standard, so one copy of each SKILL.md serves all of them, and anything that
  breaks that (a runtime, a package manager) is off the table. Other hosts reading the same standard
  work by copying a block, but are not claimed until their path is confirmed.
- Skill `description` fields lead with knowledge- and concept-shaped triggers; a code change appears
  as one target among many, never as the framing. Review- or approval-only wording would hide the
  suite from most of its uses.

## Relationship to other repos

Separate from `songsnim/skills` (`songsnim-skills`: branching, pr, land, explain-diff,
mental-alignment) by design — that repo is the git workflow harness, this one is comprehension. Do
not fold mind-meld into its marketplace, and do not import from `mental-alignment`, whose HTML +
quiz + drill flow was the ancestor of this pipeline.
