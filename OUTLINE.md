# OUTLINE.md — Índice canónico

> Tabla maestra de los 43 capítulos. Cualquier reorganización pasa por aquí. Plan curricular completo en [`PLAN.md`](./PLAN.md).

**Total**: 43 capítulos en 9 partes · ≈ 945 min declarados (15.75 h) · 17–18 h realistas para developers en primer contacto.

---

## Parte I — De Software 1.0 a Software 3.0 (anclaje)

*Diátaxis: explanation. Romper expectativas falsas y construir modelo mental.*

| # | Título | Modalidad | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 01 | Lo que tu experiencia ayuda y lo que te traiciona | explanation | 12 min | — | Identificar qué del oficio sigue siendo levier (refactor, tests, tipos, code review) y qué cambia |
| 02 | Software 3.0 en una página | explanation | 18 min | 01 | Situar a Karpathy: modelo como runtime, prompt como código, datos como dependencia |
| 03 | Anatomía de un LLM para developers | explanation | 25 min | 02 | Vocabulario mínimo: tokens, weights, sampling, temperature, inference, context window |
| 04 | Vibe coding vs structured AI development | explanation | 15 min | 02 | Distinguir modo exploratorio de modo producción y declarar dónde vive cada uno |

**Subtotal**: 70 min.

---

## Parte II — Conversar con el modelo (prompt → context engineering)

*Diátaxis: reference + how-to + explanation. Base operativa.*

| # | Título | Modalidad | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 05 | Prompt como interfaz, no como conjuro | how-to | 25 min | 03 | Estructurar prompts con criterio de ingeniería |
| 06 | Context window y la atención del modelo | reference | 25 min | 05 | Decidir qué meter, qué dejar fuera, dónde colocarlo |
| 07 | Few-shot, system prompts y plantillas | how-to | 20 min | 05, 06 | Calibrar comportamiento con ejemplos y system prompts reusables |
| 08 | De prompt engineering a context engineering | explanation | 18 min | 06, 07 | El problema real es gobernar el contexto, no afinar la frase |
| 09 | RAG: cuándo el contexto vive fuera del prompt | explanation | 25 min | 08 | Distinguir RAG ligero (lookup) de RAG pesado (retrieval system); decidir cuándo añadir vectores y cuándo no |

**Subtotal**: 113 min.

---

## Parte III — El loop de un agente (tool use, MCP)

*Diátaxis: explanation + reference. Multi-agente movido a Parte VII.*

| # | Título | Modalidad | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 10 | Tool use: el modelo aprende a llamar funciones | explanation | 25 min | 09 | Contrato de function-calling, structured output, qué amplía y qué no |
| 11 | El loop básico: plan, act, observe | explanation | 20 min | 10 | Modelar un agente como bucle con estado y criterios de parada |
| 12 | MCP, el USB-C de los agentes | reference | 25 min | 10 | Qué resuelve Model Context Protocol, cuándo merece la pena, cuándo no |

**Subtotal**: 70 min.

---

## Parte IV — Trabajo asistido en el día a día (worked example)

*Diátaxis: tutorial. Recorrido en primera persona, replicado en **Gemini Code Assist + Cline**.*

| # | Título | Modalidad | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 13 | Setup: repo, agente y primer prompt útil | tutorial | 30 min | 04, 07 | Arrancar repo nuevo con un agente y obtener primer cambio revisable |
| 14 | El workflow Willison: especificar, seguir, revisar | tutorial | 25 min | 13 | Aplicar las tres fases sin perder control; introducir review como mini-eval |
| 15 | Refactor con agente: pequeño, verificable, reversible | tutorial | 30 min | 14 | Guiar refactors graduales con tests como red de seguridad |
| 16 | Cuando el agente se atasca: diagnóstico y rescate | how-to | 20 min | 14 | Reconocer síntomas (loops, hallucinated deps, context blindness) y salir |

**Subtotal**: 105 min.

---

## Parte V — Specs como código (spec-driven development)

*Diátaxis: explanation + how-to.*

| # | Título | Modalidad | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 17 | Por qué la especificación es el nuevo código fuente | explanation | 18 min | 12, 15 | Argumentar la spec como levier sin caer en waterfall regresivo |
| 18 | EARS: requisitos que un agente puede ejecutar | reference | 20 min | 17 | Escribir requisitos en notación EARS sin ambigüedad |
| 19 | Frameworks: Kiro, Spec Kit, BMAD-METHOD | reference | 15 min | 17 | Comparar enfoques sin sectarismo. **Snapshot 2026; revisar trimestralmente** |
| 20 | AGENTS.md: el contrato de tu repo | how-to | 25 min | 13, 18 | AGENTS.md operativo (≤150 líneas, 6 áreas core, ejemplos sobre abstracciones) |

**Subtotal**: 78 min.

---

## Parte VI — Calidad cuando el código no lo escribiste tú

*Diátaxis: how-to + reference + explanation. Aquí va la evidencia dura.*

| # | Título | Modalidad | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 21 | El número incómodo: qué dicen los datos sobre código IA | explanation | 20 min | 15 | Internalizar la magnitud del riesgo (1.7× bugs, 75 % logic, 1.5–2× security) con muestra y limitación |
| 22 | Code review específico para AI: los seis antipatterns | how-to | 30 min | 21 | Detectar refactoring avoidance, context blindness, shotgun surgery, hallucinated dependencies |
| 23 | Tests antes que código: TDD reescrito para agentes | how-to | 25 min | 22 | Pedir tests primero, ejecutarlos rojos, dejar al agente implementar para verde |
| 24 | Static analysis y type systems como sensores | reference | 20 min | 22 | Configurar el feedback determinista que un agente sí respeta; advertencia: feedback ≠ garantía |
| 25 | Adversarial AI review: un agente revisa al otro | how-to | 25 min | 23, 24 | Montar un revisor LLM con rúbrica calibrada y few-shot |
| 26 | Seguridad: secrets, dependencies, prompt injection, privilege escalation | how-to | 25 min | 22 | Cerrar vectores inflados (322 % privilege, 153 % architectural) + prompt injection y jailbreak |

**Subtotal**: 145 min.

---

## Parte VII — Harness engineering aplicado

*Diátaxis: reference + explanation + how-to. Cita explícita de la guía hermana en cada capítulo.*

| # | Título | Modalidad | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 27 | Agent = Model + Harness | explanation | 15 min | 25 | Aceptar la fórmula y por qué el harness gap pesa más que el model gap |
| 28 | Feedforward y feedback en tu repo | reference | 25 min | 27 | Catalogar guides (AGENTS.md, skills, MCP) y sensors (tests, lints, jueces) |
| 29 | Patrones del catálogo: generator-evaluator, sprint contracts, context reset | how-to | 30 min | 28 | Aplicar los patrones más rentables sin replicar la guía hermana |
| 30 | Topologías multi-agente | explanation | 25 min | 28 | Distinguir planner-coder-reviewer, generator-evaluator, supervisor-worker |
| 31 | HITL: dónde, cómo y cuándo no | how-to | 20 min | 28 | Diseñar puntos de intervención humana sin convertirlos en cuello de botella |
| 32 | Drift: cómo detectarlo antes de que duela | how-to | 20 min | 28 | Señales tempranas de desviación de convenciones |

**Subtotal**: 110 min.

---

## Parte VIII — Producción: observabilidad, evals, decisión

*Diátaxis: reference + explanation + how-to.*

| # | Título | Modalidad | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 33 | Observabilidad de agentes: logs, traces, eval runs | reference | 25 min | 29 | Instrumentar un agente como instrumentas un servicio |
| 34 | Costo, latencia y prompt caching | reference | 25 min | 33 | Tokens cobrados, throughput, KV-cache, decisiones operacionales |
| 35 | Eval pipelines y golden datasets | how-to | 30 min | 25, 33 | Construir y mantener dataset de referencia y pipeline de regresión |
| 36 | Métricas y ROI: cuándo el harness vale la pena | explanation | 20 min | 33, 34 | Justificar la inversión con números (lectura de lead) |
| 37 | Risk tiering y compliance ligero (NIST AI RMF, ISO 42001) | reference | 20 min | 31, 36 | Clasificar usos por riesgo y aplicar controles proporcionales |
| 38 | Despliegue con gates de eval pre-merge | how-to | 20 min | 35 | Ningún cambio entra sin pasar el eval |

**Subtotal**: 130 min.

---

## Parte IX — Síntesis y rutas adelante

| # | Título | Modalidad | Tiempo | Prereq | Objetivo |
|---|---|---|---|---|---|
| 39 | Antipatterns globales: 12 trampas (repaso espaciado) | explanation | 20 min | 21–38 | Revisión consolidada con vocabulario completo, **declarado como repaso** |
| 40 | Casos comentados: Stripe, Shopify, Airbnb, Codex | explanation | 30 min | 27–36 | Ver harnesses reales y nombrarlos desde la silla del *developer* |
| 41 | Tu propio playbook: plantilla de adopción por equipo | how-to | 25 min | 20, 31, 35 | Salir con un plan concreto de adopción por sprint |
| 42 | Glosario navegable y mapa de fuentes | reference | consulta | — | Material de consulta permanente |
| 43 | Hacia dónde mirar: spec-first, agentic IDEs, autonomous teams | explanation | 15 min | todo | Cierre seco con punteros, sin moralejas |

**Subtotal**: 90 min.

---

## Hilos de spaced repetition

Cada concepto pesado se revisita al menos tres veces, con separación creciente.

| Concepto | Capítulos donde aparece |
|---|---|
| `AGENTS.md` | 13 → 20 → 28 → 41 |
| `tool use` | 10 → 12 → 25 → 33 |
| `eval` | 14 → 25 → 35 → 38 |
| `hallucinated dependency` | 16 → 22 → 24 → 26 |
| `context window` | 06 → 16 → 28 → 33 |
| `TDD` para agentes | 23 → 25 → 35 → 38 |
| `spec-driven` | 17–20 → 29 → 41 |

---

## Modalidad Diátaxis: distribución

| Modalidad | Capítulos | Total |
|---|---|---|
| `explanation` | 01, 02, 03, 04, 08, 09, 10, 11, 17, 21, 27, 30, 36, 39, 40, 43 | 16 |
| `how-to` | 05, 07, 16, 20, 22, 23, 25, 26, 29, 31, 32, 35, 38, 41 | 14 |
| `reference` | 06, 12, 18, 19, 24, 28, 33, 34, 37, 42 | 10 |
| `tutorial` | 13, 14, 15 | 3 |

---

## Estado por capítulo

(Esta tabla se actualiza fase a fase. Estado actual: **0 / 43 escritos**, **Fase 0** en curso.)

| Estado | Capítulos |
|---|---|
| 📅 Planificado | 01–43 |
| ✏️ En escritura | — |
| 🔍 En revisión | — |
| ✅ Validado | — |
