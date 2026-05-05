# Guía de desarrollo de software asistido por IA

> Manual técnico, modelo-agnóstico, en Markdown. Para developers con años de Software 1.0 que llegan por primera vez a IA con seriedad. Del primer prompt a producción con observabilidad y evals.

**Estado**: en construcción. Versión actual: `0.1.0` (esqueleto). Ver [`CHANGELOG.md`](./CHANGELOG.md).

**Licencia**: [CC-BY-SA 4.0](./LICENSE).

---

## Para quién es

Si llevas años escribiendo software clásico y este es tu primer contacto profesional con desarrollo asistido por IA, este manual es para ti. Asume que sabes refactorizar, leer un diff, escribir tests y revisar una PR. No asume que sabes qué es un *agent loop*, cómo se gobierna un *context window*, ni por qué el código generado por IA viene con 1.7× más bugs que el escrito a mano.

No es para principiantes en programación. No es un tutorial de un producto concreto. No es un manifiesto.

---

## Cómo está organizado

**43 capítulos en 9 partes**, ~17 horas de lectura activa. Cada capítulo tiene una modalidad [Diátaxis](https://diataxis.fr/) declarada en el frontmatter (`tutorial`, `how-to`, `reference`, `explanation`).

| Parte | Capítulos | Tiempo | De qué trata |
|---|---|---|---|
| I — De Software 1.0 a Software 3.0 | 01–04 | 70 min | Anclaje. Qué de tu oficio sigue siendo levier y qué cambia |
| II — Conversar con el modelo | 05–09 | 113 min | Prompt, context window, few-shot, RAG, system prompts |
| III — El loop de un agente | 10–12 | 70 min | Tool use, plan-act-observe, MCP |
| IV — Workflow asistido | 13–16 | 105 min | Tutorial replicado en dos coding agents reales |
| V — Specs como código | 17–20 | 78 min | Spec-driven, EARS, frameworks, AGENTS.md |
| VI — Calidad cuando no escribiste el código | 21–26 | 145 min | Antipatterns, TDD para agentes, adversarial review, seguridad |
| VII — Harness aplicado | 27–32 | 110 min | Agent = Model + Harness, feedforward/feedback, multi-agente, HITL, drift |
| VIII — Producción | 33–38 | 130 min | Observabilidad, costo/latencia, evals, ROI, compliance, gates |
| IX — Síntesis | 39–43 | 90 min | Antipatterns globales, casos, playbook, mirada adelante |

Ver el índice canónico completo en [`OUTLINE.md`](./OUTLINE.md).

---

## Rutas de aprendizaje

No tienes que leer en orden. Elige la ruta que coincide con tu situación.

### 1. "Vengo de backend tradicional, primer contacto serio con IA"
`01 → 02 → 03 → 04 → 05 → 06 → 07 → 08 → 10 → 13 → 14 → 21 → 22 → 23`

MCP y multi-agente saltados en primera pasada. Cap. 09 (RAG) opcional.

### 2. "Soy lead, necesito decidir tooling para mi equipo"
`02 → 04 → 21 → 12 → 19 → 20 → 13 → 22 → 27 → 28 → 36 → 37 → 41`

Sin pasada al agente operando (cap. 13) y sin antipatterns concretos (cap. 22), decides a ciegas.

### 3. "Quiero llegar a producción rápido (MVP aceptando deuda)"
`04 → 21 → 10 → 13 → 14 → 20 → 23 → 24 → 25 → 35 → 38`

El cap. 21 al inicio no es opcional. Sin internalizar el riesgo, prod rápido es vibe coding con esteroides.

### 4. "Vengo de Cursor/Copilot pero sin método"
`04 → 08 → 14 → 16 → 20 → 22 → 23 → 25`

El cap. 23 (TDD para agentes) es la pieza que probablemente te falta.

### 5. "Mi equipo ya genera con IA y la calidad bajó"
`21 → 22 → 23 → 24 → 25 → 32 → 28 → 35`

Triaje primero, reforma sistémica después con cap. 28 (feedforward/feedback).

### 6. "Quiero entender la disciplina a fondo"
Lee [`OUTLINE.md`](./OUTLINE.md) y elige tu propio orden. La numeración 01 → 43 es válida pero no obligatoria; los `prerrequisitos` en frontmatter son la guía dura.

### 7. "Developer senior escéptico forzado por su empresa"
`01 → 21 → 04 → 16 → 22 → 39 → 41`

Crítica antes que promesa. Empieza por qué del oficio sigue valiendo (01) y los datos incómodos (21). Después el modo de adopción operacional (04, 16, 22). Cierra con repaso y playbook (39, 41).

---

## Cómo leer un capítulo

Cada capítulo tiene un frontmatter YAML que declara modalidad, tiempo, prerrequisitos y fecha de validación:

```yaml
---
modalidad: how-to
archivo: cap-22-code-review-ia
parte: 6
tiempo_estimado: 30 min
prerrequisitos: [cap-21]
herramientas: [gemini-code-assist, cline]
caducidad: estable
es_repaso: false
validado: 2026-05
---
```

Si la `caducidad` es `revisar-trimestral`, el capítulo trata de herramientas o versiones que cambian rápido y se audita cada tres meses. Si `es_repaso: true`, no introduce conceptos nuevos: consolida los previos.

---

## Stack y prerrequisitos técnicos

Para los tutoriales de Parte IV (caps. 13–16) necesitarás:

- Editor con soporte de extensiones (VS Code recomendado).
- Cuenta de Google (para Gemini Code Assist y Gemini API key gratuita).
- Node 20+ y `git` instalados.

No hace falta tarjeta de crédito. Las dos herramientas elegidas tienen free-tier real verificado en mayo 2026.

---

## Convenciones, contribución y lectura crítica

- Convenciones de prosa y prohibiciones explícitas: [`STYLE.md`](./STYLE.md).
- Términos canónicos (30 conceptos): [`GLOSSARY.md`](./GLOSSARY.md).
- Bibliografía con URL y fecha de consulta: [`SOURCES.md`](./SOURCES.md).
- Cómo proponer correcciones: [`CONTRIBUTING.md`](./CONTRIBUTING.md).
- Plan curricular completo: [`PLAN.md`](./PLAN.md).
- Contrato del agente que escribe el manual: [`AGENTS.md`](./AGENTS.md).

---

## Por qué existe esta guía

Porque la mayoría del material disponible es uno de estos tres extremos: marketing de un producto concreto, teoría académica sin loop práctico, o vibe-coding tutorials que no escalan. Falta el puente entre el oficio que ya tienes y el cambio real que ocurre cuando usas IA para escribir código que va a producción.

Esta guía intenta ser ese puente.
