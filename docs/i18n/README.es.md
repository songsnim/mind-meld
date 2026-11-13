<p align="center">
  <img src="../../assets/hero.png" width="220" alt="mind-meld">
</p>

<h1 align="center">mind-meld</h1>

<p align="center">
  <strong><em>Otra mente a tu mente. Entiéndelo antes de confiar en ello.</em></strong>
</p>

<p align="center">
  <sub>Un conjunto de herramientas para entender de verdad un conocimiento desconocido —un concepto, la pericia de un campo, un algoritmo, una biblioteca, un sistema, una decisión de diseño o un cambio de código— en lugar de conformarte con la impresión que deja un resumen.</sub>
</p>

<p align="center">
  <sub><a href="../../README.md">English</a> &middot; <a href="README.ko.md">한국어</a> &middot; <a href="README.zh.md">中文</a> &middot; <a href="README.ja.md">日本語</a> &middot; <a href="README.pt.md">Português</a> &middot; <a href="README.ru.md">Русский</a></sub>
</p>

---

Leer una explicación produce la impresión de entender, no la comprensión. mind-meld cierra esa brecha midiéndola: construye un mundo que puedes explorar, te pone un cuestionario, ataca el punto débil y califica tu propia explicación hasta que se sostiene. El nombre viene de la [fusión mental vulcana](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld): una vía hacia otra mente —la de un experto, la de un autor, la de un agente.

## Dos formas de usarlo

**Vía 1 — una sesión completa.** Llama al orquestador con lo que quieras entender; ejecuta todo el
flujo.

```
/mind-meld "consistent hashing"
/mind-meld src/scheduler.ts
/mind-meld #42
```

**Vía 2 — una herramienta, cuando la necesites.** Llama a una herramienta directamente con lo que sea:
un concepto, un módulo, un algoritmo, un artículo, una frase que leíste.

```
/microworld "consistent hashing"
/socratic src/scheduler.ts
/five-whys "por qué este repo fija todas las versiones"
/first-principles "vector clocks"
```

La vía 1 es un pipeline medido con nota de aprobado. La vía 2 es una herramienta, todo el tiempo que
quieras. Solo el orquestador elige herramientas por ti; en la vía 2 eliges tú.

## Vía 1: la sesión completa

```
/mind-meld "consistent hashing"
```

1. **Microworld** — un mundo HTML interactivo que encarna el mecanismo, no un resumen. Tú lo exploras.
   La sesión espera.
2. **Quiz** — unas pocas preguntas con respuesta determinada, para ubicar lo que se te escapó. No te
   aprueba ni te suspende.
3. **Una herramienta profunda** — `feynman`, `five-whys`, `socratic` o `first-principles`, según lo que
   se te escapó.
4. **Ensayo corto** — explícaselo a un colega, de memoria. Un concepto recibe una sola nota; un cambio de
   código se califica en tres ejes: **Qué** cambió, **Por qué** así, **Qué puede romperse**.
5. **Aprobado con 8/10 en cada eje**, o a revisar. Dos revisiones fallidas cambian la herramienta
   profunda; cuatro fallos terminan la sesión y lo dicen: es evidencia de que el objetivo no está claro,
   no tú.

Para un cambio de código sale `.mind-meld/<objetivo>-report.md`: las notas, lo que siguió sin
quedar claro y las preguntas para devolver a quien lo produjo. Para un concepto el informe es opcional.
No se envía nada por ti, y lo que decidas con esa comprensión es cosa tuya.

El objetivo puede ser un concepto, una ruta, un número de PR, una rama o un rango de commits. Sin
argumento, toma el tema de la conversación.

## Vía 2: cualquier herramienta, sobre cualquier cosa

No hay calificación ni orden obligatorio. Elige según dónde estés atascado:

| Atascado en | Llamada |
| --- | --- |
| No consigo imaginar cómo se comporta | `/microworld <cosa>` |
| Quiero saber qué se me escapó | `/quiz <cosa>` |
| No sé decir qué se rompería | `/socratic <cosa>` |
| Creo que lo entiendo pero no sé explicarlo | `/feynman <cosa>` |
| No veo por qué se hizo así | `/five-whys <cosa>` |
| El vocabulario mismo es nuevo | `/first-principles <cosa>` |
| Quiero que puntúen mi comprensión | `/short-essay <cosa>` |

El argumento es texto libre. `/microworld "CRDT merge"` y `/microworld src/merge.ts` son ambos
válidos.

## Instalación

Copia solo el bloque del agente que uses.

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

Actualiza con `git -C ~/.mind-meld pull`; los enlaces simbólicos siguen. Claude Code se actualiza por
el marketplace.

## Qué incluye

Ocho skills: `mind-meld` más las siete herramientas entre las que enruta — `microworld`, `quiz`,
`socratic`, `feynman`, `five-whys`, `first-principles`, `short-essay`. Solo `mind-meld` se activa por
sí mismo; las otras siete son de invocación explícita, así que pedir una explicación nunca acaba en
un diálogo socrático por sorpresa.

## Notas

- Sin estado. No recuerda puntuaciones entre sesiones.
- La salida va a `.mind-meld/`, añadido a `.git/info/exclude`: tu árbol de trabajo queda limpio.
- La sesión habla tu idioma. Calificar un ensayo en un segundo idioma mide redacción, no comprensión.
- Sin scripts, sin dependencias, sin build. Ocho archivos `SKILL.md`.

[MIT](../../LICENSE).
