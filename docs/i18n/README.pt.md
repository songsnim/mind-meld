<p align="center">
  <img src="../../assets/hero.png" width="220" alt="mind-meld">
</p>

<h1 align="center">mind-meld</h1>

<p align="center">
  <strong><em>Outra mente para a sua mente. Entenda antes de confiar.</em></strong>
</p>

<p align="center">
  <sub>Um conjunto de ferramentas para entender de verdade um conhecimento desconhecido — um conceito, a expertise de uma área, um algoritmo, uma biblioteca, um sistema, uma decisão de design ou uma mudança de código — em vez de se contentar com a impressão que um resumo deixa.</sub>
</p>

<p align="center">
  <sub><a href="../../README.md">English</a> &middot; <a href="README.ko.md">한국어</a> &middot; <a href="README.zh.md">中文</a> &middot; <a href="README.ja.md">日本語</a> &middot; <a href="README.es.md">Español</a> &middot; <a href="README.ru.md">Русский</a></sub>
</p>

---

Ler uma explicação produz a impressão de entender, não o entendimento. O mind-meld fecha essa lacuna medindo-a: constrói um mundo que você pode explorar, aplica um quiz, ataca o ponto fraco e avalia a sua própria explicação até ela se sustentar. O nome vem da [fusão mental vulcana](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld): um caminho para outra mente — a de um especialista, a de um autor, a de um agente.

## Duas formas de usar

**Trilha 1 — uma sessão completa.** Chame o orquestrador com o que você quer entender; ele roda o
fluxo inteiro.

```
/mind-meld "consistent hashing"
/mind-meld src/scheduler.ts
/mind-meld #42
```

**Trilha 2 — uma ferramenta, sob demanda.** Chame uma ferramenta diretamente com o que for: um
conceito, um módulo, um algoritmo, um artigo, uma frase que você leu.

```
/microworld "consistent hashing"
/socratic src/scheduler.ts
/five-whys "por que este repo fixa todas as versões"
/first-principles "vector clocks"
```

A trilha 1 é um pipeline medido, com nota de aprovação. A trilha 2 é uma ferramenta, pelo tempo que
você quiser. Só o orquestrador escolhe ferramentas por você; na trilha 2, você escolhe.

## Trilha 1: a sessão completa

```
/mind-meld "consistent hashing"
```

1. **Microworld** — um mundo HTML interativo que incorpora o mecanismo, não um resumo dele. Você
   explora. A sessão espera.
2. **Quiz** — poucas perguntas com resposta determinada, para localizar o que você deixou passar. Não
   aprova nem reprova.
3. **Uma ferramenta profunda** — `feynman`, `five-whys`, `socratic` ou `first-principles`, conforme o
   que você deixou passar.
4. **Redação curta** — explique para um colega, de memória. Um conceito recebe uma nota; uma mudança de
   código é avaliada em três eixos: **O que** mudou, **Por que** assim, **O que pode quebrar**.
5. **Aprovação com 8/10 em todos os eixos**, ou revisão. Duas revisões falhas trocam a ferramenta
   profunda; quatro falhas encerram a sessão e dizem isso — é evidência de que o alvo está obscuro, não
   você.

Para uma mudança de código, sai `.mind-meld/<alvo>-report.md`: as notas, o que continuou obscuro e
as perguntas para devolver a quem o produziu. Para um conceito, o relatório é opcional. Nada é enviado
por você, e o que você decidir com esse entendimento é seu.

O alvo pode ser um conceito, um caminho, um número de PR, um branch ou um intervalo de commits. Sem
argumento, ele pega o assunto da conversa.

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
- A saída vai para `.mind-meld/`, incluído em `.git/info/exclude` — sua árvore de trabalho fica limpa.
- A sessão fala a sua língua. Avaliar um texto em segunda língua mede redação, não compreensão.
- Sem scripts, sem dependências, sem build. Oito arquivos `SKILL.md`.

[MIT](../../LICENSE).
