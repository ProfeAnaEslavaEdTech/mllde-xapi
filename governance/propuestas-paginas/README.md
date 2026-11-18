# Propuestas de actualización de las páginas publicadas · 12 nov 2026

`index.html` y `tk-coachai-mllde.html`, en `main`, son el anexo publicado y no se tocan aquí. Esta carpeta guarda las versiones corregidas para que la autora las revise. Solo pasan a `main` con su visto bueno, después de comprobar qué cita el artículo.

## 1. `tk-coachai-mllde.html` → copia corregida en esta carpeta

Doce frases cambian (seis en español y sus seis equivalentes en inglés). El resto de la página no cambia.

| Lo que decía (5 nov) | Lo que dice | Por qué |
|---|---|---|
| «Evaluador v2: descriptor, estado, turno y cita literal, sin notas…», presentado como el flujo actual | «Evaluador v2 (en validación; hoy sigue midiendo el v1): …» | **Principio de verificación.** El Evaluador v2 no está en producción. En el export del 11 nov, `score.raw` coincide con la nota global de la IA en 127 de 127 `completed` |
| «Una persona docente decide el nivel, fuera del sistema» · «La promoción la decide una persona docente» | «El progreso queda a nombre del alumno y una persona docente valida el nivel fuera de la app» | **G-NIVEL-1 (11 nov):** el `progressed` lleva siempre al alumno como actor; la validación del profesor es externa a la app y no entra en la LRS |
| «una persona decide» | «una persona valida» | El mismo cambio, en el lema «la IA mide, el código gobierna, una persona…» |
| (panel del profesor) «decide la promoción fuera del sistema» | «valida el nivel fuera de la app, con otra evaluación» | G-NIVEL-1: el profesor constata el nivel con otra evaluación, oral y escrita |

**Lo que no se cambia y queda pendiente de la autora:** la página nombra a Talketika y a Orkelia (Q21, autorización por escrito).

### 1b. Actualización del 18 nov 2026 (normas v1.7)

La copia de esta carpeta se actualiza con las decisiones posteriores al 12 nov. **`main` no cambia.** La página publicada en `main` es la del 5 nov (`b5b17f8`). La que circula con las cifras del piloto («2.536 sentencias», «106/106», «≥ 80 h») es anterior a esa, y no se usa.

| Lo que decía (12 nov) | Lo que dice (18 nov) | Por qué |
|---|---|---|
| «Evaluador v2 (en validación; hoy sigue midiendo el v1)» | «Evaluador v2 (diseñado, pendiente de implementar; hoy mide el v1)» | **Principio de verificación.** El v2 no está implementado. Plan del 18 nov: primero el código, luego el modo sombra y la activación |
| «una persona docente valida el nivel» | «una persona valida el nivel: el profesor en B2B; en B2C, el propio usuario tras ver su evidencia» | Decisión de nivel en B2C (v1.5) y G-NIVEL-1 (11 nov) |
| (modal 1) «El nivel lo valida una persona docente» | «El nivel lo valida una persona. Ningún agente decide, sea cual sea el modelo» | Principio de invariancia del rol (10 nov) |
| (modal 2) «(El panel ya muestra la banda, no el %.)» | Se quita | No tiene sus tres pruebas |
| (modal 4) «Prueba en vivo: 10 statements… se detectaron y excluyeron» | «Las sesiones medidas por un proveedor de respaldo se detectaron gracias a measure-model. Su salida de las medias queda pendiente de sus tres pruebas. Desde ahora, sin modelo de respaldo» | La exclusión «parece aplicada» en el cotejo del 18 nov, pero le faltan el extracto del código y la fecha (P13) |
| «La IA mide» · «el modelo que la midió» · «hoy mide el v1» | «La IA compara» · «el modelo que hizo la comparación» · «hoy funciona el v1» | **Decisión de Ana (18 nov):** ningún agente de IA mide, valora ni evalúa. Compara el texto de la voz con el knowledge base y localiza cuántos descriptores se cumplen; el código cuenta y calcula |
| Cabecera con degradado | Cabecera sobria, como el portafolio | Regla de diseño de la autora (12 nov): minimalista, Ocean Ink |
| — | Nota al pie: «Actualizado el 18 nov 2026, con las normas de gobernanza v1.7» | Fecha desde la que rige |

**Sigue pendiente de la autora:** la página nombra a Talketika y a Orkelia (Q21). Para el congreso hace falta una versión sin nombres, o su autorización por escrito.

## 2. `index.html` (registro y perfil v0.8.3)

### 2a. Rediseño sin cambio de contenido → copia en esta carpeta (12 nov) · **publicado en `main` el 18 nov** (commit `9523cd6`, con el visto bueno de la autora, para el congreso). La versión anterior sigue en el historial de git (`b5b17f8`)

Aplica la regla de diseño de la autora: ES/EN, modo claro y oscuro, WCAG 2.1 AA, Ocean Ink y el estilo minimalista del portafolio.

**El contenido no cambia.** Comprobado sobre el archivo: 8 de 8 verbos de ADL, 382 de 382 filas del inventario, las 17 anclas originales y las mismas IRIs. La de más es la repetición en inglés de la introducción.

**Cambian el idioma de la interfaz y los títulos.** El contenido normativo (IRIs, definiciones y descriptores) queda en su idioma original en las dos versiones.

~~**Por revisar antes de pasarla a `main`:**~~ *revisado el 18 nov:*
- la traducción al inglés de las 15 etiquetas de categoría del inventario;
- «Etiqueta» como cabecera de la columna «Label» en español.

### 2c. Dos secciones nuevas: «Normas de gobernanza» y «Agentes involucrados» (18 nov 2026, petición de la autora)

La copia de `index.html` de esta carpeta añade al final, después del inventario, dos secciones con el mismo diseño (ES/EN, claro y oscuro, tablas que se apilan en el móvil) y dos entradas en el índice:
- **Normas de gobernanza (v1.7):** los 5 principios (rector, terminología, verificación, invariancia del rol y conservación del registro) y 23 reglas en una línea cada una (R-MED-1, N1–N13 con N6-bis y N6-ter, G-NIVEL-1, P1–P6, R-ADM, R-ID, vocabulario, OCR y el guardián). Enlaza al texto completo, `governance/html/normas-gobernanza.html`.
- **Agentes involucrados (registro v1.0):** los 11 agentes con su identificador (`account.name`), su fase, su función y su grupo, y lo que no es agente de IA (el motor, el consolidador y el guardián, la infraestructura y la cuenta del sistema). No muestra la `homePage`, que lleva el dominio de la empresa (Q21).

**Antes de pasarla a `main`:** el enlace al texto completo solo funciona si `governance/` también pasa a `main`. Hace falta el visto bueno de la autora para las dos cosas.

### 2b. Cambios de contenido previstos para la v0.8.4 → ~~no se hacen todavía (van después del congreso)~~ **Cambia el mismo 18 nov (la autora): la corrección de los 66 *can-do* va ahora**, en la versión que entra en producción con los arreglos del desarrollador, no en una «v0.8.4». Número de versión por confirmar: los *can-do* son del inventario (eje v0.7.x), no del perfil (eje v0.8.x)

`index.html` muestra el vocabulario del perfil v0.8.3. Sus definiciones cambian en la v0.8.4, al terminar la auditoría (Q24). La autora aprobó las definiciones de los verbos el 18 nov (`../verbos-xapi/README.md`). Cambios previstos:

| Término | Hoy en el perfil v0.8.3 | Cambio previsto | Motivo |
|---|---|---|---|
| `adapted` | «Actor is the teaching agent (human or AI)…» | Actor = el alumno; el agente que adapta va en `context.instructor` | R-ID (10 nov) |
| `progressed` | «Band or subskill progression event (e.g. B1 → B2 readiness signal)» | Progreso lineal y no final dentro del paquete de descriptores del nivel; nunca del nivel declarado al mismo | Definición de ADL y regla de la autora (11 nov) |
| `completed` / `passed` de nivel | No existe | `passed` de nivel al alcanzar la regla pública del 80 %; `completed` de nivel al trabajar todos los objetivos del nivel | Decisión de la autora (12 nov) |
| `completed` de misión | «Task completed — the <MISSION_COMPLETE> gate event» | Añade `result.completion = true`, `ext/input-channel` y el tipo de práctica | Decisión de la autora (18 nov) |
| `attempted` | «Learner attempts a task/mission» | Se emite al empezar toda misión | Decisión de la autora (18 nov) |
| `played` | `https://w3id.org/xapi/audio/verbs/played` | `https://w3id.org/xapi/video/verbs/played` | Esa IRI no existe en el perfil de audio de ADL, que reutiliza el `played` de vídeo |
| `level-decision` | «demonstrated-level recalibration decision» | Sin la palabra «decision»: es la marca del progreso del alumno | La IA no decide (G-NIVEL-1) |
| Inventario: 66 *can-do* de gramática | Empiezan por «Can» seguido de un sustantivo (p. ej. «Can location using…») | Un verbo en su lugar; la forma no cambia. Propuesta, uno por uno, en `revision-inventario/` | Revisión a mano del 18 nov (H10) |
| Inventario: 11 hallazgos más | Ejemplos que no usan el término, solapes gramática–vocabulario, un id que no coincide con su forma | Ver `revision-inventario/README.md` | Revisión a mano del 18 nov |
