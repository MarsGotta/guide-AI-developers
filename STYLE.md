# STYLE.md — Voz, registro y prohibiciones

> Contrato de estilo para los 43 capítulos de la guía. Cualquier desviación se justifica en el commit.

---

## 1. Voz general

Escribimos para *developer experienced* que llega por primera vez a IA con seriedad. No es novato en software. No quiere drills, no quiere motivación, no quiere palmadita en la espalda. Quiere ver el oficio cambiar y entender qué del suyo sigue valiendo.

- **Primera persona plural** ("vamos a ver…", "tenemos dos opciones…").
- **Frases cortas**. Si una frase tiene más de 25 palabras, parte.
- **Verbos en activa**. La pasiva refleja se reserva para procesos genuinamente sin agente.
- **Concreto antes que abstracto**. Una escena, un archivo, un error real, una métrica.
- **Conectar al oficio**. "Igual que ya haces con tests" funciona; "imagina que…" no.

---

## 2. Registros por modalidad Diátaxis

Cada modalidad tiene su propio registro de prosa. La skill chain `spanish-prose-craft` se aplica con la variante correspondiente.

### Tutorial (`tutorial`)
Registro de **escena**. Narración paso a paso, primera persona plural, presente del indicativo. El lector va con nosotros. Cada paso muestra el resultado completo antes de pedir transferencia (worked example effect).

> Abrimos `package.json`. Vemos que el agente añadió `lodash` como dependencia. Antes de aceptarlo, verificamos…

### How-to (`how-to`)
Registro de **instrucción**. Imperativo, paso numerado o con bullets, sin preámbulo. Asume lector competente.

> 1. Define la rúbrica en `eval-rubric.md`.
> 2. Lanza el evaluador con `--rubric eval-rubric.md`.
> 3. Revisa el output. Si la nota media baja de 7, recalibra.

### Reference (`reference`)
Registro de **catálogo**. Prosa mínima. Tablas, listas comparativas, definiciones. El lector busca dato, no argumento.

> | Término | Significado | Ejemplo |
> |---|---|---|
> | `temperature` | Aleatoriedad del muestreo (0 = determinista, 1+ = creativo) | 0.2 para código, 0.7 para prosa |

### Explanation (`explanation`)
Registro de **argumento**. Prosa con tensión: tesis, contraste, evidencia, conclusión. Ningún capítulo de explanation es solo "¿qué es X?"; es "por qué X cambia algo del oficio".

> El context window no es solo un límite técnico. Es lo que decide qué del repo el modelo "sabe" y qué inventa. Y eso convierte el orden de lo que metes en una decisión de arquitectura.

---

## 3. Registro frente a developer senior escéptico

El 30 % del público real es un developer senior obligado por la empresa a usar IA, dudando del paradigma, leyendo a la defensiva. Si la prosa parece marketing, cierra la guía.

### Prohibiciones explícitas (cero tolerancia)

- **"Imagina que…"**, "imagínate", "pensemos juntos".
- **"Magic"**, "mágico", "milagroso", "increíble", "potente", "revoluciona".
- **"Let's dive in"**, "profundicemos", "vamos a explorar".
- **Viñetas-explicativas-de-tres-puntos al inicio de sección** (si hay 3 puntos, escribe en prosa).
- **Apertura de capítulo con tesis genérica** ("La IA está cambiando el desarrollo…"); siempre escena u objeto concreto.
- **Cierres motivacionales** ("¡Ahora tienes las herramientas!"). Cierre seco: instrucción accionable o pregunta abierta concreta.
- **Emojis decorativos**. Salvo en la tabla de modalidades de OUTLINE.md (uno por celda como icono funcional).
- **Mayúsculas para énfasis** (NUNCA usar). Cursiva sí, negrita con criterio.
- **Citas de "expertos" sin trazabilidad**. Toda cita pasa por SOURCES.md con URL y fecha.

### Aperturas que sí funcionan

- Una escena: "Cline acaba de proponer un cambio que toca seis archivos. Antes de aceptar, miramos…"
- Un objeto: "Este AGENTS.md tiene 312 líneas. Es el problema."
- Un dato: "Apiiro analizó 50 empresas Fortune. El código generado por IA tenía 322 % más vulnerabilidades de privilege escalation que el escrito por humanos."
- Una pregunta concreta: "¿Por qué tu refactor con tests verdes pasó a producción y rompió el flujo de pago?"

### Aperturas que NO funcionan

- "En este capítulo veremos…"
- "La inteligencia artificial está transformando…"
- "Como developers, sabemos que…"
- "Imagina que tu equipo…"

---

## 4. Convenciones tipográficas

- **Cursiva** (`*texto*`): primera aparición de un término canónico, siempre con definición seca de una frase a continuación.
- **Negrita** (`**texto**`): palabra clave de la frase. Máximo una por párrafo.
- **`Backticks`**: nombres de archivos, comandos, variables, identificadores de código.
- **Bloques de código**: lenguaje declarado siempre (` ```bash`, ` ```yaml`, ` ```typescript`).
- **Citas en bloque** (`>`): para definiciones canónicas, advertencias, o cita textual de fuente.
- **Tablas**: para reference. No abusar en explanation o tutorial.
- **Listas**: bullets sin viñeta-explicativa al inicio. Si una sección tiene 3 bullets de una palabra, vuelve a prosa.

---

## 5. Carga cognitiva (Sweller)

- **Una unidad nueva por sub-sección**. La sub-sección introduce un solo concepto canónico nuevo.
- **Reuso explícito**: si reusas un concepto del cap. anterior, dilo: "vimos en cap. 06 que…".
- **Densidad declarada**: capítulos `reference` de marco (caps. 03, 12, 19, 29, 37) llevan en frontmatter `densidad: alta` y advertencia en cabecera.
- **Worked example effect**: en `tutorial`, cada paso muestra resultado antes de transferencia.

---

## 6. Bilingüismo

Cuerpo en **español neutro**. Términos en **inglés** cuando son nombres propios o jerga consolidada en el dominio.

### Anglicismos que se mantienen

`prompt`, `context window`, `tool use` (function calling), `agent`, `agent loop`, `harness`, `MCP`, `system prompt`, `few-shot`, `zero-shot`, `chain-of-thought`, `RAG`, `golden dataset`, `eval`, `HITL`, `drift`, `prompt injection`, `jailbreak`, `prompt caching`, `vibe coding`, `spec-driven`, `EARS`, `feedforward`, `feedback`, `sprint contract`, `context reset`, `compaction`, `hallucination`, `refactoring avoidance`, `context blindness`, `shotgun surgery`, `reward hacking`, `generator-evaluator`.

### Cómo se introducen

- **Primera aparición** en un capítulo: en cursiva con definición seca de una frase.
  > Un *prompt* es la entrada de texto que damos al modelo para que genere una respuesta.
- **Siguientes apariciones**: en redonda, sin cursiva, sin definir.
- **Nunca traducción forzada**: jamás "arnés" para *harness*, jamás "ventana de contexto" como sustituto canónico (puede aparecer como aclaración una vez).

### Términos que sí traducimos

`agente`, `modelo`, `herramienta` (cuando no es jerga técnica), `revisor`, `evaluador`, `flujo`, `tubería` (preferimos `pipeline` solo en `eval pipeline`).

---

## 7. Términos prohibidos en cuerpo y titulares

- **"IA generativa"** en titulares (en cuerpo permitido si distingue de IA discriminativa).
- **"potente"**, **"empoderar"**, **"mágico"**, **"increíble"**, **"revolucionario"**.
- **"arnés"** (siempre `harness`).
- **"última generación"**, **"de vanguardia"**, **"state-of-the-art"** sin fecha de consulta.
- **"experto"** referido a un humano sin nombre y fuente.
- **"todos los developers"**, **"siempre"**, **"nunca"** sin matiz.

---

## 8. Citas y fuentes

- Toda afirmación numérica viene con fuente: `(Apiiro 2025, ver SOURCES.md)`.
- Cita a la guía hermana: `[harness-eng-guide §parte.cap]` + URL y fecha en SOURCES.md.
- Datos de calidad de código IA (1.7×, 75 %, 322 %, 153 %): siempre con muestra y limitación del estudio en cap. 21.
- Fuentes con caducidad (versiones, herramientas): fecha de consulta visible. Patrones (EARS, Diátaxis, AGENTS.md) atemporales: sin fecha.

---

## 9. Cierre del capítulo

Tres formas válidas:

1. **Instrucción accionable**: "Antes del siguiente capítulo, audita tu AGENTS.md con el rubric del anexo."
2. **Pregunta abierta concreta**: "¿Cuál de los seis antipatterns ya viste en una PR de tu equipo este mes?"
3. **Bisagra al siguiente**: "El cap. 20 te da el AGENTS.md operativo. Aquí cerramos viendo por qué tu repo lo necesita."

Nunca "espero que hayas disfrutado", nunca "¡a por el siguiente!", nunca emoji de confeti.

---

## 10. Revisión por modalidad (skill chain)

Cada capítulo pasa por:

| Modalidad | skill chain |
|---|---|
| `tutorial` | `technical-guide-design` → `spanish-prose-craft` (registro escena) → `humanizer` |
| `how-to` | `technical-guide-design` → `spanish-prose-craft` (registro instrucción) → `humanizer` |
| `reference` | `technical-guide-design` → `spanish-prose-craft` (registro catálogo, prosa mínima) → `humanizer-light` |
| `explanation` | `technical-guide-design` → `spanish-prose-craft` (registro argumento) → `humanizer` |

Evidencia del skill chain en el commit message del capítulo: `cap-NN: write + tgd + spc(escena) + humanizer`.
