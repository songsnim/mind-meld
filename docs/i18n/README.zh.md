# mind-meld

一套用来在信任之前，先真正理解智能体写代码时引入的陌生概念、知识与设计决策的工具集。它最常派上用场的场景
是智能体刚提交的 Pull Request，但目标也可以是任意模块、算法、库、架构决策，或某个概念本身。

智能体产出的速度快于人类阅读的速度。评审的瓶颈不在于点下批准，而在于理解你到底批准了什么。名字取自
[瓦肯人的心灵融合](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld) —— 一条进入智能体头脑的路。

## 一次会话怎么走

```
/mind-meld 42
```

1. **microworld** —— 不是变更摘要，而是把机制本身实现出来的交互式 HTML 世界。你去探索，会话在等你。
2. **quiz** —— 少量答案确定的问题，用来定位你漏掉的地方。它不判定通过与否。
3. **一个深度工具** —— 依据漏掉的维度，在 `feynman`、`five-whys`、`socratic`、`first-principles` 中选择。
4. **short-essay** —— 凭记忆向同事解释。按三个维度评分：**改了什么**、**为什么这样做**、**什么会坏**。
5. **每个维度都达到 8/10 才算通过**，否则修改。两次修改仍不达标就换一个深度工具；四次失败则结束会话并
   如实说明 —— 这是变更本身不清晰的证据，而不是你慢。

产物是 `.mind-meld/<目标>-report.md`：各维度分数、始终没弄清的点，以及要抛回给智能体的问题。不会自动
发布。批准由人来做，mind-meld 不做。

每个工具也可以单独调用。

```
/microworld src/scheduler.ts
/five-whys 42
/first-principles "vector clocks"
```

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

更新用 `git -C ~/.mind-meld pull`，符号链接会自动跟上。Claude Code 通过 marketplace 更新。

## 内容

| 技能 | 作用 |
| --- | --- |
| `mind-meld` | 编排器，负责在其余技能之间路由。 |
| `microworld` | 把机制实现出来的交互式 HTML 世界。 |
| `quiz` | 少量确定性问题，定位缺口。 |
| `socratic` | 一次一问，直到你自己看见什么会坏。 |
| `feynman` | 让你用平实语言解释，标出含糊之处。 |
| `five-whys` | 一路下探到迫使该决策成立的约束。 |
| `first-principles` | 从最基本的前提重建陌生的概念。 |
| `short-essay` | 测量仪器。评分，并修改到达标为止。 |

只有 `mind-meld` 会自动触发。其余七个只接受显式调用，所以你要一段解释时，不会突然被拉进苏格拉底问答。

## 说明

- 无状态。不跨会话记忆分数。
- 输出写入 `.mind-meld/`，并登记到 `.git/info/exclude` —— 正在评审的 diff 保持干净。
- 会话使用你的语言。用第二语言写的小论文，评的是写作而不是理解。
- 没有脚本、没有依赖、无需构建。只有八个 `SKILL.md`。

MIT.
