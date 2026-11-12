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

## 2. `index.html` (registro y perfil v0.8.3) → **no se cambia todavía**

`index.html` muestra el vocabulario del perfil v0.8.3. Sus definiciones cambian en la v0.8.4, cuando la autora apruebe las de los verbos (`../verbos-xapi/README.md`) y al terminar la auditoría (Q24). Cambios previstos:

| Término | Hoy en el perfil v0.8.3 | Cambio previsto | Motivo |
|---|---|---|---|
| `adapted` | «Actor is the teaching agent (human or AI)…» | Actor = el alumno; el agente que adapta va en `context.instructor` | R-ID (10 nov) |
| `progressed` | «Band or subskill progression event (e.g. B1 → B2 readiness signal)» | Progreso lineal y no final dentro del paquete de descriptores del nivel; nunca del nivel declarado al mismo | Definición de ADL y regla de la autora (11 nov) |
| `completed` / `passed` de nivel | No existe | Cierre de nivel: regla pública del 80 % o todos los objetivos del nivel (pendiente: ¿`passed` o `completed`?) | Regla de la autora (11 nov) |
| `played` | `https://w3id.org/xapi/audio/verbs/played` | `https://w3id.org/xapi/video/verbs/played` | Esa IRI no existe en el perfil de audio de ADL, que reutiliza el `played` de vídeo |
| `level-decision` | «demonstrated-level recalibration decision» | Sin la palabra «decision»: es la marca del progreso del alumno | La IA no decide (G-NIVEL-1) |
