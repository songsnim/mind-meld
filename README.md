<p align="center">
  <img src="assets/hero.png" width="220" alt="mind-meld, a way into the agent's head">
</p>

<h1 align="center">mind-meld</h1>

<p align="center">
  <em>The agent already understands it. Now you do.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/github/stars/songsnim/mind-meld?style=flat-square&color=111111&label=stars" alt="Stars">
  <img src="https://img.shields.io/badge/skills-8-111111?style=flat-square" alt="8 skills">
  <img src="https://img.shields.io/badge/works%20with-5%20agents-111111?style=flat-square" alt="Works with 5 agents">
  <img src="https://img.shields.io/badge/dependencies-0-111111?style=flat-square" alt="Zero dependencies">
  <img src="https://img.shields.io/badge/license-MIT-111111?style=flat-square" alt="MIT license">
</p>

<p align="center">
  <strong>Understand the PR before you approve it &middot; measured, not assumed</strong><br>
  <sub>Eight skills that build an interactive world out of the change, quiz you on it, drill the part you missed, and grade your own explanation until it holds at 8/10 on <em>what changed</em>, <em>why this way</em>, and <em>what can break</em>. Markdown only — no scripts, no dependencies, no build.</sub>
</p>

<p align="center">
  <sub><a href="docs/i18n/README.ko.md">한국어</a> &middot; <a href="docs/i18n/README.zh.md">中文</a> &middot; <a href="docs/i18n/README.ja.md">日本語</a> &middot; <a href="docs/i18n/README.es.md">Español</a> &middot; <a href="docs/i18n/README.pt.md">Português</a> &middot; <a href="docs/i18n/README.ru.md">Русский</a></sub>
</p>

---

A tool suite for understanding the unfamiliar concepts, knowledge, and design decisions an agent
pulls in while it writes code — before you trust them. Its most frequent venue is the pull request an
agent just opened, but the target can be any module, algorithm, library, architectural decision, or
bare concept.

Agents ship faster than humans can read. The review bottleneck is not typing an approval, it is
understanding what you are approving. mind-meld is the [Vulcan mind
meld](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld): a way into the agent's head.

## How a session runs

```
/mind-meld 42
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

Any tool can also be called on its own:

```
/microworld src/scheduler.ts
/five-whys 42
/first-principles "vector clocks"
```

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

**Cursor**

```sh
git clone https://github.com/songsnim/mind-meld ~/.mind-meld
mkdir -p ~/.cursor/skills
ln -sfn ~/.mind-meld/skills/* ~/.cursor/skills/
```

**Hermes**

```sh
git clone https://github.com/songsnim/mind-meld ~/.mind-meld
mkdir -p ~/.hermes/skills
ln -sfn ~/.mind-meld/skills/* ~/.hermes/skills/
```

Update with `git -C ~/.mind-meld pull` — the symlinks follow. Claude Code updates through the
marketplace.

## What is in it

| Skill | What it does |
| --- | --- |
| `mind-meld` | The orchestrator. Routes between the rest. |
| `microworld` | Interactive HTML world embodying the mechanism. |
| `quiz` | Few determinate questions; locates the gap. |
| `socratic` | One question at a time, until you see what breaks. |
| `feynman` | Explain it plainly; the vague spots get marked. |
| `five-whys` | Down to the constraint that forced the decision. |
| `first-principles` | Rebuild an unfamiliar idea from its primitives. |
| `short-essay` | The measuring instrument. Graded, revised until it holds. |

Only `mind-meld` auto-triggers; the seven tools are invoked explicitly, so a request for an
explanation never gets ambushed by a Socratic dialogue.

## Notes

- Stateless. No scores are remembered between sessions.
- Output goes to `.mind-meld/`, added to `.git/info/exclude` — the diff under review stays clean.
- The session speaks your language; grading an essay in a second language measures writing, not
  understanding.
- No scripts, no dependencies, no build. Eight `SKILL.md` files.

MIT.
