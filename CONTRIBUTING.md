# CONTRIBUTING.md — Cómo proponer correcciones

Gracias por leer la guía. Si encontraste algo que mejorar, hay tres caminos según el tipo de cambio.

---

## 1. Errata o ajuste menor

Errores tipográficos, enlaces rotos, fechas desactualizadas, ejemplos de código que no compilan.

**Cómo**:
- Abre un issue describiendo el problema y la página/capítulo afectados.
- O abre directamente una PR con el fix. No necesitas avisar antes.

---

## 2. Cambio de contenido en un capítulo

Reformulación de un párrafo, corrección de una afirmación, adición de un ejemplo, sustitución de una fuente.

**Cómo**:
- Issue primero, describiendo el cambio y la justificación.
- Si la justificación incluye un dato, viene con fuente y URL.
- Si Marcela aprueba en el issue, abre PR con:
  - El cambio.
  - Frontmatter del capítulo actualizado (si toca `tiempo_estimado`, `validado` o `prerrequisitos`).
  - Actualización de `GLOSSARY.md` si el cambio introduce un término canónico.
  - Actualización de `SOURCES.md` si el cambio introduce una fuente.

---

## 3. Cambio estructural

Añadir un capítulo, eliminar uno, mover capítulos entre partes, cambiar la modalidad Diátaxis declarada de un capítulo, o tocar las rutas de aprendizaje del `README.md`.

**Cómo**:
- Issue primero. Estos cambios pasan por revisión explícita de Marcela porque tocan `PLAN.md` y `OUTLINE.md`.
- Espera aprobación antes de abrir PR.
- En la PR: actualizar `PLAN.md`, `OUTLINE.md`, `README.md`, `CHANGELOG.md` y los archivos afectados de capítulos en una sola PR.

---

## Convenciones para PRs

- **Idioma**: español en cuerpo de issue/PR. Inglés solo en términos canónicos del `GLOSSARY.md`.
- **Mensaje de commit**: imperativo, presente. `corrige enlace roto en cap-12`, `actualiza fecha de consulta en SOURCES`.
- **Skill chain**: si la PR toca prosa de un capítulo, debe haber pasado por la skill chain correspondiente (ver `STYLE.md` sección 10). Indícalo en la descripción de la PR.
- **Frontmatter**: si tocas un capítulo, actualiza `validado: YYYY-MM` a la fecha del cambio.

---

## Reportar un problema sin proponer solución

Si viste algo que te chirría pero no sabes cómo arreglarlo, abre el issue de todas formas. Describe qué viste, qué esperabas, y dónde. Es más útil eso que el silencio.

Issues tipo "esto no me convenció" son bienvenidos también, siempre que digas concretamente qué no te convenció.

---

## Lo que no aceptamos

- PRs que añaden contenido sin pasar por issue previo (excepto erratas obvias).
- Cambios masivos de estilo automáticos sin contexto pedagógico.
- Traducciones forzadas de términos canónicos del `GLOSSARY.md`.
- Adiciones de capítulos motivadas por "este tema también es interesante" sin justificación curricular.
- Cualquier cambio que viole prohibiciones explícitas del `STYLE.md` (mayúsculas para énfasis, "imagina que…", emojis decorativos, etc.).

---

## Licencia

Al contribuir aceptas que tu aporte se publique bajo CC-BY-SA 4.0, igual que el resto del manual.
