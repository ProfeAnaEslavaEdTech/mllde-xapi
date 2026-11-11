# Verbos xAPI: definición oficial de ADL, perfil MLLDE y uso real en TK CoachAI · 11 nov 2026

**Para qué sirve:**
- que la base de conocimiento de TK CoachAI use cada verbo con su definición oficial;
- que no haya incongruencias entre lo que dice ADL, lo que dice el perfil MLLDE v0.8.3 y lo que emite la app.

**Estado:** borrador. Las definiciones propuestas (§3) **no están aprobadas**; se revisan con Ana el 12 nov.

## 1. Fuentes

**Definiciones oficiales de ADL**, descargadas el 11 nov del repositorio oficial `adlnet/xapi-authored-profiles` (rama `master`):

| Perfil ADL | Archivo | IRI del perfil |
|---|---|---|
| ADL Vocabulary | `adl/v1.0/adl.jsonld` | `https://w3id.org/xapi/adl` |
| SCORM | `scorm/v1.0/scorm.jsonld` | `https://w3id.org/xapi/scorm` |
| cmi5 | `cmi5/v1.0/cmi5.jsonld` | `https://w3id.org/xapi/cmi5` |
| Audio | `audio/v1.0/audio.jsonld` | `https://w3id.org/xapi/audio` |

Copia de las definiciones en `mllde-xapi/governance/verbos-xapi/definiciones-adl-oficiales.json` (rama `claude/normas-gobernanza-v1.6`).

**Las demás fuentes:**
- **Perfil MLLDE:** `mllde-xapi-profile_v0.8.3.jsonld` (publicado en `main`, sin tocar).
- **Uso real:** export de Veracity del 11 nov, con 2.244 sentencias.

## 2. Comparación verbo a verbo

«Vivas» = no anuladas. **Actor:** en todos los verbos de aprendizaje es el alumno (seudónimo TK o UUID); en `voided`, «TK Coach Engine».

| Verbo | Definición oficial de ADL | Perfil MLLDE v0.8.3 | Qué hace hoy la app (export del 11 nov) | ¿Encaja con las reglas? |
|---|---|---|---|---|
| **attempted** | «Indicates the actor made an effort to access the object. An attempt statement without additional activities could be considered incomplete in some cases.» | «Learner attempts a task/mission» | Tarjetas de vocabulario (433) y misiones con incidente (19) | ✅ Encaja con ADL. La tarjeta es un intento de acceso, no una medición (cortafuegos de práctica) |
| **completed** | «Indicates the actor finished or concluded the activity normally.» (perfil SCORM) | «Task completed — the <MISSION_COMPLETE> gate event» | 139 vivos, **todos con una misión como objeto**: el cierre de sesión con su rúbrica. **Ninguno de nivel** | ◐ El de misión encaja. **Falta el de nivel** (regla de Ana, 11 nov). Ver §3 sobre el 80 % |
| **passed** | «Indicates the actor successfully passed an activity to a level of predetermined satisfaction.» (SCORM) | «Performance meets the level's can-do descriptors (rubric floors met)» | Sin uso (0) | ⚠️ Según ADL, superar un umbral fijado (el 80 %) es justo `passed`. Hay que decidir si el 80 % es `passed` o `completed` (§3) |
| **failed** | «Indicates the actor did not successfully pass an activity to a level of predetermined satisfaction.» (SCORM) | «Attempt did not yet meet floors (non-punitive: pairs with unlimited retry)» | Sin uso (0) | ⚪ Con un progreso lineal y no final, no hace falta |
| **progressed** | «Indicates a value of how much of an actor has advanced or moved through an activity.» | «Band or subskill progression event (e.g. B1 → B2 readiness signal)» | 8 vivos. **Todos van del nivel declarado al mismo** (B1 → B1, B2 → B2, C1 → C1), «nivel declarado confirmado», con una misión como objeto. Salen tras 3 sesiones con banda ≥ 6 y no dicen cuántos descriptores se cumplen | ❌ **No encaja ni con ADL ni con la regla de Ana:** lineal, no final, más descriptores del paquete de nivel. La definición MLLDE tampoco encaja con ADL |
| **interacted** | «Indicates the actor engaged with a physical or virtual object.» | «A conversational turn in interaction scales» | Sin uso (0). Los turnos van como `adapted` | ⚪ Coherente, pero sin uso |
| **asked** | «Indicates an inquiry by an actor with the expectation of a response or answer to a question.» | «Vocabulary/help request by the learner» | Sin uso (0). La Pista y el traductor no dejan rastro | ⚪ Si se quedan la Pista o el traductor (reunión, Q5), su uso sería `asked`, con el alumno como actor y el agente en `context.instructor` |
| **answered** | «Indicates the actor replied to a question, where the object is generally an activity representing the question. The text of the answer will often be included in the response inside result.» | «Discrete scorable practice item. H2 resolved: reuse ADL answered.» | Drills de gramática y tarjetas: 858 drills y 48 tarjetas | ✅ Encaja |
| **played** | En el perfil de audio de ADL, el verbo es **`https://w3id.org/xapi/video/verbs/played`** | Usa **`https://w3id.org/xapi/audio/verbs/played`** | Sin uso (0) | ❌ **La IRI MLLDE no existe en el perfil oficial:** el audio de ADL reutiliza el `played` de vídeo. Se corrige en la v0.8.4; no afecta a datos |
| **voided** | «A special reserved verb used by a LRS or application to mark a statement as invalid.» | Reservado; el agregador excluye las anuladas | 36, todas con «TK Coach Engine» como actor | ✅ Encaja (acto del sistema, R-ID) |
| **pronounced** (MLLDE) | No existe en ADL | «Made a pronunciation attempt at a declared target feature…» | Sin uso (0); el generador de pronunciación está oculto | ⚪ Coherente; depende de la reunión (Q5) |
| **mediated** (MLLDE) | No existe en ADL | «Performed a mediation activity: transformed or relayed content from a source for a recipient…» | 63, con una misión como objeto y el alumno como actor | ✅ Encaja |
| **adapted** (MLLDE) | No existe en ADL | «**Actor is the teaching agent (human or AI)**: the learning path or assessment was adapted for the learner…» | 488 por turno con el alumno como actor; 141 de fin de sesión con **Capi como actor** | ❌ **La definición contradice R-ID** (10 nov): el actor es el alumno y el agente va en `context.instructor`. Los 141 con Capi tampoco encajan |
| **evaluated** | No existe en ADL ni en el perfil MLLDE | — | No se emite | — La medición va en el `completed` de misión, con la rúbrica. **No hay un verbo «evaluated»** |

**Nota (error ya corregido; no entra en la lista):** hasta el 25 sep algunos verbos se emitieron con IRIs no canónicas:
- `https://adlnet.gov/…` en `attempted`, `completed` y `progressed`;
- `https://w3id.org/mllde/verb/answered`, con 749 sentencias.

Desde el 25 sep van con la IRI canónica.

## 3. Definiciones propuestas para la base de conocimiento (borrador para el 12 nov)

Reglas que aplican:
- **R-ID:** el actor es siempre el alumno, y el agente va en `context.instructor`.
- **G-NIVEL-1:** B2B y B2C; la IA no decide.
- **La regla de Ana sobre `progressed` y `completed`** (11 nov).

| Verbo | Propuesta (ES) | Objeto |
|---|---|---|
| attempted | El alumno inicia una misión o una tarjeta. No implica que la termine ni mide nada | Misión o tarjeta |
| completed · misión | El alumno termina la sesión de una misión con normalidad (puerta MISSION_COMPLETE). Lleva la banda que calcula el código | Misión |
| completed · nivel | **Nuevo.** El alumno ha trabajado todos los objetivos de su nivel | Nivel |
| passed · nivel | **Por decidir:** el alumno alcanza la regla pública del 80 % de su paquete de descriptores | Nivel |
| progressed | Progreso lineal y no final dentro del paquete de descriptores del nivel del alumno: **demuestra más descriptores que antes.** Lleva cuántos de cuántos. Nunca va del nivel declarado al mismo | Nivel |
| answered | El alumno responde a un ítem de práctica (drill o tarjeta). No cuenta para la banda | Drill o tarjeta |
| asked | El alumno pide ayuda o vocabulario. Si responde un agente, el agente va en `context.instructor` | La ayuda o la palabra |
| interacted | Sin uso en TK CoachAI (los turnos van como `adapted`) | — |
| failed | Sin uso en TK CoachAI: el progreso es lineal y no hay suspensos | — |
| played | IRI corregida: `https://w3id.org/xapi/video/verbs/played` (perfil de audio de ADL). Sin uso hoy | Audio |
| pronounced | Sin cambios; depende de la reunión (Q5) | Rasgo de pronunciación |
| mediated | Sin cambios | Misión |
| adapted | **La ruta o la tarea se adaptó para el alumno.** Actor = el alumno; el agente que adapta va en `context.instructor` (R-ID). El «advance» que decide el código va sin `instructor` y con `rules-version` | Misión |
| voided | Sin cambios. Actor = `tk-coach-engine` | La sentencia anulada |

## 4. Lo que hay que decidir el 12 nov

1. **El 80 %:**
   - ¿es `passed` (ADL: superar un umbral fijado) o `completed` (ADL: terminar con normalidad)?
   - Propuesta: `passed` al alcanzar el 80 %, y `completed` cuando el alumno ha trabajado todos los objetivos del nivel. cmi5 los usa así, por separado.
2. **¿Se aprueban las definiciones del §3?** Irían en las normas ya, y en el perfil en la v0.8.4 (Q24).
3. **¿Se anulan los 8 `progressed` «B1 → B1»?** No son progreso, y el código los sigue emitiendo (el último es del 4 nov).
4. **¿Se quita la prueba T-NIVEL-1 (b)?** Ya la cubre A3 de R-ID.
5. **Dependencia:** el contador de `progressed` necesita el criterio de «demostrado», que se decide con casos reales.
