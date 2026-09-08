<p align="center">
  <img src="../../assets/hero.png" width="220" alt="mind-meld">
</p>

<h1 align="center">mind-meld</h1>

<p align="center">
  <strong><em>A mente do agente para a sua mente. Entenda antes de confiar.</em></strong>
</p>

<p align="center">
  <sub>Um conjunto de ferramentas para entender os conceitos, conhecimentos e decisões de projeto pouco familiares que um agente traz enquanto escreve código, antes de confiar neles. Seu palco mais frequente é o pull request que o agente acabou de abrir, mas o alvo pode ser qualquer módulo, algoritmo, biblioteca, decisão arquitetural ou conceito em si.</sub>
</p>

<p align="center">
  <sub><a href="../../README.md">English</a> &middot; <a href="README.ko.md">한국어</a> &middot; <a href="README.zh.md">中文</a> &middot; <a href="README.ja.md">日本語</a> &middot; <a href="README.es.md">Español</a> &middot; <a href="README.ru.md">Русский</a></sub>
</p>

---

Agentes produzem mais rápido do que um humano lê. O gargalo da revisão não é clicar em aprovar, é entender o que você está aprovando. O nome vem da [fusão mental vulcana](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld): um caminho para dentro da cabeça do agente.

## Duas formas de usar

**Trilha 1: há um PR para revisar.** Chame o orquestrador e ele roda todo o fluxo.

```
/mind-meld #42
```

**Trilha 2: qualquer outra coisa que você não entendeu.** Chame uma ferramenta direto com o que for:
um conceito, um módulo, um algoritmo, um paper, uma frase que você acabou de ler.

```
/microworld "consistent hashing"
/socratic src/scheduler.ts
/five-whys "por que este repo fixa todas as versões"
/first-principles "vector clocks"
```

A trilha 1 é um processo medido, com nota de corte. A trilha 2 é uma ferramenta só, quando você
quiser e pelo tempo que quiser. Só o orquestrador escolhe ferramentas por você; na trilha 2 você
escolhe.

## Trilha 1: revisar um PR

```
/mind-meld #42
```

1. **microworld** — um mundo HTML interativo que encarna o mecanismo, não um resumo da mudança. Você
   explora; a sessão espera.
2. **quiz** — poucas perguntas de resposta determinada, para localizar o que passou. Não aprova nem
   reprova.
3. **Uma ferramenta profunda** — `feynman`, `five-whys`, `socratic` ou `first-principles`, conforme o
   eixo que falhou.
4. **short-essay** — explique a um colega, de memória. Avaliado em três eixos: **o que** mudou,
   **por que** desse jeito, **o que pode quebrar**.
5. **Passa com 8/10 em todos os eixos**; abaixo disso, revisa. Duas revisões falhas trocam a
   ferramenta profunda; quatro falhas encerram a sessão e dizem isso — é evidência de que a mudança
   está obscura, não de que você é lento.

A saída é `.mind-meld/<alvo>-report.md`: as notas, o que ficou obscuro e as perguntas para devolver
ao agente. Nada é publicado por você. A aprovação é sua; mind-meld não aprova.

Um branch, um intervalo de commits, um caminho, ou nenhum argumento (o diff de trabalho) funcionam
igual a um número de PR.

## Trilha 2: qualquer ferramenta, sobre qualquer coisa

Sem nota e sem ordem obrigatória. Escolha pelo que travou:

| Travou em | Chamada |
| --- | --- |
| Não consigo imaginar como aquilo se comporta | `/microworld <coisa>` |
| Quero saber o que me passou | `/quiz <coisa>` |
| Não sei dizer o que quebraria | `/socratic <coisa>` |
| Acho que entendi, mas não sei explicar simples | `/feynman <coisa>` |
| Não vejo por que foi feito assim | `/five-whys <coisa>` |
| O próprio vocabulário é novo | `/first-principles <coisa>` |
| Quero minha compreensão pontuada | `/short-essay <coisa>` |

O argumento é texto livre. `/microworld "CRDT merge"` e `/microworld src/merge.ts` são ambos válidos.

## Instalação

Copie só o bloco do agente que você usa.

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

Atualize com `git -C ~/.mind-meld pull` — os symlinks acompanham. O Claude Code atualiza pelo
marketplace.

## O que tem dentro

Oito skills: `mind-meld` mais as sete ferramentas que ele roteia — `microworld`, `quiz`, `socratic`,
`feynman`, `five-whys`, `first-principles`, `short-essay`. Só `mind-meld` dispara sozinho; as outras
sete são de chamada explícita, então pedir uma explicação nunca vira um diálogo socrático de
surpresa.

## Notas

- Sem estado. Não guarda notas entre sessões.
- A saída vai para `.mind-meld/`, incluído em `.git/info/exclude` — o diff em revisão fica limpo.
- A sessão fala a sua língua. Avaliar um texto em segunda língua mede redação, não compreensão.
- Sem scripts, sem dependências, sem build. Oito arquivos `SKILL.md`.

[MIT](../../LICENSE).
