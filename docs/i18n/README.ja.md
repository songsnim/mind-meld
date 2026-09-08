<p align="center">
  <img src="../../assets/hero.png" width="220" alt="mind-meld">
</p>

<h1 align="center">mind-meld</h1>

<p align="center">
  <strong><em>エージェントの心をあなたの心へ。信頼する前に理解する。</em></strong>
</p>

<p align="center">
  <sub>エージェントがコードを書く過程で持ち込んだ、馴染みのない概念・知識・設計判断を、信頼する前に理解するためのツール群です。最も出番が多いのはエージェントが開いたプルリクエストですが、対象は任意のモジュール、アルゴリズム、ライブラリ、アーキテクチャ上の判断、あるいは概念そのものでも構いません。</sub>
</p>

<p align="center">
  <sub><a href="../../README.md">English</a> &middot; <a href="README.ko.md">한국어</a> &middot; <a href="README.zh.md">中文</a> &middot; <a href="README.es.md">Español</a> &middot; <a href="README.pt.md">Português</a> &middot; <a href="README.ru.md">Русский</a></sub>
</p>

---

エージェントは人間が読める速度より速く出力します。レビューのボトルネックは承認操作ではなく、何を承認しているのかを理解することです。名前は[バルカンの精神融合](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld)から取りました。エージェントの頭の中へ入る道です。

## 使い方は2通り

**トラック1 — レビューすべき PR がある場合。** オーケストレータを呼べば、ワークフロー全体が回ります。

```
/mind-meld #42
```

**トラック2 — それ以外、理解できないものすべて。** ツールを直接呼び、対象をそのまま書きます。概念、
モジュール、アルゴリズム、論文、いま読んだ一文、何でも構いません。

```
/microworld "consistent hashing"
/socratic src/scheduler.ts
/five-whys "なぜこの repo は全バージョンを pin するのか"
/first-principles "vector clocks"
```

トラック1 は合格ラインのある測定型パイプラインです。トラック2 は必要なときに好きなだけ使うツール1つです。
ツールを選ぶのはオーケストレータだけで、トラック2 では人が選びます。

## トラック1: PR のレビュー

```
/mind-meld #42
```

1. **microworld** — 変更の要約ではなく、仕組みそのものを体現したインタラクティブな HTML の世界。人が
   探索し、セッションは待ちます。
2. **quiz** — 答えが一意に定まる少数の問いで、抜けている箇所を特定します。合否は付けません。
3. **深いツール1つ** — 抜けた軸に応じて `feynman`、`five-whys`、`socratic`、`first-principles` から選択。
4. **short-essay** — 記憶だけを頼りに同僚へ説明する。3つの軸で採点します: **何が**変わったか、**なぜ**
   この方法か、**何が壊れ**得るか。
5. **全軸 8/10 以上で通過**、届かなければ改稿。改稿2回失敗で別の深いツールに交代し、4回失敗ならセッション
   を終えてそう報告します。人が遅いのではなく、変更が不明瞭だという証拠です。

成果物は `.mind-meld/<対象>-report.md`: 各軸のスコア、最後まで不明瞭だった点、そしてエージェントに投げ返す
質問。自動投稿はしません。承認するのは人で、mind-meld ではありません。

ブランチ、commit range、パス、あるいは引数なし(現在の作業 diff)でも、PR 番号と同じように動きます。

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
- 出力は `.mind-meld/` へ。`.git/info/exclude` に登録するので、レビュー対象の diff を汚しません。
- セッションは利用者の言語で進みます。第二言語で書いた小論文の採点は、理解度ではなく作文力の測定です。
- スクリプト・依存・ビルドなし。`SKILL.md` 8枚だけです。

[MIT](../../LICENSE).
