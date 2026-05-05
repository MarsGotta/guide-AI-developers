# GLOSSARY.md — Términos canónicos

> 30 términos en 5 grupos. Cada término tiene una sola forma canónica. La primera aparición en cualquier capítulo va en cursiva con la definición seca de aquí.

---

## Grupo 1 — Núcleo del modelo (8)

### `prompt`
Entrada de texto que se envía a un LLM para que genere una respuesta. Incluye instrucción, contexto y ejemplos opcionales.

### `context window`
Cantidad máxima de tokens que un modelo puede procesar en una sola inferencia. Define qué cabe en la "memoria de trabajo" del modelo.

### `token`
Unidad mínima de texto que un modelo procesa. Aproximadamente 4 caracteres o 0.75 palabras en inglés.

### `temperature`
Parámetro que controla la aleatoriedad del muestreo en la generación. 0 = determinista, valores altos = más creativo y menos predecible. Incluye los conceptos relacionados de `top_p` y `top_k`.

### `inference`
Proceso de generar una respuesta a partir de un prompt en un modelo entrenado. Es runtime, no entrenamiento.

### `system prompt`
Prompt de nivel superior que define rol, restricciones y comportamiento del modelo durante toda la conversación. Persiste mientras los `prompt` de usuario cambian.

### `few-shot` / `zero-shot`
Estrategia de prompting con (`few-shot`) o sin (`zero-shot`) ejemplos resueltos en el prompt. Los ejemplos calibran el formato y el comportamiento esperado.

### `chain-of-thought`
Técnica que pide al modelo explicitar pasos intermedios de razonamiento antes de la respuesta final. Aumenta calidad en tareas complejas, encarece tokens.

---

## Grupo 2 — Mecánica del agente (5)

### `tool use`
Capacidad de un LLM de invocar funciones externas declaradas con un schema. También se llama `function calling`. Convierte el modelo en algo más que un generador de texto.

### `structured output`
Salida del modelo forzada a un schema (JSON, XML, etc.). Garantía de forma, no de contenido.

### `MCP`
Model Context Protocol. Estándar abierto para conectar agentes con herramientas, recursos y prompts externos. El "USB-C" de los agentes.

### `agent`
Sistema que usa un LLM en un bucle con `tool use` para alcanzar un objetivo. No es solo un prompt; tiene estado y criterios de parada.

### `agent loop`
Bucle plan → act → observe que ejecuta un `agent`. Plan: el modelo decide qué hacer. Act: invoca una tool. Observe: el output vuelve al contexto.

### `harness`
Infraestructura alrededor de un modelo que lo hace fiable en producción. Incluye `feedforward` (guías de qué hacer) y `feedback` (sensores de qué pasó). El `harness gap` pesa más que el `model gap`.

---

## Grupo 3 — Datos y contexto (5)

### `RAG`
Retrieval-Augmented Generation. Estrategia de inyectar contexto recuperado de una fuente externa (vector store, base de datos) en el prompt antes de la inferencia. Distinguir RAG ligero (lookup) de RAG pesado (retrieval system).

### `golden dataset`
Conjunto de pares input–output esperados que sirve de referencia para evaluar regresión de un agente o prompt. Es el equivalente a tests para sistemas LLM.

### `context reset`
Reiniciar el contexto del agente desde cero, descartando la conversación anterior. Útil cuando el contexto está contaminado o sobrepoblado.

### `compaction`
Comprimir el contexto resumiendo lo previo, no descartándolo. Mantiene continuidad pero pierde detalle.

### `prompt caching`
Reutilizar partes prefijadas de un prompt entre llamadas para abaratar tokens y reducir latencia. La provider implementa el cache; tú decides qué prefijar.

---

## Grupo 4 — Calidad y antipatterns (8)

### `hallucination`
Output del modelo que afirma algo falso o inventado con apariencia de verdad. Sub-tipo crítico: `hallucinated dependency` (paquete o función que no existe).

### `refactoring avoidance`
Antipattern donde el agente añade código en vez de reorganizar el existente, aunque la solución correcta sea refactor.

### `context blindness`
Antipattern donde el agente ignora archivos o convenciones del repo que no están en su contexto inmediato.

### `shotgun surgery` (variante IA)
Antipattern donde el cambio toca muchos archivos por copia y pega del agente. Hace casi imposible revisar y mantener.

### `reward hacking`
Comportamiento del modelo que optimiza la métrica visible (tests verdes, lint pasado) sin cumplir el objetivo real.

### `drift`
Desviación gradual del agente respecto a las convenciones del repo o las preferencias declaradas. Detectable solo con sensores.

### `prompt injection`
Vector de ataque donde un input externo (web, archivo, output de tool) inyecta instrucciones que cambian el comportamiento del agente.

### `jailbreak`
Vector de ataque donde el atacante usa el `prompt` directo para bypassear las restricciones del system prompt o las guardrails del modelo.

---

## Grupo 5 — Disciplina (8)

### `AGENTS.md`
Archivo en la raíz del repo que documenta para el agente: comandos, tests, estructura, estilo, git workflow y boundaries. Convención abierta de la industria. Máximo recomendado: 150 líneas.

### `vibe coding`
Modo de desarrollo donde se prompt-ea sin revisar el código generado. Útil para prototipos exploratorios; no escala a producción.

### `spec-driven development`
Disciplina donde la especificación es el código fuente: el agente la implementa, los tests la verifican, los humanos la mantienen. Frameworks: Kiro, Spec Kit, BMAD-METHOD.

### `EARS notation`
Easy Approach to Requirements Syntax. Notación para escribir requisitos sin ambigüedad: `When <trigger>, the <system> shall <response>`.

### `feedforward` / `feedback`
Dos ejes del `harness`. Feedforward: guías que el agente lee antes de actuar (AGENTS.md, skills, MCP). Feedback: sensores que evalúan lo que produjo (tests, lints, jueces LLM).

### `generator-evaluator loop`
Patrón donde un agente genera y otro evalúa, iterando hasta que el evaluador aprueba. Variante simple del adversarial review.

### `sprint contract`
Acuerdo escrito al inicio de un sprint sobre qué hace y qué no hace el agente, con criterios de aceptación. Es la spec operativa del sprint.

### `HITL`
Human In The Loop. Punto del flujo del agente donde un humano revisa, aprueba o corrige. Usado en: cambios destructivos, decisiones arquitectónicas, output con riesgo legal.

### `eval`
Pipeline o instancia que mide la calidad de un agente o prompt contra un `golden dataset` o rúbrica. Es el test del sistema LLM.

---

## Términos prohibidos

No usar en cuerpo ni titulares:

- **"IA generativa"** en titulares (en cuerpo solo si distingue de discriminativa).
- **"potente"**, **"empoderar"**, **"mágico"**, **"increíble"**, **"revolucionario"**.
- **"arnés"** (siempre `harness`, en redonda tras primera aparición).
- **"ventana de contexto"** como sustituto canónico de `context window` (sí como aclaración una sola vez).
- **"última generación"**, **"de vanguardia"**, **"state-of-the-art"** sin fecha de consulta.
- **"experto"** referido a un humano sin nombre y fuente.

---

## Convención de añadidos

Cuando un capítulo necesita un término nuevo:

1. Añadir aquí, en su grupo, con definición seca.
2. Marcar primera aparición en el capítulo en cursiva.
3. Reportar en el `CHANGELOG.md` del manual.

No se introduce un término en cursiva-de-definición que no esté aquí.
