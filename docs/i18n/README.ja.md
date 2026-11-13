<p align="center">
  <img src="../../assets/hero.png" width="220" alt="mind-meld">
</p>

<h1 align="center">mind-meld</h1>

<p align="center">
  <strong><em>誰かの心をあなたの心へ。信頼する前に理解する。</em></strong>
</p>

<p align="center">
  <sub>馴染みのない知識を本当に理解するためのツール群です。概念、分野の専門知識、アルゴリズム、ライブラリ、システム、設計判断、コード変更のどれでも対象になります。要約が残す「わかった気」で終わらせません。</sub>
</p>

<p align="center">
  <sub><a href="../../README.md">English</a> &middot; <a href="README.ko.md">한국어</a> &middot; <a href="README.zh.md">中文</a> &middot; <a href="README.es.md">Español</a> &middot; <a href="README.pt.md">Português</a> &middot; <a href="README.ru.md">Русский</a></sub>
</p>

---

説明を読むと、わかった気にはなりますが、理解そのものは生まれません。mind-meld はその差を測ることで埋めます。探索できる世界を作り、クイズで弱点を見つけ、そこを掘り下げ、あなた自身の説明が基準を超えるまで採点します。名前は[ヴァルカンのマインド・メルド](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld)から。専門家でも、作者でも、エージェントでも、誰かの頭の中に入る道です。

## 使い方は2通り

**トラック1 — フルセッション。** 理解したい対象をオーケストレーターに渡すと、ワークフロー全体が走ります。

```
/mind-meld "consistent hashing"
/mind-meld src/scheduler.ts
/mind-meld #42
```

**トラック2 — 必要なときにツールを1つ。** ツールを直接呼び、対象をそのまま書きます。概念、モジュール、
アルゴリズム、論文、さっき読んだ一文、何でも構いません。

```
/microworld "consistent hashing"
/socratic src/scheduler.ts
/five-whys "なぜこの repo は全バージョンを pin するのか"
/first-principles "vector clocks"
```

トラック1は合格ラインのある計測型パイプラインです。トラック2は好きなだけ使えるツール1つです。
ツールを選んでくれるのはオーケストレーターだけで、トラック2では自分で選びます。

## トラック1: フルセッション

```
/mind-meld "consistent hashing"
```

1. **microworld** — 対象の要約ではなく、メカニズムそのものを体現したインタラクティブな HTML の世界。
   あなたが探索し、セッションは待ちます。
2. **quiz** — 答えの確定した少数の質問で、見落としを特定します。合否は判定しません。
3. **深掘りツール1つ** — 見落とした点に応じて `feynman`、`five-whys`、`socratic`、`first-principles` から選択。
4. **short-essay** — 記憶だけで同僚に説明する。概念は1つのスコアで、コード変更は3軸で採点します:
   **何が**変わったか、**なぜ**この方法か、**何が壊れうる**か。
5. **全軸 8/10 以上で合格**、そうでなければ書き直し。書き直し2回失敗で深掘りツールを交代し、4回失敗で
   セッションを終えてそう報告します。あなたが遅いのではなく、対象が不明瞭だという証拠です。

コード変更なら `.mind-meld/<対象>-report.md` が出力されます: スコア、最後まで不明瞭だった点、そして
それを作った側に送り返す質問。概念ならレポートは任意です。自動では送らず、理解の上で何を決めるかは
あなたのものです。

対象は概念、パス、PR 番号、ブランチ、commit range のどれでも構いません。引数なしなら、いまの会話の
話題を対象にします。

## トラック2: どのツールでも、どんな対象にも

採点もなく、決まった順序もありません。何に詰まっているかで選んでください。

| 詰まっている点 | 呼び出し |
| --- | --- |
| どう動くのか像が結べない | `/microworld <対象>` |
| 自分が何を見落としたか知りたい | `/quiz <対象>` |
| 何が壊れるか言えない | `/socratic <対象>` |
| 分かった気はするが平易に説明できない | `/feynman <対象>` |
| なぜこの方法なのか分からない | `/five-whys <対象>` |
| 用語そのものが馴染みがない | `/first-principles <対象>` |
| 自分の理解度を点数で見たい | `/short-essay <対象>` |

引数は自由テキストです。`/microworld "CRDT merge"` も `/microworld src/merge.ts` も有効です。

## インストール

使っているエージェントのブロックだけコピーしてください。

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

更新は `git -C ~/.mind-meld pull` — symlink が追随します。Claude Code は marketplace 経由で更新します。

## 中身

スキルは8つ: `mind-meld` と、それが振り分ける7つのツール — `microworld`、`quiz`、`socratic`、
`feynman`、`five-whys`、`first-principles`、`short-essay`。自動起動するのは `mind-meld` だけです。残る
7つは明示呼び出し専用なので、説明を頼んだら突然ソクラテス問答が始まる、ということは起きません。

## 注意

- 状態を持ちません。セッション間でスコアを覚えません。
- 出力は `.mind-meld/` へ。`.git/info/exclude` に登録するので、作業ツリーを汚しません。
- セッションは利用者の言語で進みます。第二言語で書いた小論文の採点は、理解度ではなく作文力の測定です。
- スクリプト・依存・ビルドなし。`SKILL.md` 8枚だけです。

[MIT](../../LICENSE).
