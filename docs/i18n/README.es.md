# mind-meld

Un conjunto de herramientas para entender los conceptos, el conocimiento y las decisiones de diseño
poco familiares que un agente incorpora mientras escribe código, antes de confiar en ellos. Su lugar
más frecuente es el pull request que el agente acaba de abrir, pero el objetivo puede ser cualquier
módulo, algoritmo, biblioteca, decisión arquitectónica o concepto por sí mismo.

Los agentes producen más rápido de lo que un humano lee. El cuello de botella de la revisión no es
pulsar aprobar, es entender qué se está aprobando. El nombre viene de la [fusión mental
vulcana](https://en.wikipedia.org/wiki/Vulcan_(Star_Trek)#Mind_meld): una vía hacia la cabeza del
agente.

## Cómo transcurre una sesión

```
/mind-meld 42
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

Cada herramienta también se invoca sola.

```
/microworld src/scheduler.ts
/five-whys 42
/first-principles "vector clocks"
```

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

Actualiza con `git -C ~/.mind-meld pull`; los enlaces simbólicos siguen. Claude Code se actualiza por
el marketplace.

## Qué incluye

| Skill | Qué hace |
| --- | --- |
| `mind-meld` | El orquestador. Enruta hacia el resto. |
| `microworld` | Mundo HTML interactivo que encarna el mecanismo. |
| `quiz` | Pocas preguntas determinadas; localiza el hueco. |
| `socratic` | Una pregunta cada vez, hasta que veas qué se rompe. |
| `feynman` | Explícalo en llano; se marcan los puntos vagos. |
| `five-whys` | Bajar hasta la restricción que forzó la decisión. |
| `first-principles` | Reconstruir una idea ajena desde sus primitivas. |
| `short-essay` | El instrumento de medida. Calificado y revisado hasta que aguante. |

Solo `mind-meld` se activa por sí mismo. Las otras siete son de invocación explícita, así que pedir
una explicación nunca acaba en un diálogo socrático por sorpresa.

## Notas

- Sin estado. No recuerda puntuaciones entre sesiones.
- La salida va a `.mind-meld/`, añadido a `.git/info/exclude`: el diff en revisión queda limpio.
- La sesión habla tu idioma. Calificar un ensayo en un segundo idioma mide redacción, no comprensión.
- Sin scripts, sin dependencias, sin build. Ocho archivos `SKILL.md`.

MIT.
