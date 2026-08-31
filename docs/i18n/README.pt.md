# mind-meld

Um conjunto de ferramentas para entender os conceitos, conhecimentos e decisões de projeto pouco
familiares que um agente traz enquanto escreve código — antes de confiar neles. Seu palco mais
frequente é o pull request que o agente acabou de abrir, mas o alvo pode ser qualquer módulo,
algoritmo, biblioteca, decisão arquitetural ou conceito em si.

Agentes produzem mais rápido do que um humano lê. O gargalo da revisão não é clicar em aprovar, é
entender o que você está aprovando. O nome vem da [fusão mental
vulcana](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld): um caminho para dentro da
cabeça do agente.

## Como uma sessão corre

```
/mind-meld 42
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

Cada ferramenta também roda sozinha.

```
/microworld src/scheduler.ts
/five-whys 42
/first-principles "vector clocks"
```

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

Atualize com `git -C ~/.mind-meld pull` — os symlinks acompanham. O Claude Code atualiza pelo
marketplace.

## O que tem dentro

| Skill | O que faz |
| --- | --- |
| `mind-meld` | O orquestrador. Roteia para os demais. |
| `microworld` | Mundo HTML interativo que encarna o mecanismo. |
| `quiz` | Poucas perguntas determinadas; localiza a lacuna. |
| `socratic` | Uma pergunta por vez, até você ver o que quebra. |
| `feynman` | Explique em linguagem simples; os pontos vagos são marcados. |
| `five-whys` | Desce até a restrição que forçou a decisão. |
| `first-principles` | Reconstrói uma ideia estranha a partir das primitivas. |
| `short-essay` | O instrumento de medida. Avaliado e revisado até sustentar. |

Só `mind-meld` dispara sozinho. As outras sete são de chamada explícita, então pedir uma explicação
nunca vira um diálogo socrático de surpresa.

## Notas

- Sem estado. Não guarda notas entre sessões.
- A saída vai para `.mind-meld/`, incluído em `.git/info/exclude` — o diff em revisão fica limpo.
- A sessão fala a sua língua. Avaliar um texto em segunda língua mede redação, não compreensão.
- Sem scripts, sem dependências, sem build. Oito arquivos `SKILL.md`.

MIT.
