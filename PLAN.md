# Plan refinado v2 — Guía de desarrollo de software asistido por IA

> **Diff vs plan original**: 41 → **43 capítulos** (RAG nuevo en II, multi-agente movido de III a VII, costo/latencia nuevo en VIII), tiempos a **~17 h** de lectura activa (15.5 h declaradas, 17–18 h realistas), glosario **22 → 30 términos** reorganizados, **7 rutas** (nueva: senior escéptico forzado), **12 riesgos pedagógicos**, **8 fases** con kill switch en Fase 3, **18–20 sesiones**, dos coding agents free-tier decididos para Parte IV.

> **Cambios v2 vs v1** (segunda revisión): cap. 13 movido a Parte VII; nuevo cap. en Parte VIII (costo/latencia/caching); modalidades corregidas en caps. 09, 30; ROI subido a 20 min; cap. 38 declarado como repaso; dos hilos nuevos de spaced repetition (TDD, spec-driven); glosario reorganizado (− builder/user harness, + prompt injection, jailbreak, prompt caching, split reset/compaction); ruta 7 nueva; ruta 4 eliminada como ruta (era la TOC); decisiones pre-Fase 1 cerradas (coding agents, diagramas, licencia, eval rubric, pilotos); kill switch en Fase 3; sección "registro senior escéptico" en STYLE.md; variantes del skill chain por modalidad.

---

## Context

Marcela necesita una guía técnica modelo-agnóstica sobre desarrollo de software asistido por IA, en Markdown, bilingüe (cuerpo en español, jerga canónica en inglés). El público son developers con años de Software 1.0 en su primer contacto serio con IA: andragogía pura, sin drills, "por qué" antes que "cómo". El espectro va desde el primer prompt hasta producción con observabilidad y evals.

El directorio `/Users/marsgotta/Projects/guide-ai-developers/` está vacío. Existen dos linajes previos de la usuaria:
- **harness-engineering-guide** (42 capítulos, 8 partes, Diátaxis explícito): disciplina del harness desde la silla del *builder*.
- **taller-testing-frontend-material** (16 archivos, frontmatter YAML, rutas por perfil): plantilla didáctica.

Esta guía hereda ambos linajes pero adopta la perspectiva del *developer* que **usa** un coding agent en su repo — no del builder que construye el agente. Donde haya solapamiento conceptual con la guía hermana (Partes VII–VIII), se cita y enlaza, no se replica.

---

## Forma del arco

```mermaid
flowchart LR
    I["I. Paradigma<br/>01–04 · 70 min"] --> II["II. Prompt → Context<br/>05–09 · 113 min"]
    II --> III["III. Agente<br/>10–12 · 70 min"]
    III --> IV["IV. Workflow<br/>13–16 · 105 min"]
    IV --> V["V. Specs<br/>17–20 · 78 min"]
    V --> VI["VI. Calidad<br/>21–26 · 145 min"]
    VI --> VII["VII. Harness<br/>27–31 · 110 min"]
    VII --> VIII["VIII. Producción<br/>32–37 · 130 min"]
    VIII --> IX["IX. Síntesis<br/>38–42 · 90 min"]

    IV -. AGENTS.md .-> V
    V -. AGENTS.md .-> VII
    III -. tool use .-> VI
    II -. context engineering .-> VII
    VI -. eval ligero .-> VIII
    III -. hallucinated dep .-> VI
    VI -. TDD .-> VIII
    V -. spec-driven .-> VII
```

Cada parte abre una pregunta que la siguiente responde. Las flechas punteadas son los **7 hilos de spaced repetition**: cada concepto pesado se revisita al menos tres veces, con separación creciente.

---

## Estructura curricular: 43 capítulos en 9 partes

### Parte I — De Software 1.0 a Software 3.0 (anclaje)
*Diátaxis: explanation. Romper expectativas falsas y construir modelo mental.*

| # | Título | Mod. | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 01 | Lo que tu experiencia ayuda y lo que te traiciona | explanation | 12 min | — | Identificar qué del oficio sigue siendo levier (refactor, tests, tipos, code review) y qué cambia |
| 02 | Software 3.0 en una página | explanation | 18 min | 01 | Situar Karpathy: modelo como runtime, prompt como código, datos como dependencia |
| 03 | Anatomía de un LLM para developers | explanation | 25 min | 02 | Vocabulario mínimo: tokens, weights, sampling, temperature, inference, context window |
| 04 | Vibe coding vs structured AI development | explanation | 15 min | 02 | Distinguir modo exploratorio de modo producción y declarar dónde vive cada uno |

### Parte II — Conversar con el modelo (prompt → context engineering)
*Diátaxis: reference + how-to + explanation. Base operativa.*

| # | Título | Mod. | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 05 | Prompt como interfaz, no como conjuro | how-to | 25 min | 03 | Estructurar prompts con criterio de ingeniería |
| 06 | Context window y la atención del modelo | reference | 25 min | 05 | Decidir qué meter, qué dejar fuera, dónde colocarlo |
| 07 | Few-shot, system prompts y plantillas | how-to | 20 min | 05, 06 | Calibrar comportamiento con ejemplos y system prompts reusables |
| 08 | De prompt engineering a context engineering | explanation | 18 min | 06, 07 | El problema real es gobernar el contexto, no afinar la frase |
| 09 | RAG: cuándo el contexto vive fuera del prompt | **explanation** | 25 min | 08 | Distinguir RAG ligero (lookup) de RAG pesado (retrieval system); decidir cuándo añadir vectores y cuándo no |

> **Cambio v2**: cap. 09 modalidad `reference` → `explanation`. El objetivo es decisión, no catálogo.

### Parte III — El loop de un agente (tool use, MCP)
*Diátaxis: explanation + reference. Más ligera que en v1: multi-agente movido a Parte VII.*

| # | Título | Mod. | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 10 | Tool use: el modelo aprende a llamar funciones | explanation | 25 min | 09 | Contrato de function-calling, structured output, qué amplía y qué no |
| 11 | El loop básico: plan, act, observe | explanation | 20 min | 10 | Modelar un agente como bucle con estado y criterios de parada |
| 12 | MCP, el USB-C de los agentes | reference | 25 min | 10 | Qué resuelve Model Context Protocol, cuándo merece la pena, cuándo no |

> **Cambio v2**: el cap. de topologías multi-agente sale de aquí (era el 13) y va a Parte VII como cap. 31. Razón: sin haber operado un agente, multi-agente es abstracción pura. Beneficio: descomprime el punto crítico de saturación.

### Parte IV — Trabajo asistido en el día a día (worked example)
*Diátaxis: tutorial. Recorrido en primera persona, replicado en **dos coding agents free-tier**: Gemini Code Assist + Cline (decisión cerrada en sección "Decisiones pre-Fase 1").*

| # | Título | Mod. | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 13 | Setup: repo, agente y primer prompt útil | tutorial | 30 min | 04, 07 | Arrancar repo nuevo con un agente y obtener primer cambio revisable |
| 14 | El workflow Willison: especificar, seguir, revisar | tutorial | 25 min | 13 | Aplicar las tres fases sin perder control; introducir "review como mini-eval" |
| 15 | Refactor con agente: pequeño, verificable, reversible | tutorial | 30 min | 14 | Guiar refactors graduales con tests como red de seguridad |
| 16 | Cuando el agente se atasca: diagnóstico y rescate | how-to | 20 min | 14 | Reconocer síntomas (loops, hallucinated deps, context blindness) y salir |

### Parte V — Specs como código (spec-driven development)
*Diátaxis: explanation + how-to.*

| # | Título | Mod. | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 17 | Por qué la especificación es el nuevo código fuente | explanation | 18 min | 12, 15 | Argumentar la spec como levier sin caer en waterfall regresivo |
| 18 | EARS: requisitos que un agente puede ejecutar | reference | 20 min | 17 | Escribir requisitos en notación EARS sin ambigüedad |
| 19 | Frameworks: Kiro, Spec Kit, BMAD-METHOD | reference | **15 min** | 17 | Comparar enfoques sin sectarismo. **Snapshot 2026; revisar trimestralmente** |
| 20 | AGENTS.md: el contrato de tu repo | how-to | 25 min | 13, 18 | AGENTS.md operativo (≤150 líneas, 6 áreas core, ejemplos sobre abstracciones) |

> **Cambio v2**: cap. 19 (frameworks) baja a 15 min y declara caducidad explícita en frontmatter. Mantengo separado de cap. 18 (EARS) porque EARS es atemporal y merece su capítulo propio.

### Parte VI — Calidad cuando el código no lo escribiste tú
*Diátaxis: how-to + reference. Aquí va la evidencia dura.*

| # | Título | Mod. | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 21 | El número incómodo: qué dicen los datos sobre código IA | explanation | 20 min | 15 | Internalizar la magnitud del riesgo (1.7× bugs, 75 % logic, 1.5–2× security) **con muestra y limitación de cada estudio** |
| 22 | Code review específico para AI: los seis antipatterns | how-to | 30 min | 21 | Detectar refactoring avoidance, context blindness, shotgun surgery (variante IA), hallucinated dependencies |
| 23 | Tests antes que código: TDD reescrito para agentes | how-to | 25 min | 22 | Pedir tests primero, ejecutarlos rojos, dejar al agente implementar para verde |
| 24 | Static analysis y type systems como sensores | reference | 20 min | 22 | Configurar el feedback determinista que un agente sí respeta; advertencia: feedback ≠ garantía |
| 25 | Adversarial AI review: un agente revisa al otro | how-to | 25 min | 23, 24 | Montar un revisor LLM con rúbrica calibrada y few-shot |
| 26 | Seguridad: secrets, dependencies, prompt injection, privilege escalation | how-to | 25 min | 22 | Cerrar vectores inflados (322 % privilege, 153 % architectural) **+ prompt injection y jailbreak** |

> **Cambio v2**: cap. 26 incorpora explícitamente prompt injection y jailbreak (vectores primarios en LLM-systems, omitidos en v1).

### Parte VII — Harness engineering aplicado
*Diátaxis: reference + explanation + how-to. Cita explícita de la guía hermana en cada capítulo.*

| # | Título | Mod. | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 27 | Agent = Model + Harness | explanation | 15 min | 25 | Aceptar la fórmula y por qué el harness gap pesa más que el model gap |
| 28 | Feedforward y feedback en tu repo | reference | 25 min | 27 | Catalogar guides (AGENTS.md, skills, MCP) y sensors (tests, lints, jueces) |
| 29 | Patrones del catálogo: generator-evaluator, sprint contracts, context reset | **how-to** | 30 min | 28 | **Aplicar** los patrones más rentables sin replicar la guía hermana |
| 30 | Topologías multi-agente | explanation | 25 min | 28 | Distinguir planner-coder-reviewer, generator-evaluator, supervisor-worker (visual, baja densidad) |
| 31 | HITL: dónde, cómo y cuándo no | how-to | 20 min | 28 | Diseñar puntos de intervención humana sin convertirlos en cuello de botella |
| 32 | Drift: cómo detectarlo antes de que duela | how-to | 20 min | 28 | Señales tempranas de desviación de convenciones |

> **Cambios v2**: cap. 29 modalidad `reference` → `how-to` (objetivo es "aplicar"). Cap. 30 (multi-agente) llega aquí desde Parte III.

### Parte VIII — Producción: observabilidad, evals, decisión
*Diátaxis: reference + explanation + how-to.*

| # | Título | Mod. | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 33 | Observabilidad de agentes: logs, traces, eval runs | reference | 25 min | 29 | Instrumentar un agente como instrumentas un servicio |
| 34 | Costo, latencia y prompt caching | reference | 25 min | 33 | Tokens cobrados, throughput, KV-cache, decisiones operacionales **(nuevo)** |
| 35 | Eval pipelines y golden datasets | how-to | 30 min | 25, 33 | Construir y mantener dataset de referencia y pipeline de regresión |
| 36 | Métricas y ROI: cuándo el harness vale la pena | explanation | **20 min** | 33, 34 | Justificar la inversión con números (lectura de lead) |
| 37 | Risk tiering y compliance ligero (NIST AI RMF, ISO 42001) | reference | 20 min | 31, 36 | Clasificar usos por riesgo y aplicar controles proporcionales |
| 38 | Despliegue con gates de eval pre-merge | how-to | 20 min | 35 | Ningún cambio entra sin pasar el eval |

> **Cambios v2**: nuevo cap. 34 (costo/latencia/caching) — tema más Software-1.0 ausente en v1, motivado por audiencia experienced. Cap. 36 (ROI) sube a 20 min.

### Parte IX — Síntesis y rutas adelante

| # | Título | Mod. | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 39 | Antipatterns globales: 12 trampas (repaso espaciado) | explanation | 20 min | 21–38 | **Revisión consolidada con vocabulario completo, declarado como repaso, no como contenido nuevo** |
| 40 | Casos comentados: Stripe, Shopify, Airbnb, Codex | explanation | 30 min | 27–36 | Ver harnesses reales y nombrarlos desde la silla del *developer* |
| 41 | Tu propio playbook: plantilla de adopción por equipo | how-to | 25 min | 20, 31, 35 | Salir con un plan concreto de adopción por sprint |
| 42 | Glosario navegable y mapa de fuentes | reference | consulta | — | Material de consulta permanente |
| 43 | Hacia dónde mirar: spec-first, agentic IDEs, autonomous teams | explanation | 15 min | todo | Cierre seco con punteros, sin moralejas |

> **Cambio v2**: cap. 39 declara explícitamente "repaso espaciado, no contenido nuevo" en frontmatter para evitar lectura como redundancia.

**Tiempo total agregado**: ≈ 945 min = **15.75 h declaradas**, **17–18 h realistas** para developers en primer contacto.

---

## Modalidad Diátaxis: auditoría v2

| Cap. | Cambio v2 | Razón |
|---|---|---|
| 09 (RAG) | reference → **explanation** | Decisión "cuándo sí/no" es explanation con tabla de decisión, no catálogo |
| 19 (Frameworks) | tiempo 25 → 15 min | Riesgo de caducidad alto; menos peso, más disclaimer |
| 29 (Patrones) | reference → **how-to** | Objetivo es "aplicar", no enumerar |
| 36 (ROI) | tiempo 15 → 20 min | Caso de negocio para audiencia escéptica |
| 39 (12 trampas) | declarado repaso | Solapamiento con caps. 22, 26 — tratar como revisión |

---

## Decisiones cerradas pre-Fase 1 (nuevo en v2)

> Ningún capítulo se escribe hasta que estas decisiones estén cerradas y los artefactos creados.

### 1. Coding agents para Parte IV (verificado mayo 2026)

| Agente | Rol pedagógico | Free tier (sin tarjeta) |
|---|---|---|
| **Gemini Code Assist for individuals** | IDE-integrada, propietaria, on-rails, Google account | 6.000 code requests/día + 240 chat requests/día |
| **Cline + Gemini API key gratuita** | CLI-agéntica, open source, BYOK, MCP nativo, plan/act explícito | 1.000 RPD vía Google AI Studio (60 RPM) |

**Ejes que cubren juntos**: propietaria vs open source · IDE-sidebar vs agéntico-CLI · on-rails vs BYOK · prompts entrenan el modelo vs no entrenan. Conversación pedagógica natural sobre privacidad en cap. 13.

**Descartados**: Cursor (50 premium reqs/mes), Windsurf (25 credits ≈ 1 día), GitHub Copilot Free (usage-based desde junio 2026), Continue.dev + Ollama (excluye laptops modestas), Aider (CLI puro sin IDE — lista en SOURCES.md como tercera opción opcional).

**Riesgo de caducidad**: Gemini Code Assist medio (14 meses como gratuito); Cline bajo (open source, BYOK resiliente — si Gemini recorta, swap a Groq, Cerebras u Ollama sin tocar la herramienta).

### 2. Eval rubric para los capítulos

Antes de Fase 1, escribir `plantillas/rubric-capitulo.md` con criterios objetivos:
- Frontmatter completo y modalidad coherente con apertura.
- Apertura concreta (escena, no tesis) en 3 primeras líneas.
- Una unidad nueva por sub-sección (CLT).
- Cada término canónico de cursiva-de-definición está en GLOSSARY.md.
- Cierre seco: instrucción accionable o pregunta abierta concreta. Sin moralina.
- Cada cita con URL + fecha en SOURCES.md.
- Prerrequisitos honestos (verificable con cap-cero-prereqs lectura).
- Skill chain ejecutado en orden con evidencia.

### 3. Reclutamiento de lectores piloto

Antes del cierre de Fase 0:
- **3 developers** con perfil objetivo (años Software 1.0, primer contacto serio con IA), nominados con compromiso de leer caps. 01–14 antes de Fase 4.
- **1 revisor con experiencia profesional en agentes** para Fase 7 (caps. 27–38).
- Formulario de feedback breve por capítulo (5 preguntas: dónde te perdiste, qué no usaste, qué usarías, tiempo real de lectura, modalidad cumplida sí/no).

### 4. Convención de diagramas

**Mermaid embebido en Markdown** por defecto · ASCII como fallback cuando Mermaid es excesivo (procesos lineales) · **prohibido SVG embebido** (problemas de renderizado y caducidad).

### 5. Licencia

**CC-BY-SA 4.0**. Cita a la guía hermana con `[harness-eng-guide §parte.cap]` + URL + fecha en SOURCES.md.

### 6. Variantes del skill chain por modalidad Diátaxis

Para evitar homogeneización tonal en 43 capítulos:
- **Tutorial**: `technical-guide-design → spanish-prose-craft (registro escena) → humanizer`.
- **How-to**: `technical-guide-design → spanish-prose-craft (registro instrucción) → humanizer`.
- **Reference**: `technical-guide-design → spanish-prose-craft (registro catálogo, prosa mínima) → humanizer-light`.
- **Explanation**: `technical-guide-design → spanish-prose-craft (registro argumento) → humanizer`.

Documentar en `STYLE.md` qué distingue cada registro con un párrafo-ejemplo.

---

## Justificación pedagógica del orden

**Forma del arco**. El lector empieza donde está (Software 1.0), desencripta el paradigma (I), gana herramientas mínimas (II–III), trabaja con un agente real (IV), reencuentra la autoridad de su oficio en las specs (V), confronta el dato incómodo (VI), formaliza la disciplina (VII) y queda en producción (VIII). Cada parte abre una pregunta que la siguiente responde.

**Carga cognitiva (Sweller)**. Una unidad nueva por sub-sección. Caps. 03, 12, 19, 29, 37 son reference de marco con densidad declarada en frontmatter. Parte IV aplica *worked example effect*. **Cambio v2**: Parte III ahora tiene 3 capítulos en lugar de 4 — se quitó la presión del punto crítico de saturación al mover multi-agente a VII.

**Spaced repetition** (7 hilos auditados):
- **AGENTS.md**: 13 → 20 → 28 → 41.
- **tool use**: 10 → 12 → 25 → 33.
- **eval**: 14 (review como mini-eval, introducción ligera) → 25 → 35 → 38.
- **hallucinated dependency**: 16 → 22 → 24 → 26.
- **context window**: 06 → 16 → 28 → 33.
- **TDD** *(nuevo en v2)*: 23 → 25 → 35 (golden datasets como tests glorificados) → 38 (gates).
- **spec-driven** *(nuevo en v2)*: 17–20 → 29 (sprint contracts como specs operativas) → 41 (playbook).

**Andragogía (Knowles)**. Parte I muestra cuánto sigue siendo levier y cuánto cambia. Cap. 21 ancla el riesgo con datos antes de pedir esfuerzo extra. Parte V valida lo que el developer experienced ya sabía hacer (escribir specs claras) y lo eleva a artefacto central. Cap. 17 diferencia explícitamente *spec ligera operacional* de *spec exhaustiva tipo waterfall* para neutralizar la resistencia ágil.

---

## Relación con la guía hermana (harness-engineering-guide)

| Solapamiento | Acción |
|---|---|
| Vocabulario (agent, harness, MCP, tool use, eval, drift, HITL, feedforward/feedback) | Glosario común. Caps. 27–32 citan la guía hermana como **profundización**, no la replican. |
| Datos sobre calidad de código IA (1.7×, 75 %, 322 %, 153 %) | Cap. 21 los introduce con muestra y limitación. La guía hermana puede tenerlos en versión más cruda. |
| Patrones del catálogo | Cap. 29 los **aplica** desde el lado del developer; la guía hermana los **diseña desde cero** desde el lado del builder. |
| Observabilidad y evals | Caps. 33–35 desde la silla del consumidor del log. Guía hermana desde la silla del builder. |
| Casos (Stripe, Shopify, Airbnb, Codex) | Cap. 40 cuenta cada caso con foco en **qué hizo el developer**. Guía hermana describe **qué construyó el equipo**. |

| Divergencia exclusiva de esta guía |
|---|
| Toda la Parte I (paradigma para developer experienced) |
| Toda la Parte II (prompt + context engineering, RAG) |
| Caps. 13–16 (workflow Willison con dos coding agents) |
| Caps. 21–26 (calidad desde la silla del revisor humano, prompt injection) |
| Cap. 34 (costo/latencia/caching desde lado consumidor) |
| Cap. 41 (playbook de adopción por equipo) |

---

## Archivos canónicos en raíz

`README.md`, `OUTLINE.md`, `STYLE.md`, `GLOSSARY.md`, `SOURCES.md`, `AGENTS.md` (+ symlink `CLAUDE.md`), `CONTRIBUTING.md`, `CHANGELOG.md`, `LICENSE` (CC-BY-SA 4.0), `/capitulos/parte-{N}-{slug}/cap-{NN}-{slug}.md`, `/plantillas/` (incluye `rubric-capitulo.md`, `agents-md-referencia.md`, `eval-rubrics/`, `prompt-templates/`), `/ejemplos/`.

---

## Convenciones

**Frontmatter por capítulo**:

```yaml
---
modalidad: explanation | how-to | reference | tutorial
archivo: cap-NN-slug
parte: N
tiempo_estimado: 20 min
prerrequisitos: [cap-03, cap-08]
herramientas: [gemini-code-assist, cline]   # solo si el capítulo las usa
caducidad: estable | revisar-trimestral     # nuevo en v2
es_repaso: false                             # nuevo en v2
validado: 2026-05
---
```

**Caducidad técnica**: nunca capturar versiones de modelos ni snapshots de UI en el cuerpo. Versiones viven en SOURCES.md con fecha de consulta y se revisan trimestralmente. Patrones (Willison, AGENTS.md, EARS) son atemporales; herramientas no.

**Bilingüismo**: español neutro en cuerpo. Términos en inglés cuando son nombres propios o jerga consolidada. Primera aparición en cursiva con definición seca; siguientes en redonda. Nunca traducción forzada (jamás "arnés", jamás "ventana de contexto" como sustituto canónico).

**STYLE.md gana sección "registro frente a developer senior escéptico"** *(nuevo en v2)*. Prohibiciones explícitas:
- "Imagina que…", "imaginate", "pensemos juntos".
- "Magic", "mágico", "increíble", "potente".
- "Let's dive in", "profundicemos", "vamos a explorar".
- Viñetas-explicativas-de-tres-puntos al inicio de sección (si hay 3 puntos, escribirlos en prosa).
- Apertura de capítulo con tesis genérica; siempre escena u objeto concreto.

---

## Glosario inicial (semilla, **30 términos** — reorganizado en v2)

**Núcleo del modelo** (8): prompt · context window · token · temperature (incluye sampling) · inference · system prompt · few-shot / zero-shot · chain-of-thought.

**Mecánica del agente** (5): tool use (function calling) · structured output · MCP (Model Context Protocol) · agent · agent loop (plan-act-observe) · harness.

**Datos y contexto** (5): RAG · golden dataset · **context reset** *(separado)* · **compaction** *(separado)* · **prompt caching** *(nuevo)*.

**Calidad y antipatterns** (8): hallucination (incluye hallucinated dependency) · refactoring avoidance · context blindness · shotgun surgery (variante IA) · reward hacking · drift · **prompt injection** *(nuevo)* · **jailbreak** *(nuevo)*.

**Disciplina** (8): AGENTS.md · vibe coding · spec-driven development · EARS notation · feedforward / feedback · generator-evaluator loop · sprint contract · HITL · eval.

**Cambios v2 vs v1**:
- **Quitado**: "builder harness vs user harness" (jerga interna del linaje, vive como nota en cap. 27).
- **Añadidos**: prompt injection, jailbreak, prompt caching.
- **Separados**: context reset (borrar) y compaction (resumir) — eran una sola entrada.

**Términos prohibidos**: "IA generativa" en titulares, "potente", "empoderar", "mágico", "arnés".

---

## Rutas de aprendizaje por perfil (**7 rutas** — reescritas en v2)

1. **"Vengo de backend tradicional, primer contacto serio con IA"**
   `01 → 02 → 03 → 04 → 05 → 06 → 07 → 08 → 10 → 13 → 14 → 21 → 22 → 23`
   *MCP y multi-agente saltados en primera pasada. Cap. 09 (RAG) opcional.*

2. **"Soy lead, necesito decidir tooling para mi equipo"**
   `02 → 04 → 21 → 12 → 19 → 20 → 13 → 22 → 27 → 28 → 36 → 37 → 41`
   *Cambio v2: añadidos cap. 13 (al menos una pasada al agente operando) y cap. 22 (antipatterns concretos). Sin estos, decide a ciegas.*

3. **"Quiero llegar a producción rápido (MVP aceptando deuda)"**
   `04 → 21 → 10 → 13 → 14 → 20 → 23 → 24 → 25 → 35 → 38`
   *Cambio v2: añadido cap. 21 al inicio. Sin internalizar el riesgo, prod rápido es vibe coding con esteroides. Renombrada para honestidad.*

4. **"Vengo de Cursor/Copilot pero sin método"**
   `04 → 08 → 14 → 16 → 20 → 22 → 23 → 25`
   *Cap. 23 (TDD) es la pieza que probablemente falta.*

5. **"Mi equipo ya genera con IA y la calidad bajó"**
   `21 → 22 → 23 → 24 → 25 → 32 → 28 → 35`
   *Triaje primero, reforma sistémica después con cap. 28 (feedforward/feedback).*

6. **"Quiero entender la disciplina a fondo"**
   Lee el OUTLINE.md y elige tu propio orden. La numeración 01 → 43 es válida pero no obligatoria; las dependencias en frontmatter son la guía dura.

7. **"Developer senior escéptico forzado por su empresa"** *(nueva en v2)*
   `01 → 21 → 04 → 16 → 22 → 39 → 41`
   *Crítica antes que promesa: empieza con qué del oficio sigue valiendo (01) y los datos incómodos (21), después ofrece el modo de adopción operacional (04, 16, 22), cierra con repaso y playbook (39, 41). Estimo 30 % del público real.*

> **Cambio v2**: ruta "a fondo" (antes 4) eliminada como ruta porque era la TOC; sustituida por "elige tu propio orden con dependencias". Nueva ruta 7 añade el perfil escéptico-forzado.

---

## Riesgos pedagógicos y mitigaciones (**12 riesgos**)

Heredados (1–7): confusión modelo/agente/herramienta/harness · sobrecarga en Parte III (mitigada en v2 por mover multi-agente a VII) · expectativas falsas · trampa del developer experienced · trampa de la herramienta única · moralina en cap. 21 · saturación bilingüe.

Añadidos en v1 (8–12):
8. Sesgo de autoridad invertido (developers que vienen a confirmar "no funciona").
9. Caducidad técnica (versiones de modelos y herramientas).
10. Falsa equivalencia entre coding agents (mitigado por elección con ejes opuestos).
11. Survivorship bias en datos del cap. 21 (cifras con muestra y limitación).
12. Falsa promesa de seguridad por static analysis (cap. 24 enfatiza "señal, no garantía").

> **Cambio v2**: el riesgo "resistencia al spec-driven" del v1 se mantiene cubierto en el cap. 17 (diferencia spec ligera vs waterfall) y se elimina como riesgo separado para no inflar la lista.

---

## Plan de ejecución por fases (**8 fases, 18–20 sesiones**)

| Fase | Alcance | Caps. | Sesiones | Notas |
|---|---|---|---|---|
| 0 | Esqueleto + decisiones cerradas | — | 1 | Archivos canónicos vacíos pero estructurados, GLOSSARY con 30 términos, plantilla de capítulo, rubric-capitulo.md, STYLE.md con sección senior escéptico, lectores piloto reclutados, dos coding agents instalados |
| 1 | Parte I + capítulo piloto | 02 (piloto), 01, 03, 04 | 2 | **Cap. 02 escrito primero como piloto**. Si pasa rubric y skill chain, calibra tono para los 42 restantes. Si no, recalibra STYLE.md antes de seguir |
| 2 | Partes II–III | 05–12 | 4 | 8 capítulos. Cierra cuando el lector puede explicar agent loop, tool use, MCP y RAG sin abrir el libro |
| 3 | Parte IV (tutorial doble herramienta) | 13–16 | 3 | 4 caps × 2 worked examples (Gemini Code Assist + Cline). **Kill switch v2**: si los 3 lectores piloto no completan el tutorial del cap. 13 con éxito sin asistencia, paro y rediseño Parte IV antes de Fase 4. No se avanza por inercia |
| 4 | Parte V | 17–20 | 2 | 4 capítulos |
| 5 | Parte VI (densa) | 21–26 | 3 | 6 capítulos densos. Verificar fuentes con muestra y limitación en cap. 21 |
| 6 | Parte VII | 27–32 | 2 | 6 capítulos. Citas explícitas a la guía hermana, sin replicar |
| 7 | Parte VIII | 33–38 | 2 | 6 capítulos. Validación con revisor con experiencia profesional en agentes al cierre |
| 8 | Parte IX + cierre | 39–43 | 2 | 5 capítulos + revisión cruzada de glosario, rutas, fuentes y enlaces internos |

**Total: 21 sesiones**. Si patrones se estabilizan agresivamente, posible 17–18.

**Kill switch (nuevo en v2)**: Fase 3 tiene checkpoint duro. Criterio: ≥ 2 de los 3 lectores piloto completan el tutorial del cap. 13 sin asistencia adicional. Si no, retorno a Fase 0 para revisar la elección de coding agents o el approach de Parte IV.

---

## Verification (**13 chequeos**)

1. **Estructura**: `ls -R guide-ai-developers/` muestra 9 directorios y **43** archivos `cap-NN-slug.md` con frontmatter válido.
2. **Frontmatter parseable**: cada capítulo tiene `modalidad`, `archivo`, `parte`, `tiempo_estimado`, `prerrequisitos`, `caducidad`, `es_repaso`, `validado`. Validable con `yq`.
3. **Glosario en uso**: cada término del GLOSSARY.md aparece al menos una vez en los capítulos; ningún término fuera del glosario se usa en cursiva-de-definición.
4. **Diátaxis declarada y cumplida**: la modalidad declarada coincide con la apertura. Banderas automáticas: "luego ejecutas" en reference, "es importante notar que" en tutorial.
5. **Rutas de aprendizaje navegables**: las 7 rutas del README enlazan sin enlaces rotos.
6. **Fuentes verificadas**: cada cita aparece en SOURCES.md con URL y fecha de consulta.
7. **Lectura cruzada por developer real (Fase 3)**: ≥ 2 de los 3 pilotos completan el tutorial del cap. 13 sin asistencia. **Si falla, kill switch activo**.
8. **Lectura por revisor con experiencia en IA (Fase 7)**: caps. 27–38 validados técnicamente.
9. **Skill chain por capítulo con variante por modalidad**: tutorial, how-to, reference y explanation pasan por la cadena correspondiente. Evidencia en commits o cabecera de versión.
10. **Test de coherencia inter-capítulos**: cada capítulo cita ≥ 1 cap. previo y prepara ≥ 1 futuro.
11. **Test de prerrequisitos honesto**: aplicado a caps. 03, 13, 21, 27 (puntos críticos). Lector que solo leyó los prereqs declarados debe poder seguir.
12. **Test de fuentes vivas**: al cierre de Fase 8, `curl -I` sobre todas las URLs de SOURCES.md. Muertas se anotan con archivo (`web.archive.org`).
13. **Test de variabilidad tonal entre modalidades** *(nuevo v2)*: muestra aleatoria de 1 capítulo de cada modalidad, leída en bloque, debe sentirse claramente distinta. Si los 4 suenan igual, la skill chain está homogeneizando y hay que ajustar variantes.

---

## Resumen de cambios v2 vs v1

| Área | v1 | v2 |
|---|---|---|
| Capítulos | 42 | **43** (+ costo/latencia/caching) |
| Reordenamiento | — | Multi-agente: Parte III → Parte VII (cap. 13 → cap. 30) |
| Modalidades corregidas | — | Cap. 09 explanation, cap. 29 how-to |
| Tiempos ajustados | — | Cap. 19: 25 → 15 min · cap. 36: 15 → 20 min |
| Spaced repetition | 5 hilos | **7 hilos** (+TDD, +spec-driven) |
| Glosario | 30 términos | 30 términos **reorganizados** (− builder/user harness, + prompt injection, jailbreak, prompt caching, split context reset/compaction) |
| Rutas | 6 | **7** (nueva: senior escéptico forzado; ruta "a fondo" reformulada) |
| Riesgos | 13 | **12** (consolidación: spec-driven cubierto en cap. 17) |
| Decisiones pre-Fase 1 | implícitas | **explícitas**: 2 coding agents (Gemini Code Assist + Cline), eval rubric, 3 pilotos + 1 revisor, Mermaid+ASCII, CC-BY-SA 4.0, skill chain con variantes |
| Kill switch | ausente | **Fase 3** tiene checkpoint duro |
| STYLE.md | tono general | **+ sección registro senior escéptico** con prohibiciones explícitas |
| Verification | 12 chequeos | **13** (+ variabilidad tonal entre modalidades) |
