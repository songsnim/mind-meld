# mind-meld

エージェントがコードを書く過程で持ち込んだ、馴染みのない概念・知識・設計判断を、信頼する前に理解する
ためのツール群です。最も出番が多いのはエージェントが開いたプルリクエストですが、対象は任意のモジュール、
アルゴリズム、ライブラリ、アーキテクチャ上の判断、あるいは概念そのものでも構いません。

エージェントは人間が読める速度より速く出力します。レビューのボトルネックは承認操作ではなく、何を承認して
いるのかを理解することです。名前は[バルカンの精神融合](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld)
から取りました — エージェントの頭の中へ入る道です。

## セッションの流れ

```
/mind-meld 42
```

1. **microworld** — 変更の要約ではなく、仕組みそのものを体現したインタラクティブな HTML の世界。人が
   探索し、セッションは待ちます。
2. **quiz** — 答えが一意に定まる少数の問いで、抜けている箇所を特定します。合否は付けません。
3. **深いツール1つ** — 抜けた軸に応じて `feynman`、`five-whys`、`socratic`、`first-principles` から選択。
4. **short-essay** — 記憶だけを頼りに同僚へ説明する。3つの軸で採点します: **何が**変わったか、**なぜ**
   この方法か、**何が壊れ**得るか。
5. **全軸 8/10 以上で通過**、届かなければ改稿。改稿2回失敗で別の深いツールに交代し、4回失敗ならセッション
   を終えてそう報告します — 人が遅いのではなく、変更が不明瞭だという証拠です。

成果物は `.mind-meld/<対象>-report.md`: 各軸のスコア、最後まで不明瞭だった点、そしてエージェントに投げ返す
質問。自動投稿はしません。承認するのは人で、mind-meld ではありません。

各ツールは単独でも呼べます。

```
/microworld src/scheduler.ts
/five-whys 42
/first-principles "vector clocks"
```

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

更新は `git -C ~/.mind-meld pull` — symlink が追随します。Claude Code は marketplace 経由で更新します。

## 中身

| スキル | 役割 |
| --- | --- |
| `mind-meld` | オーケストレータ。残りを振り分けます。 |
| `microworld` | 仕組みを体現したインタラクティブ HTML の世界。 |
| `quiz` | 答えが定まる少数の問いで抜けを特定。 |
| `socratic` | 一度に一問。何が壊れるかを自分で見ることになります。 |
| `feynman` | 平易に説明させ、曖昧な箇所を印付けします。 |
| `five-whys` | 判断を強制した制約まで降りていきます。 |
| `first-principles` | 馴染みのない考えを primitive から組み直します。 |
| `short-essay` | 測定器。採点し、基準を越えるまで改稿させます。 |

自動起動するのは `mind-meld` だけです。残る7つは明示呼び出し専用なので、説明を頼んだら突然ソクラテス
問答が始まる、ということは起きません。

## 注意

- 状態を持ちません。セッション間でスコアを覚えません。
- 出力は `.mind-meld/` へ。`.git/info/exclude` に登録するので、レビュー対象の diff を汚しません。
- セッションは利用者の言語で進みます。第二言語で書いた小論文の採点は、理解度ではなく作文力の測定です。
- スクリプト・依存・ビルドなし。`SKILL.md` 8枚だけです。

MIT.
