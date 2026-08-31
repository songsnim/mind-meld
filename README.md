<p align="center">
  <img src="assets/hero.png" width="220" alt="mind-meld, a way into the agent's head">
</p>

<h1 align="center">mind-meld</h1>

<p align="center">
  <strong><em>The agent's mind to your mind. Understand the PR before you approve it.</em></strong>
</p>

<p align="center">
  <sub>A tool suite for understanding the unfamiliar concepts, knowledge, and design decisions an agent pulls in while it writes code, before you trust them. Its most frequent venue is the pull request an agent just opened, but the target can be any module, algorithm, library, architectural decision, or bare concept.</sub>
</p>

<p align="center">
  <sub><a href="docs/i18n/README.ko.md">한국어</a> &middot; <a href="docs/i18n/README.zh.md">中文</a> &middot; <a href="docs/i18n/README.ja.md">日本語</a> &middot; <a href="docs/i18n/README.es.md">Español</a> &middot; <a href="docs/i18n/README.pt.md">Português</a> &middot; <a href="docs/i18n/README.ru.md">Русский</a></sub>
</p>

---

Agents ship faster than humans can read. The review bottleneck is not typing an approval, it is understanding what you are approving. mind-meld is the [Vulcan mind meld](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld): a way into the agent's head.

## Two ways to use it

**Track 1 — a PR to review.** Call the orchestrator; it runs the whole workflow.

```
/mind-meld #42
```

**Track 2 — anything else you do not understand.** Call a tool directly with whatever it is: a
concept, a module, an algorithm, a paper, a sentence you read.

```
/microworld "consistent hashing"
/socratic src/scheduler.ts
/five-whys "why does this repo pin every version"
/first-principles "vector clocks"
```

Track 1 is a measured pipeline with a pass mark. Track 2 is one tool, on demand, for as long as you
want it. Only the orchestrator picks tools for you; in track 2 you pick.

## Track 1: reviewing a PR

```
/mind-meld #42
```

1. **Microworld** — an interactive HTML world that embodies the mechanism, not a summary of it. You
   explore it. The session waits.
2. **Quiz** — a few questions with determinate answers, to locate what you missed. It does not pass
   or fail you.
3. **One deep tool** — `feynman`, `five-whys`, `socratic`, or `first-principles`, chosen by which
   axis you missed.
4. **Short essay** — explain it to a colleague, from memory. Graded on three axes: **What** changed,
   **Why** this way, **What can break**.
5. **Pass at 8/10 on every axis**, or revise. Two failed revisions switch the deep tool; four
   failures end the session and say so — that is evidence the change is unclear, not that you are.

Out comes `.mind-meld/<target>-report.md`: the scores, what stayed unclear, and the questions to send
back to the agent. Nothing is posted for you. You approve, mind-meld does not.

A branch, a commit range, a path, or no argument at all (the working diff) works the same way as a PR
number.

## Track 2: any tool, on anything

Nothing is graded and nothing is required. Pick by what you are stuck on:

| Stuck on | Call |
| --- | --- |
| I cannot picture how it behaves | `/microworld <thing>` |
| I want to know what I missed | `/quiz <thing>` |
| I cannot say what would break | `/socratic <thing>` |
| I think I get it but cannot say it simply | `/feynman <thing>` |
| I do not see why it was done this way | `/five-whys <thing>` |
| The vocabulary itself is new | `/first-principles <thing>` |
| I want my understanding scored | `/short-essay <thing>` |

The argument is free text. `/microworld "CRDT merge"` and `/microworld src/merge.ts` are both valid.

## Install

Pick the block for the agent you use.

**Claude Code**

```
/plugin marketplace add songsnim/mind-meld
/plugin install mind-meld@mind-meld
```

**Codex CLI**

```sh
git clone https://github.com/songsnim/mind-meld ~/.mind-meld
mkdir -p ~/.codex/skills
ln -sfn ~/.mind-meld/skills/* ~/.codex/skills/
```

**opencode**

```sh
git clone https://github.com/songsnim/mind-meld ~/.mind-meld
mkdir -p ~/.config/opencode/skills
ln -sfn ~/.mind-meld/skills/* ~/.config/opencode/skills/
```

Update with `git -C ~/.mind-meld pull` — the symlinks follow. Claude Code updates through the
marketplace.

## What is in it

Eight skills: `mind-meld` plus the seven tools it routes between — `microworld`, `quiz`, `socratic`,
`feynman`, `five-whys`, `first-principles`, `short-essay`. Only `mind-meld` auto-triggers; the seven
are explicit-invocation only, so asking for an explanation never gets ambushed by a Socratic
dialogue.

## Notes

- Stateless. No scores are remembered between sessions.
- Output goes to `.mind-meld/`, added to `.git/info/exclude` — the diff under review stays clean.
- The session speaks your language; grading an essay in a second language measures writing, not
  understanding.
- No scripts, no dependencies, no build. Eight `SKILL.md` files.

[MIT](LICENSE).
