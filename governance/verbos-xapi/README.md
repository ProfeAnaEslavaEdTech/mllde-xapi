# Verbos xAPI: definición oficial de ADL y definiciones del MLLDE · 11–18 nov 2026

**Para qué sirve:**
- que la base de conocimiento de TK CoachAI use cada verbo con su definición oficial;
- que no haya incongruencias entre lo que dice ADL y lo que dice el perfil MLLDE v0.8.3.

**Estado (18 nov):** las definiciones del §3 están **aprobadas** por la autora. *Hasta el 18 nov decía: «borrador; las definiciones propuestas no están aprobadas».* Están en el perfil MLLDE v0.8.3.

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

## 2. Definición oficial de ADL y perfil MLLDE v0.8.3

| Verbo | Definición oficial de ADL | Perfil MLLDE v0.8.3 |
|---|---|---|
| **attempted** | «Indicates the actor made an effort to access the object. An attempt statement without additional activities could be considered incomplete in some cases.» | «Learner attempts a task/mission» |
| **completed** | «Indicates the actor finished or concluded the activity normally.» (perfil SCORM) | «Task completed — the <MISSION_COMPLETE> gate event» |
| **passed** | «Indicates the actor successfully passed an activity to a level of predetermined satisfaction.» (SCORM) | «Performance meets the level's can-do descriptors (rubric floors met)» |
| **failed** | «Indicates the actor did not successfully pass an activity to a level of predetermined satisfaction.» (SCORM) | «Attempt did not yet meet floors (non-punitive: pairs with unlimited retry)» |
| **progressed** | «Indicates a value of how much of an actor has advanced or moved through an activity.» | «Band or subskill progression event (e.g. B1 → B2 readiness signal)» |
| **interacted** | «Indicates the actor engaged with a physical or virtual object.» | «A conversational turn in interaction scales» |
| **asked** | «Indicates an inquiry by an actor with the expectation of a response or answer to a question.» | «Vocabulary/help request by the learner» |
| **answered** | «Indicates the actor replied to a question, where the object is generally an activity representing the question. The text of the answer will often be included in the response inside result.» | «Discrete scorable practice item. H2 resolved: reuse ADL answered.» |
| **played** | En el perfil de audio de ADL, el verbo es **`https://w3id.org/xapi/video/verbs/played`** | Usa **`https://w3id.org/xapi/audio/verbs/played`** |
| **voided** | «A special reserved verb used by a LRS or application to mark a statement as invalid.» | Reservado; el agregador excluye las anuladas |
| **pronounced** (MLLDE) | No existe en ADL | «Made a pronunciation attempt at a declared target feature…» |
| **mediated** (MLLDE) | No existe en ADL | «Performed a mediation activity: transformed or relayed content from a source for a recipient…» |
| **adapted** (MLLDE) | No existe en ADL | «**The actor is the learner.** The teaching agent (AI or human) adapted the learning path, or its answer, for the learner; an AI agent goes in context.instructor…» |
| **evaluated** | No existe en ADL ni en el perfil MLLDE | — |


## 3. Definiciones para la base de conocimiento (aprobadas el 18 nov)

Reglas que aplican:
- **R-ID:** el actor es siempre el alumno, y el agente va en `context.instructor`.
- **G-NIVEL-1:** B2B y B2C; la IA no decide.
- **La regla de Ana sobre `progressed` y `completed`** (11 nov).

| Verbo | Definición (ES) | Objeto |
|---|---|---|
| attempted | **Aprobada (18 nov):** el alumno inicia una misión o una tarjeta. **Se emite al empezar toda misión**, para que una misión abandonada deje rastro. No implica que la termine y no lleva banda. Si la misión o la tarea de mediación la generó un agente, el agente va en `context.instructor` (`mission-agent` o `mediation-agent`) y los descriptores objetivo van en `content-ref` (plantilla `attempted-mission`) | Misión o tarjeta |
| completed · misión | **Aprobada (18 nov):** el alumno termina la sesión de una misión con normalidad (puerta MISSION_COMPLETE). Uno por registration. Lleva `result.completion = true` y la banda que calcula el motor (determinista); si la sesión no supera las puertas (por ejemplo, una mediana de la confianza de la voz en los turnos del alumno inferior a 0,70), va sin banda y con su incidente. Una misión que no se termina no lleva `completed`. **Declara de dónde sale la práctica:** la entrada del alumno en `ext/input-channel` (voz, texto u OCR) y el tipo de práctica (misión de negocio, «Practica tu situación» o «Presenta tu visual»). Así las prácticas con OCR quedan identificadas (normas v1.3). | Misión |
| completed · nivel | **Decidida (12 nov).** El alumno ha trabajado todos los objetivos de su nivel | Nivel |
| passed · nivel | **Decidida (12 nov):** el alumno alcanza la regla pública del 80 % de su paquete de descriptores | Nivel |
| progressed | Progreso lineal y no final dentro del paquete de descriptores del nivel del alumno: **demuestra más descriptores que antes.** Lleva cuántos de cuántos. Nunca va del nivel declarado al mismo | Nivel |
| answered | El alumno responde a un ítem de práctica (drill o tarjeta). No cuenta para la banda | Drill o tarjeta |
| asked | El alumno pide ayuda o vocabulario. Si responde un agente, el agente va en `context.instructor` | La ayuda o la palabra |
| interacted | Sin uso en TK CoachAI (los turnos van como `adapted`) | — |
| failed | Sin uso en TK CoachAI: el progreso es lineal y no hay suspensos | — |
| played | IRI corregida en el perfil v0.8.3: `https://w3id.org/xapi/video/verbs/played` (perfil de audio de ADL). Reservado para el audio | Audio |
| pronounced | Sin cambios; depende de la reunión (Q5) | Rasgo de pronunciación |
| mediated | Sin cambios | Misión |
| adapted | **La ruta o la tarea se adaptó para el alumno.** Actor = el alumno; el agente que adapta va en `context.instructor` (R-ID). El «advance» que decide el motor (determinista) va sin `instructor` y con `rules-version` | Misión |
| voided | Sin cambios. Actor = `tk-coach-engine` | La sentencia anulada |

## 4. Decisiones del 12 nov

1. **El 80 %: decidido.** `passed` de nivel cuando el alumno alcanza la regla pública del 80 %; `completed` de nivel cuando ha trabajado todos los objetivos del nivel. Así lo hace cmi5. Está en las normas, G-NIVEL-1.
2. **La prueba T-NIVEL-1 (b): retirada el 18 nov.** El actor del `progressed` lo fijan R-ID y su control A3.
3. **Las definiciones del §3: aprobadas el 18 nov**, todas. Están en el perfil v0.8.3, que se actualizó con ellas, y con la plantilla `attempted-mission` para la tarea que genera cada agente.

## 4-ter. Decisiones del 18 nov

1. **`completed` de misión: aprobado**, con `result.completion = true`, `ext/input-channel` y el tipo de práctica. Está en las normas, G-NIVEL-1, «Verbos de la misión».
2. **`attempted` al empezar toda misión: aprobado.**
3. **T-NIVEL-1 (b): retirada.**
4. **Todas las definiciones del §3: aprobadas.**

