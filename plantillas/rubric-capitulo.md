# rubric-capitulo.md — Criterios objetivos por capítulo

> Cada capítulo, antes del commit final, pasa este rubric. Los 8 criterios son binarios (pasa/no pasa). Si falla uno, vuelve al paso 2 del flujo (ver `AGENTS.md`).

---

## Cómo se aplica

1. Lee el capítulo de principio a fin sin saltarte nada.
2. Para cada criterio, marca pasa o no pasa.
3. Si todos pasan, commit con mensaje incluyendo evidencia de la skill chain.
4. Si alguno no pasa, regresa al paso 2 del flujo de escritura (ver `AGENTS.md`).

---

## Los 8 criterios

### 1. Frontmatter completo y modalidad coherente con apertura

- [ ] Todos los campos del frontmatter están presentes y son válidos.
- [ ] La `modalidad` declarada coincide con el registro de la apertura:
  - `tutorial` → narración paso a paso, primera persona plural, presente.
  - `how-to` → imperativo, instrucciones, sin preámbulo.
  - `reference` → catálogo, prosa mínima, tablas o listas.
  - `explanation` → tesis, contraste, argumento.
- [ ] `tiempo_estimado` es realista (20–30 % menos que un primer borrador suele estimar).
- [ ] `validado: YYYY-MM` actualizado a la fecha del commit.

### 2. Apertura concreta en las 3 primeras líneas

- [ ] Las primeras 3 líneas presentan **escena, objeto o dato**, no tesis genérica.
- [ ] No empieza con "imagina que…", "en este capítulo veremos", "como developers sabemos…", "la inteligencia artificial está cambiando…".
- [ ] Si es `tutorial`, la escena tiene archivo concreto, comando o output visible.
- [ ] Si es `explanation`, abre con tensión (contraste, dato incómodo, pregunta concreta).

### 3. Una unidad nueva por sub-sección (CLT)

- [ ] Cada sub-sección introduce un solo concepto canónico nuevo, no dos.
- [ ] Reuso explícito: si el capítulo usa un concepto del cap. anterior, lo dice ("vimos en cap. XX que…").
- [ ] Si la `densidad` es `alta`, está declarada en frontmatter y advertida en cabecera.
- [ ] Hay worked example completo en cada paso de tutorial.

### 4. Cada cursiva-de-definición está en GLOSSARY.md

- [ ] Toda primera aparición de un término en cursiva tiene la definición exacta del `GLOSSARY.md`.
- [ ] No hay cursivas-de-definición de términos que no están en el glosario.
- [ ] Siguientes apariciones del término están en redonda, sin cursiva, sin redefinir.
- [ ] Términos prohibidos del glosario no aparecen (salvo en sección explícita de prohibiciones).

### 5. Cierre seco

- [ ] El capítulo cierra con una de las tres formas válidas: instrucción accionable, pregunta abierta concreta, o bisagra al siguiente.
- [ ] No hay moralina ("¡Ya tienes las herramientas!"), no hay emoji, no hay "espero que hayas disfrutado".
- [ ] Si es `how-to` o `tutorial`, el cierre tiene una instrucción que el lector puede ejecutar antes del siguiente capítulo.

### 6. Cada cita tiene URL + fecha en SOURCES.md

- [ ] Toda afirmación numérica viene con `(Apellido año, ver SOURCES.md)` o equivalente.
- [ ] Toda fuente citada está en `SOURCES.md` con URL, fecha de consulta y capítulos que la citan.
- [ ] Si la fuente tiene caducidad técnica (versión, herramienta), está marcada como `revisar-trimestral`.
- [ ] Si la fuente es la guía hermana, usa el formato `[harness-eng-guide §parte.cap]`.

### 7. Prerrequisitos honestos

- [ ] Los `prerrequisitos` del frontmatter son los capítulos cuyos conceptos se usan, no los que el lector "debería haber leído por completitud".
- [ ] Un lector que solo leyó los prereqs declarados puede seguir el capítulo sin perderse.
- [ ] Si el capítulo usa un concepto sin haberlo introducido y sin estar en prereqs, se añade a prereqs o se reformula.

### 8. Skill chain ejecutado en orden con evidencia

- [ ] El capítulo pasó por `technical-guide-design` (estructura).
- [ ] Pasó por `spanish-prose-craft` con la variante de registro correspondiente a la modalidad.
- [ ] Pasó por `humanizer` (o `humanizer-light` para reference).
- [ ] El commit message incluye: `cap-NN: write + tgd + spc(<registro>) + humanizer`.

---

## Caso especial: capítulos `es_repaso: true`

Cap. 39 (12 trampas) está marcado como repaso espaciado. Su rubric ajusta:

- **Criterio 3** se relaja: puede tocar varios conceptos por sección porque está consolidando, no introduciendo.
- **Criterio 4** sigue activo: las cursivas-de-definición se reservan para términos que el lector pudo olvidar y se reintroducen explícitamente.
- **Criterio 7** sigue activo, pero el prereq listado es "21–38" como bloque.
- En el frontmatter, `es_repaso: true` debe estar declarado y la cabecera del capítulo lo dice también.

---

## Caso especial: capítulos con `caducidad: revisar-trimestral`

Cap. 19 (frameworks), cap. 33 (observabilidad), cap. 34 (costo/latencia/caching) tratan de herramientas o métricas que cambian rápido.

- **Criterio 6** se refuerza: cada herramienta nombrada tiene fuente con fecha de consulta visible.
- En el cuerpo no aparecen versiones de modelos ni snapshots de UI.
- En la cabecera del capítulo se anuncia: "Snapshot 2026-MM. Revisar trimestralmente."

---

## Variabilidad tonal entre modalidades

Verificación cruzada al cierre de cada parte:

- Toma un capítulo `tutorial`, uno `how-to`, uno `reference` y uno `explanation` recientes.
- Léelos en bloque.
- Si los cuatro suenan iguales, la skill chain está homogeneizando. Ajusta los registros de `spanish-prose-craft` antes de seguir.
