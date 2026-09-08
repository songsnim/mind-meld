<p align="center">
  <img src="../../assets/hero.png" width="220" alt="mind-meld">
</p>

<h1 align="center">mind-meld</h1>

<p align="center">
  <strong><em>把智能体的心思接到你的心思上。信任之前，先看懂它。</em></strong>
</p>

<p align="center">
  <sub>一套用来在信任之前，先真正理解智能体写代码时引入的陌生概念、知识与设计决策的工具集。它最常派上用场的场景是智能体刚提交的 Pull Request，但目标也可以是任意模块、算法、库、架构决策，或某个概念本身。</sub>
</p>

<p align="center">
  <sub><a href="../../README.md">English</a> &middot; <a href="README.ko.md">한국어</a> &middot; <a href="README.ja.md">日本語</a> &middot; <a href="README.es.md">Español</a> &middot; <a href="README.pt.md">Português</a> &middot; <a href="README.ru.md">Русский</a></sub>
</p>

---

智能体产出的速度快于人类阅读的速度。评审的瓶颈不在于点下批准，而在于理解你到底批准了什么。名字取自[瓦肯人的心灵融合](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld)，一条进入智能体头脑的路。

## 两种用法

**轨道一 —— 有一个待评审的 PR。** 调用编排器，它会跑完整个流程。

```
/mind-meld #42
```

**轨道二 —— 其他任何你没看懂的东西。** 直接调用某个工具，把对象原样写上：概念、模块、算法、论文、刚读到
的一句话，都可以。

```
/microworld "consistent hashing"
/socratic src/scheduler.ts
/five-whys "为什么这个 repo 要 pin 住每个版本"
/first-principles "vector clocks"
```

轨道一是有通过线的测量式流程。轨道二是随手取用、想用多久就用多久的单个工具。只有编排器会替你挑工具，
轨道二里由你自己挑。

## 轨道一：评审 PR

```
/mind-meld #42
```

1. **microworld** —— 不是变更摘要，而是把机制本身实现出来的交互式 HTML 世界。你去探索，会话在等你。
2. **quiz** —— 少量答案确定的问题，用来定位你漏掉的地方。它不判定通过与否。
3. **一个深度工具** —— 依据漏掉的维度，在 `feynman`、`five-whys`、`socratic`、`first-principles` 中选择。
4. **short-essay** —— 凭记忆向同事解释。按三个维度评分：**改了什么**、**为什么这样做**、**什么会坏**。
5. **每个维度都达到 8/10 才算通过**，否则修改。两次修改仍不达标就换一个深度工具；四次失败则结束会话并
   如实说明 —— 这是变更本身不清晰的证据，而不是你慢。

产物是 `.mind-meld/<目标>-report.md`：各维度分数、始终没弄清的点，以及要抛回给智能体的问题。不会自动
发布。批准由人来做，mind-meld 不做。

分支、commit range、路径，或者不带参数（当前工作区 diff），用法与 PR 号完全相同。

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
- 输出写入 `.mind-meld/`，并登记到 `.git/info/exclude`，正在评审的 diff 保持干净。
- 会话使用你的语言。用第二语言写的小论文，评的是写作而不是理解。
- 没有脚本、没有依赖、无需构建。只有八个 `SKILL.md`。

[MIT](../../LICENSE).
