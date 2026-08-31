# CLAUDE.md

## What this repo is

`mind-meld` is a tool suite of Agent Skills that makes a human actually understand the unfamiliar
concepts, knowledge, and design decisions an agent pulled in while writing code — before they trust
it. The most frequent venue is reviewing a PR an agent just opened; the target is not limited to PRs
(modules, algorithms, libraries, architectural decisions, bare concepts all qualify).

The problem it attacks: agents ship faster than humans read, so the review bottleneck is
comprehension, not approval. Summaries do not fix it — reading a summary produces the impression of
understanding. So the loop is the product: build a world, quiz, drill, then **measure** the human's
own explanation and repeat while it sits below the floor.

Named after Star Trek's Vulcan mind meld — a way into the agent's head.

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
- **Floor is 8/10 on every axis.** Change mode axes are What / Why / Risk; concept mode is a single
  score, no forced template or required report — follow the knowledge.
- **Loop caps**: 2 failed revisions switch the deep tool; 2 more failures end the session. Four
  explanations that did not land is evidence the target is unclear, so the output becomes questions
  for the agent, not a fifth explanation.
- **Stateless.** No scores remembered between sessions — the dependency was not worth the memory.
- **Output** goes to `.mind-meld/`, registered in `.git/info/exclude`, never the reviewed project's
  `.gitignore`: the diff under review must stay clean. Reports are never posted as PR comments; the
  human sends them, and the human approves — this suite reports comprehension and stops.
- **Large targets**: read the core change, skip generated/lock/vendored/test churn, and list every
  exclusion in the report. Telling a reviewer to split an already-opened PR is not actionable.
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
- Install parity across five hosts is a hard constraint: Claude Code (`/plugin marketplace add
  songsnim/mind-meld`), Codex `~/.codex/skills/`, opencode `~/.config/opencode/skills/`, Cursor
  `~/.cursor/skills/`, Hermes `~/.hermes/skills/`. All five read the same Agent Skills standard, so
  one copy of each SKILL.md serves all of them — anything that breaks that (a runtime, a package
  manager) is off the table.
- Skill `description` fields carry both PR-shaped and concept-shaped triggers. PR-only wording would
  hide the suite from half its uses.

## Relationship to other repos

Separate from `songsnim/skills` (`songsnim-skills`: branching, pr, land, explain-diff,
mental-alignment) by design — that repo is the git workflow harness, this one is comprehension. Do
not fold mind-meld into its marketplace, and do not import from `mental-alignment`, whose HTML +
quiz + drill flow was the ancestor of this pipeline.
