<p align="center">
  <img src="../../assets/hero.png" width="220" alt="mind-meld">
</p>

<h1 align="center">mind-meld</h1>

<p align="center">
  <strong><em>把另一个心智接到你的心智上。信任之前，先看懂它。</em></strong>
</p>

<p align="center">
  <sub>一套用来真正理解陌生知识的工具：概念、领域专业知识、算法、库、系统、设计决策或代码变更都可以作为对象，而不是停留在摘要留下的“好像懂了”的印象上。</sub>
</p>

<p align="center">
  <sub><a href="../../README.md">English</a> &middot; <a href="README.ko.md">한국어</a> &middot; <a href="README.ja.md">日本語</a> &middot; <a href="README.es.md">Español</a> &middot; <a href="README.pt.md">Português</a> &middot; <a href="README.ru.md">Русский</a></sub>
</p>

---

读一段解释，只会产生“懂了”的错觉，而不是真正的理解。mind-meld 用测量来弥合这段差距：它构建一个可以探索的世界，用小测定位弱点，深入钻研弱点，再给你自己的解释打分，直到它站得住。名字来自[瓦肯人的心灵融合](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld)：一条通往另一个心智的路——专家的、作者的、智能体的。

## 两种用法

**轨道一——完整会话。** 把想理解的对象交给编排器，它会跑完整个流程。

```
/mind-meld "consistent hashing"
/mind-meld src/scheduler.ts
/mind-meld #42
```

**轨道二——按需用一个工具。** 直接调用工具，对象照原样写上：概念、模块、算法、论文、刚读到的一句话都行。

```
/microworld "consistent hashing"
/socratic src/scheduler.ts
/five-whys "为什么这个 repo 要 pin 住每个版本"
/first-principles "vector clocks"
```

轨道一是带及格线的测量流水线。轨道二是一个工具，想用多久用多久。
只有编排器会替你选工具；在轨道二里由你自己选。

## 轨道一：完整会话

```
/mind-meld "consistent hashing"
```

1. **microworld** —— 一个体现机制本身、而不是摘要的交互式 HTML 世界。你来探索，会话等待。
2. **quiz** —— 少量有确定答案的问题，用来定位你漏掉了什么。它不判定及格与否。
3. **一个深挖工具** —— 根据漏掉的地方，从 `feynman`、`five-whys`、`socratic`、`first-principles` 中选一个。
4. **short-essay** —— 凭记忆向同事解释。概念给一个分数；代码变更按三个维度评分：
   改了**什么**、**为什么**这样做、**什么可能出问题**。
5. **每个维度 8/10 以上即通过**，否则修改。修改两次仍失败就换一个深挖工具；四次失败则结束会话并如实说明——
   这说明对象本身不清楚，而不是你慢。

如果是代码变更，会输出 `.mind-meld/<对象>-report.md`：分数、始终不清楚的地方，以及要发回给产出者的问题。
如果是概念，报告可选。不会替你发送；基于理解做出什么决定，由你自己决定。

对象可以是概念、路径、PR 号、分支或 commit range。不带参数时，以当前对话的主题为对象。

## 轨道二：任意工具，任意对象

不评分，也没有固定顺序。按你卡在哪里来挑：

| 卡在哪里 | 调用 |
| --- | --- |
| 想不出它是怎么跑的 | `/microworld <对象>` |
| 想知道自己漏了什么 | `/quiz <对象>` |
| 说不出什么会坏 | `/socratic <对象>` |
| 好像懂了但讲不明白 | `/feynman <对象>` |
| 不明白为什么这么做 | `/five-whys <对象>` |
| 术语本身就陌生 | `/first-principles <对象>` |
| 想给自己的理解打个分 | `/short-essay <对象>` |

参数是自由文本。`/microworld "CRDT merge"` 和 `/microworld src/merge.ts` 都有效。

## 安装

只复制你所用智能体对应的那一段。

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

更新用 `git -C ~/.mind-meld pull`，符号链接会自动跟上。Claude Code 通过 marketplace 更新。

## 内容

一共八个技能：`mind-meld` 加上它负责路由的七个工具 —— `microworld`、`quiz`、`socratic`、`feynman`、
`five-whys`、`first-principles`、`short-essay`。只有 `mind-meld` 会自动触发。其余七个只接受显式调用，
所以你要一段解释时，不会突然被拉进苏格拉底问答。

## 说明

- 无状态。不跨会话记忆分数。
- 输出写入 `.mind-meld/`，并登记到 `.git/info/exclude`，工作区保持干净。
- 会话使用你的语言。用第二语言写的小论文，评的是写作而不是理解。
- 没有脚本、没有依赖、无需构建。只有八个 `SKILL.md`。

[MIT](../../LICENSE).
