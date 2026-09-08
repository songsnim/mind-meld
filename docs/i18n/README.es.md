<p align="center">
  <img src="../../assets/hero.png" width="220" alt="mind-meld">
</p>

<h1 align="center">mind-meld</h1>

<p align="center">
  <strong><em>La mente del agente a tu mente. Entiéndelo antes de confiar en ello.</em></strong>
</p>

<p align="center">
  <sub>Un conjunto de herramientas para entender los conceptos, el conocimiento y las decisiones de diseño poco familiares que un agente incorpora mientras escribe código, antes de confiar en ellos. Su lugar más frecuente es el pull request que el agente acaba de abrir, pero el objetivo puede ser cualquier módulo, algoritmo, biblioteca, decisión arquitectónica o concepto por sí mismo.</sub>
</p>

<p align="center">
  <sub><a href="../../README.md">English</a> &middot; <a href="README.ko.md">한국어</a> &middot; <a href="README.zh.md">中文</a> &middot; <a href="README.ja.md">日本語</a> &middot; <a href="README.pt.md">Português</a> &middot; <a href="README.ru.md">Русский</a></sub>
</p>

---

Los agentes producen más rápido de lo que un humano lee. El cuello de botella de la revisión no es pulsar aprobar, es entender qué se está aprobando. El nombre viene de la [fusión mental vulcana](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld): una vía hacia la cabeza del agente.

## Dos formas de usarlo

**Vía 1: hay un PR que revisar.** Llama al orquestador y él ejecuta todo el flujo.

```
/mind-meld #42
```

**Vía 2: cualquier otra cosa que no entiendas.** Llama a una herramienta directamente con lo que sea:
un concepto, un módulo, un algoritmo, un paper, una frase que acabas de leer.

```
/microworld "consistent hashing"
/socratic src/scheduler.ts
/five-whys "por qué este repo fija todas las versiones"
/first-principles "vector clocks"
```

La vía 1 es un proceso medido con nota de corte. La vía 2 es una sola herramienta, cuando quieras y
durante el tiempo que quieras. Solo el orquestador elige herramientas por ti; en la vía 2 eliges tú.

## Vía 1: revisar un PR

```
/mind-meld #42
```

1. **microworld** — un mundo HTML interactivo que encarna el mecanismo, no un resumen del cambio. Tú
   lo exploras; la sesión espera.
2. **quiz** — unas pocas preguntas de respuesta determinada, para localizar lo que se te escapó. No
   aprueba ni suspende.
3. **Una herramienta profunda** — `feynman`, `five-whys`, `socratic` o `first-principles`, según el
   eje que falló.
4. **short-essay** — explícalo a un colega, de memoria. Se califica en tres ejes: **qué** cambió,
   **por qué** así, **qué puede romperse**.
5. **Se aprueba con 8/10 en todos los ejes**; si no, se revisa. Dos revisiones fallidas cambian la
   herramienta profunda; cuatro fallos terminan la sesión y lo dicen: eso es evidencia de que el
   cambio es confuso, no de que tú seas lento.

El resultado es `.mind-meld/<objetivo>-report.md`: las puntuaciones, lo que quedó sin aclarar y las
preguntas para devolver al agente. Nada se publica por ti. La aprobación es tuya; mind-meld no
aprueba.

Una rama, un rango de commits, una ruta o ningún argumento (el diff de trabajo) funcionan igual que
un número de PR.

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
- La salida va a `.mind-meld/`, añadido a `.git/info/exclude`: el diff en revisión queda limpio.
- La sesión habla tu idioma. Calificar un ensayo en un segundo idioma mide redacción, no comprensión.
- Sin scripts, sin dependencias, sin build. Ocho archivos `SKILL.md`.

[MIT](../../LICENSE).
