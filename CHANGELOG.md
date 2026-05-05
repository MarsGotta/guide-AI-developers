# CHANGELOG

> Versiones del manual. Formato: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versiones siguen [SemVer](https://semver.org/) adaptado: `MAJOR.MINOR.PATCH` donde MAJOR cambia con reorganización estructural, MINOR con capítulos nuevos, PATCH con correcciones.

---

## [Unreleased]

### Pendiente
- Caps. 01–43: ninguno escrito todavía.
- Plantillas en `plantillas/` por crear.
- Implementar scripts de validación (`yq` frontmatter, `curl -I` URLs).

---

## [0.1.0] — 2026-05-05

### Añadido — Esqueleto Fase 0
- `README.md` con introducción, mapa de partes y 7 rutas de aprendizaje por perfil.
- `OUTLINE.md` con índice canónico de los 43 capítulos en 9 partes, modalidad Diátaxis y prerrequisitos por capítulo. Incluye hilos de spaced repetition y distribución de modalidades.
- `STYLE.md` con voz, registros por modalidad Diátaxis (4 variantes), sección "registro frente a developer senior escéptico" con prohibiciones explícitas, convenciones tipográficas y bilingüismo.
- `GLOSSARY.md` con 30 términos canónicos en 5 grupos (Núcleo del modelo, Mecánica del agente, Datos y contexto, Calidad y antipatterns, Disciplina) más términos prohibidos.
- `SOURCES.md` con bibliografía inicial en 12 secciones, todas las fuentes con URL y fecha de consulta. Pendientes de verificación declarados.
- `AGENTS.md` con contrato operativo del agente que escribe el manual: persona, comandos, estructura, flujo de escritura, boundaries, tech stack.
- `CLAUDE.md` como symlink a `AGENTS.md`.
- `CONTRIBUTING.md` con tres caminos para aportes: errata, cambio de contenido, cambio estructural.
- `LICENSE` CC-BY-SA 4.0.
- `.gitignore` mínimo.
- Estructura de directorios `/capitulos/parte-{1..9}-{slug}/` y `/plantillas/eval-rubrics/`, `/plantillas/prompt-templates/`, `/ejemplos/`.

### Decisiones registradas
- Plan curricular v2 aprobado por la usuaria (43 capítulos, 9 partes, ~17 h lectura).
- Coding agents para Parte IV: **Gemini Code Assist + Cline** (free-tier sin tarjeta verificado mayo 2026).
- Diagramas: Mermaid embebido por defecto, ASCII como fallback, SVG embebido prohibido.
- Licencia: CC-BY-SA 4.0.
- Skill chain con variantes por modalidad Diátaxis.

### Notas
- Próxima fase (Fase 1): escribir `plantillas/cap-NN-template.md` y `plantillas/rubric-capitulo.md`, luego cap. 02 como piloto.
- Pilotos por reclutar: 3 developers con perfil objetivo + 1 revisor con experiencia en agentes para Fase 7.
