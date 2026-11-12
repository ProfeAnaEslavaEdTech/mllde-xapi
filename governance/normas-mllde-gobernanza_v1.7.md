# Normas de gobernanza MLLDE — paquete descargable
**Versión:** 1.7 · **Fecha:** 9–11 de noviembre de 2026 · **Cambio del 11 nov (G-NIVEL-1):** dos modalidades, B2B y B2C. En las dos, el `progressed` entra en la LRS con el alumno como actor, y la validación del profesor es externa a la app. La IA no decide: compara la evidencia con los descriptores. El test de nivel de la app se desactiva (P6). **Cambio v1.7:** regla de trazabilidad N6-bis — paquete de auditoría semanal en cmi5 (decisión de la autora, reunión del 9 nov). Recordatorio en N9 del acuerdo previo: el nombre del alumno lo pone la app al presentar el informe, nunca el modelo. Corregida la nota sobre la N14: existe desde el 8 nov. Añadido el principio de verificación junto al principio rector. Principio de invariancia del rol (la temperatura deja de ser condición de cumplimiento; R-ADM-2 ajustada). Teo (`support-agent`) declarado en el registro, por el art. 50(1) del AI Act. Registro de identificadores con un JSON por agente en `governance/registro-agentes/`. N6 apunta a `context.instructor`. Fundamento legal de N5 (AI Act cotejado con el texto del DOUE, RGPD, ISO/IEC 42001). Nueva sección **R-ID**: identificación de los agentes en el registro (`context.instructor`, xAPI 1.0.3 §2.4.6) y forma exacta de sus identificadores; sustituye la regla «actor = el agente que actúa» (decisión 53). **Cambio v1.6:** propuesta de acuñación de IRIs (bump v0.8.4 del registro) tras el análisis del registro publicado v0.8.3 — sin verbos nuevos; 7 extensiones, 4 campos en `ext/level-decision` y 2–3 tipos de incidente. **Cambio v1.5:** regla de decisión de nivel para el usuario libre sin profesor — el código propone y el propio usuario acepta tras ver la evidencia, con revisor humano obligatorio en saltos de dos niveles, entrada en nivel C o disputa; menores excluidos de la autoaceptación. **Cambio v1.4:** regla principal de gobernanza (R-MED-1) — toda medición pasa por el flujo de medición contra la base completa y ningún otro agente mide por su cuenta. **Cambio v1.3:** doble vía de vocabulario según el tipo de usuario (decisión de la autora), alcance del lector OCR (decide sobre la imagen, nunca sobre el alumno) y regla de medición en toda interacción con comparación nivel real vs declarado. **Cambio v1.2:** tabla de equivalencia con la numeración de la spec del Evaluador v2 (§6.1) y nota sobre la referencia huérfana «N14» de la Cartilla de los 7.
**Principio rector:** La base define · la IA localiza · el código calcula · el profesor valida · la LRS lo registra. *(Hasta el 12 nov decía «el profesor decide»; cambia por G-NIVEL-1: la validación del profesor es externa a la app.)*
**Principio de verificación (Ana Eslava-Graterol):** cotejar cada afirmación con los datos es lo que destapó los fallos de TK CoachAI. Si se hubiera aceptado lo que se decía sin comprobarlo, seguiríamos con cifras falsas. Cotejar no es lentitud: es la auditoría. Para la gobernanza, ninguna afirmación se da por buena sin su prueba (IDs de sentencias en el LRS, extracto de código y fecha desde la que se cumple).
**Principio de invariancia del rol (Ana Eslava-Graterol, 10 nov):** ningún agente decide, y todos se apegan a su rol, sea cual sea el modelo, se llame como se llame, y sea cual sea la temperatura que aplique el sistema. El rol lo hacen cumplir el código y las pruebas (esquema validado, ids de la base, bloque común, controles A1–A4 de R-ID, prueba de estabilidad), no los parámetros del modelo. El identificador exacto del modelo se registra para auditar, no para confiar.

> Estas normas gobiernan a todo agente de IA del modelo MLLDE y de sus aplicaciones (p. ej. TK CoachAI). Un agente que no está en el mapa no entra en el loop.

## R-MED-1 — Regla principal: toda medición pasa por el flujo de medición

> **REGLA PRINCIPAL, vinculante para todo agente de IA:** la producción del usuario la contrasta siempre el flujo de medición contra la base completa — **381 descriptores A1–C2 medibles desde texto** (el inventario tiene 382: gram 115 · voc 96 · spk 100 · med 71; se excluye un descriptor de pronunciación, que no se mide desde texto) —, con `ext/input-channel` declarado. **Ningún otro agente mide, puntúa ni evalúa al usuario por su cuenta.**

- Un agente que no es el flujo de medición puede extraer, seleccionar, redactar o planificar, pero **nunca emite juicio sobre el nivel o la competencia del usuario** (N10: cero cálculos en LLM; P2 de G-NIVEL-1: un campo `level`/`grade` invalida la respuesta entera).
- La comparación **nivel real vs declarado** la computa el código con la regla pública del 80 % (umbrales v0.7.2); el Evaluador nunca recibe el nivel declarado (P1, anti-anclaje).
- Los descriptores que el usuario evidencia con cita literal seleccionan el contenido de la fase Process siguiente (i+1 por código).
- Toda emisión al perfil exige actor humano (G-NIVEL-1, P3–P5).
- Regla acuñada el 9 nov por decisión de la autora; entra en vigor con las firmas de pedagogía e ingeniería (N12).

## N — Normas estructurales (N1–N13, extracto operativo)

| Norma | Regla |
|---|---|
| **N1 — Registro cerrado** | Solo los agentes del mapa canónico pueden actuar. Agente nuevo = propuesta con ficha firmada, no una instalación. |
| **N2 — Puerta única** | Toda emisión a la LRS pasa por el Consolidador (código). Ningún agente escribe a la LRS por su cuenta. |
| **N3 — Anti-agente-rogue** | El prompt en producción debe coincidir con el aprobado (`prompt-hash`); si difiere, el agente no arranca. |
| **N4 — Base cerrada** | Un solo bundle de conocimiento (registry v0.8.3 + inventario v0.7.2), montado por código, con `kb-version` y `kb-hash` declarados. Nada de material con copyright en el prompt. |
| **N5 — Modelos fijos** | Modelo con versión fijada por escrito; contrato no-train verificado; **sin fallback jamás** (lección Gemini, 5–19 oct). El identificador exacto del modelo va en cada sentencia (R-ID). **Aplica a todos los agentes, no solo al que mide** (decisión de la autora, 11 nov), con seguimiento de la tasa de apego por modelo. Fundamento legal: ver la nota bajo esta tabla. |
| **N6 — Trazabilidad** | El agente en `context.instructor`, con su `account` del registro (R-ID, v1.7; antes, `agent-id`), + `agent-version` + `measure-model` (identificador exacto) + `rules-version` en cada statement. Meta: todos los agentes registrados con rastro propio. El registro está en `governance/registro-agentes/`. |
| **N7 — Flujos que no se cruzan** | Medición (1×/sesión), pedagogía (por turno), actividad (loop). La banda solo nace del flujo de medición. |
| **N8 — Fail-closed** | Ante la duda, no emite: puerta ASR 0.70, juez no disponible → sin tip, esquema inválido → descarte. |
| **N9 — PII** | Al modelo solo va UUID + transcripción; nunca nombre, empresa, puesto ni correo. Autoridad LRS = cuenta de servicio, nunca credencial personal. **Los hitos (texto libre del perfil): en revisión** (12 nov), sin decisión final. Propuesta: dejar de enviarlos al modelo. |
| **N10 — Cero cálculos en LLM** | Ningún agente genera números de competencia: notas (5.2/5.3), banda (fórmula del 26/08), i+1 y nivel propuesto los calcula el código. |
| **N11 — Incidentes declarados** | Cada agente define sus tipos de incidente con IRI del registry; van a su registro, nunca a KPIs del alumno. |
| **N12 — Versionado firmado** | Cambio de prompt/modelo/reglas = bump + firma (pedagogía + ingeniería) + entrada en el mapa + fecha desde la que cuenta. |
| **N13 — Pruebas en CI** | Toda prueba de admisión corre en CI en cada despliegue; si falla, el despliegue se bloquea. |

**Fundamento legal de N5** (desarrollado en la cartilla de agentes, §3.1). Las citas del AI Act se cotejaron el 11 nov con el texto oficial del DOUE (Reglamento (UE) 2024/1689, versión original, sin los cambios del Reglamento (UE) 2026/1744):
- **AI Act:**
  - art. 11 y anexo IV 2(a);
  - art. 25(4);
  - art. 53(1)(b) y anexo XII;
  - arts. 12, 15(1), 15(4) y 19;
  - modificación sustancial: arts. 3(23) y 43(4);
  - art. 86.

  Las obligaciones de alto riesgo aplican desde el 2 dic 2027 (Reglamento (UE) 2026/1744).
- **RGPD** (aplica hoy):
  - arts. 5(1)(a), (b), (d) y (f), y art. 5(2);
  - arts. 13(1)(e)–(f);
  - art. 28(3);
  - art. 30(1)(d)–(e);
  - art. 32;
  - art. 35;
  - arts. 44–46.
- **ISO/IEC 42001:** A.6.2.8 y A.10.

> **Qué es el UUID de N9 (12 nov).** UUID son las siglas de *Universally Unique Identifier*, «identificador único universal». Es un código de 32 caracteres hexadecimales en cinco grupos separados por guiones, por ejemplo `7ba714b6-b6b5-4b7f-8cbd-1ca44b43145e`. Se genera de forma que la probabilidad de que se repita es prácticamente nula.
>
> **En TK CoachAI** es el identificador seudónimo del alumno: aparece en la LRS como `account.name` del actor, en lugar de su nombre. Al modelo solo van el UUID y la transcripción: así el modelo sabe a qué alumno pertenece una sesión sin saber quién es (sin nombre, empresa, puesto ni correo).
>
> **El seudónimo corto de los paneles**, del tipo `TK-7BA714B6`, son los 8 primeros caracteres del UUID en mayúsculas. Comprobado en el export de Veracity del 11 nov: 577 de 577 sentencias con seudónimo.
>
> **Seudónimo no es anónimo:** quien tiene la tabla que une el UUID con el perfil puede identificar al alumno. Por eso el UUID sigue siendo un dato personal y se protege como tal.

> **Recordatorio de un acuerdo previo (N9 · datos personales).** Si el informe tiene que mostrar el nombre del alumno, lo pone **la app al presentarlo, fuera de la IA**: el código toma el texto del modelo y le añade el nombre desde el perfil. Así el nombre aparece en pantalla o en el PDF **sin pasar nunca por el modelo**. Es lo que pide la minimización de datos (RGPD, art. 5(1)(c)).

### N6-bis — Paquete de auditoría semanal en cmi5 (regla de trazabilidad, v1.7)

> **Regla:** cada semana, el entorno entrega a la diseñadora un **paquete cmi5** de la versión en producción, descargable sin intervención del desarrollador. Se importa en **SCORM Cloud** y se lanza con un alumno de prueba; las sentencias xAPI que emite se comparan con el registro y el perfil vigentes.

- **Qué se comprueba:**
  - **a. Continuidad del loop:** Input → Process → Output → Adaptar, paso a paso y en orden.
  - **b. Métricas no declaradas:** ninguna extensión, verbo ni resultado que no esté en el registro.
  - **c. Métricas duplicadas:** una sesión, un `completed`; ningún dato emitido dos veces.
  - **d. Actores y agentes no autorizados:** ningún actor ni agente que no esté en el mapa canónico. Un actor desconocido es un incidente y se revisa antes de seguir.
- **Por qué cmi5 y no SCORM 2004:** cmi5 se basa en xAPI, así que muestra actores, verbos y objetos. SCORM 2004 no transporta sentencias xAPI y no permite esta comprobación.
- **Lo que el paquete no sustituye:** el paquete prueba lo que la versión **emite**. Lo que **ha pasado** se audita con los 3 exportables del LRS (sentencias, verbos y objetos, agentes) y con el JSON del panel de administración (modelo de medida). Las dos auditorías se cruzan.
- **Registro:** cada paquete lleva fecha, versión de la app y `prompt-hash` de los agentes; se conserva con el resultado de la comprobación.
- **Contenido del paquete (decisión de la autora, 12 nov):** las secuencias completas learn, practice y progress, no solo `initialized` y `terminated`, con los verbos según su definición oficial de ADL (`governance/verbos-xapi/`).
- Regla acordada en la reunión del 9 nov; entra en vigor con las firmas de pedagogía e ingeniería (N12).

### N6-ter — Conservación de las transcripciones (Ana Eslava-Graterol, 12 nov)

> **Regla:** las transcripciones de cada sesión se guardan en el servidor **al menos 6 meses**, seudonimizadas (solo el UUID del alumno) y con acceso limitado, y **se pueden descargar cuando se audita**.

- **Por qué:** el humano valida, y sin evidencia no puede validar. El profesor constata el nivel con las respuestas, los errores y las citas del alumno (G-NIVEL-1 P4). El auditor comprueba que cada etiqueta del LRS (por ejemplo, un `implicit-recast`) corresponde a lo que pasó en la conversación (principio de verificación).
- **Hoy no se cumple:** solo se guarda el JSON del Evaluador, y la conversación vive 3 horas en el navegador del alumno.
- **Fundamento:** AI Act, arts. 12 y 19 (registros), y art. 26(6) (conservación de los registros al menos 6 meses).
- **Cómo se comprueba:** el ID de una sesión, su transcripción descargada y la fecha desde la que se cumple.
- Entra en vigor con las firmas de pedagogía e ingeniería (N12).

### Equivalencia con la numeración de la spec del Evaluador v2 (§6.1)

> **Aviso de numeración.** La spec del Evaluador v2 (8 nov) numera sus normas de otra forma a partir de N4, y la Cartilla de los 7 (8 nov) cita esa numeración de la spec (p. ej. «N9 = modelo exacto»). Para que el comité no encuentre dos «N9» distintas, esta es la correspondencia oficial:

| Spec Evaluador v2 (§6.1) | Equivalente en este paquete v1.1 |
|---|---|
| N1 · Registro cerrado | **N1** (misma regla) |
| N2 · Puerta única de llamadas a modelos | **N2** (aquí con énfasis en la emisión a la LRS) |
| N3 · Prueba anti-agentes sueltos (incluye prompt-hash) | **N3** (misma regla) |
| N4 · Ficha antes que código (solicitud justificada + dos firmas) | **R-ADM-1 y R-ADM-5** |
| N5 · Una función por agente; ningún agente decide | Principio rector + **N10** |
| N6 · Bloque común obligatorio en cada prompt | **Ausente en v1.1 — incorporar** (texto literal en la spec §6.2) |
| N7 · La base se hereda por código | **N4** |
| N8 · Trazabilidad (actor = el agente que actúa) | **N6** + **R-ID** (v1.7: el actor es el alumno; el agente va en `context.instructor`) |
| N9 · Modelos aprobados y fijos, sin respaldo | **N5** |
| N10 · Datos mínimos (sin datos personales) | **N9** |
| N11 · Cambios = versión nueva, con prueba y firmas | **N12** |
| N12 · Auditoría periódica (agentes ↔ llamadas ↔ Veracity) | **Ausente en v1.1 — incorporar** |
| N13 · Retirada de agentes sin ficha en plazo | **Ausente en v1.1 — incorporar** |
| N14 · Necesidad demostrada (8 nov) | **R-ADM-1**, con la condición de necesidad demostrada |
| N12-bis · Paquete de auditoría semanal en cmi5 (9 nov) | **N6-bis** (v1.7) |

> **Sobre la «N14» que cita la Cartilla de los 7 (corregido en v1.7):** la N14 **sí existe**. La añadió la autora a la spec del Evaluador v2 el 8 nov, con su decisión de que el loop solo necesita 7 agentes: **N14 · Necesidad demostrada** — un agente solo se aprueba si su ficha demuestra qué parte del loop lo necesita y por qué no lo puede hacer el código ni uno de los 7 agentes del loop. Su equivalente en este paquete es **R-ADM-1** (registro en el mapa con justificación) reforzada con esa condición. La nota de la v1.2 que la daba por huérfana se escribió sobre una versión anterior de la spec. Entra en vigor con las firmas de pedagogía e ingeniería (N12).

## G-NIVEL-1 — El nivel: la app propone, nunca genera el nivel

**Dos modalidades de usuario (Ana Eslava-Graterol, 11 nov).** TK CoachAI se creó para B2B y para B2C. Las especificaciones las distinguen siempre:

| | **B2B** (empresa · `user-track: pilot`) | **B2C** (consumidor · `user-track: free`) |
|---|---|---|
| Quién hay | El alumno y, detrás, un profesor que modera | El alumno solo, sin profesor |
| Qué hace la app | Compara la evidencia real del alumno con los descriptores: cuántos se cumplen y de qué nivel son, y emite una banda | Lo mismo |
| Qué entra en la LRS | **`progressed`, con el alumno como actor**: el usuario que interactúa y produce la conversación es siempre el que ha progresado. Lleva su marca y su evidencia | Lo mismo |
| Validación externa (fuera de la app; no entra en la LRS) | El profesor constata el nivel con otra evaluación, oral y escrita | Si la persona quiere el nivel validado, un profesor lo constata fuera, con otra evaluación |
| Entorno | Formación con profesor responsable | Fuera de los entornos educativos oficiales |

- **REGLA:** la app PROPONE una medida con una regla pública, contra los criterios fijados en la app: el nivel más alto con **≥80% de descriptores evidenciados con cita literal** (umbrales v0.7.2: A1 48 · A2 52 · B1 63 · B2 58 · C1 48 · C2 40). **La IA no decide:** no evalúa la evidencia con su propio criterio ni con lo que le parece. Compara datos reales de distintas fuentes, la evidencia del alumno y los descriptores de la base: la IA localiza la evidencia y el código cuenta y calcula la banda. **El `progressed` es la marca de progreso del alumno en la app, no la acreditación del nivel:** esa la da, cuando corresponde, una validación externa.
- **Verbos del nivel (Ana Eslava-Graterol, 11–12 nov):**
  - **`progressed`:** progreso lineal y no final dentro del paquete de descriptores del nivel del alumno. Se emite cuando demuestra más descriptores que antes y lleva cuántos de cuántos. Nunca va del nivel declarado al mismo nivel.
  - **`passed` de nivel:** el alumno alcanza la regla pública del 80 % (12 nov).
  - **`completed` de nivel:** el alumno ha trabajado todos los objetivos del nivel (12 nov). El `completed` de misión sigue siendo el cierre de cada sesión.
  - Los 8 `progressed` del nivel al mismo nivel que hay hoy en la LRS se revisan con el desarrollador (12 nov).
- **P1:** ningún agente recibe el nivel declarado del alumno (anti-anclaje).
- **P2:** ningún modelo devuelve niveles ni notas (un campo `level`/`grade` invalida la respuesta entera).
- **P3:** la propuesta nunca se escribe en el perfil; se muestra como «pendiente de decisión».
- **P4 (Ana Eslava-Graterol, 11 nov): actor del `progressed` = el alumno, en B2B y en B2C.** La validación del profesor es externa a la app: constata el nivel con otra evaluación (oral, escrita) y no entra en la LRS. Por eso la app nunca emite un `progressed` en nombre del profesor ni de un agente. **Lo que la app debe garantizar:** que la evidencia que sostiene cada `progressed` (respuestas, errores, citas y descriptores) se pueda ver en los paneles. *Sustituye a:* «todo `progressed` exige actor humano + `evidenceReviewed: true`; si no, la puerta lo rechaza».
- **P5:** el perfil no cambia por desempeño sin decisión humana (R-DESAJUSTE-1: 3 sesiones desajustadas → marca «revisar», perfil intacto).
- **P6 (Ana Eslava-Graterol, 11 nov): el test de nivel de la app se desactiva.** Cambiaba el nivel del alumno sin dejar sentencia y sin profesor, y los generadores usaban ese nivel.
- **Base legal:** AI Act art. 14 + Anexo III 3(b)/(c) · RGPD art. 22.
- **Incidentes propios:** `incident/nivel-sin-decision-humana` · `incident/nivel-propuesto-escrito-en-perfil` (severidad alta: detienen la emisión).

## Decisión de nivel en B2C: el usuario libre, sin profesor (v1.5)

*B2C = usuario libre (`user-track: free`): no tiene profesor y no forma parte de los entornos educativos oficiales (Ana, 11 nov).* *Su `progressed` sigue la regla general de G-NIVEL-1 P4: el actor es el alumno.*

> **Regla:** para el usuario libre, el código propone y **el propio usuario decide sobre su perfil tras ver la evidencia**; en los casos de mayor impacto la decisión exige **revisor humano**.

- **Propuesta con evidencia:** la propuesta (regla pública del 80 %) se muestra con los descriptores evidenciados y su cita literal; el usuario acepta o no. Si ignora, nada cambia (P3/P5 intactos).
- **Rastro de la decisión del usuario libre:** su aceptación sí ocurre dentro de la app, así que su `progressed` lleva actor = UUID del usuario + `evidenceReviewed: true` + versión de la regla.
- **Revisión humana obligatoria** en tres casos: salto de dos niveles o más (p. ej. A2→B2), entrada en nivel C, o disputa del usuario.
- **Nunca hacia abajo sin aceptación:** una propuesta de bajada se notifica, no se aplica; si se ignora, el perfil se mantiene y R-DESAJUSTE-1 marca «revisar».
- **Sin patrones oscuros:** aceptar no puede ser más atractivo que rechazar; sin presión ni cuenta atrás.
- **Menores:** si el canal libre admite menores, la autoaceptación no es válida — exige mayoría de edad o revisión de un adulto responsable.
- Regla adoptada del análisis del 9 nov (opción híbrida recomendada); entra en vigor con las firmas de pedagogía e ingeniería (N12).

## T-NIVEL-1 — Test automático en cada despliegue

- **a.** Respuesta del modelo con `{"level":"b2"}` → rechazo total + incidente; nada se calcula.
- **b.** `progressed` cuyo actor no es el alumno (un agente, la app o el profesor) → rechazado antes de la LRS (P4, 11 nov).
- **c.** 3 sesiones simuladas con evidencia de otro nivel → perfil intacto + «revisar» + incidente.

## R-ADM — Admisión de un agente nuevo (las 5 reglas)

1. **R-ADM-1 · Mapa:** registro previo en el mapa canónico con justificación.
2. **R-ADM-2 · Modelo fijado:** versión concreta, sin fallback. La temperatura no es condición de admisión (principio de invariancia, 10 nov): el agente demuestra su estabilidad con la prueba de la misma entrada repetida. Hasta el 10 nov decía «temperatura fijada».
3. **R-ADM-3 · Base cerrada:** solo el bundle oficial; nada de copyright; nada «del modelo».
4. **R-ADM-4 · Prompt con hash (N3):** producción == aprobado o no arranca.
5. **R-ADM-5 · Firma:** ficha firmada por pedagogía e ingeniería antes del despliegue.

## Clasificación de componentes (agente vs. infraestructura)

- ¿Es determinista (misma entrada → misma salida)? → **infraestructura**, no es agente (ASR, OCR, planificador SRS). Se gobierna con puerta de confianza, contrato no-train y sin almacenar la entrada cruda.
- ¿Es generativo y cabe en una pieza canónica? → **se absorbe** (los 4 generadores → pieza 5; la Pista → pieza 1).
- ¿No cabe en ninguna? → **examen R-ADM completo o retirada**.

## R-ID — Identificación de los agentes en el registro (v1.7)

**Fundamento (estándar xAPI 1.0.3 publicado por ADL, xAPI-Data):**
- §2.4.6, propiedad `instructor` del contexto: «Agent (MAY be a Group). Instructor that the Statement relates to, if not included as the Actor of the Statement.»
- §2.4.2.1: «An Agent MUST be identified by one (1) of the four types of Inverse Functional Identifiers».
- §2.4.2.4: el objeto `account` exige `homePage` (IRL del sistema) y `name` (identificador único en ese sistema).

**Regla del actor (decisión de la autora, 10 nov; sustituye la decisión 53):**
- **El actor de toda sentencia de aprendizaje es el alumno.** Aplica a `completed`, `answered`, `attempted`, `mediated` y `adapted`.
- **El agente de IA que interviene va en `context.instructor`**, con su `account`. Si intervienen dos a la vez (p. ej. el Corrector y el Juez), va un **Group** con los dos.
- **Las anulaciones (`voided`) llevan como actor la cuenta del sistema**, `tk-coach-engine`. Es un acto de sistema, no de un agente de IA.
- **La `authority` la pone el LRS** a partir de la clave de servicio. La app no la escribe (N9).
- **Fundamento de diseño:** la IA no califica. El Evaluador aporta evidencia, el código calcula (N10) y el profesor valida el nivel fuera de la app (G-NIVEL-1). Por eso el logro es del alumno y el agente consta como quien intervino.

**Qué recibe identificador de agente (enlace con la clasificación de componentes):**
- **Todo componente generativo que actúa en el aprendizaje o habla con el usuario.** Cada función tiene un identificador.
- **Teo, el agente de soporte, se declara en el registro** (`support-agent`, decisión de la autora, 10 nov). Está fuera del aprendizaje, pero habla con el usuario (art. 50). **Nunca aparece en una sentencia de aprendizaje** (si aparece, salta A2); su rastro es el registro de llamadas.
- **Nunca reciben identificador de agente ni aparecen en `instructor`:**
  - la infraestructura (ASR, OCR, planificador SRS);
  - el código (consolidador, guardián, límite de ritmo).

**Forma exacta de los identificadores** (equivalente a la regla de IRIs del 24 sep: «0 verbos ADL en https://», «0 verbos MLLDE en http://», que se mantiene):
1. Un solo identificador, `account`; nunca `mbox` ni `openid`.
2. `homePage` exacta: `https://tkcoach.talketika.app`. Con «s», en minúsculas, sin barra final y sin ruta.
3. `account.name` exacto, tal como está en el registro de identificadores: en minúsculas, con guiones y terminado en `-agent`. La única excepción es la cuenta del sistema, `tk-coach-engine`.
4. La etiqueta `name` (p. ej. «Capi») no identifica; los controles filtran siempre por `account.name`.
5. La versión nunca va en el nombre (nada de `capi-agent-v2`): va en `ext/agent-version`.
6. Un identificador no se renombra ni se reutiliza; el de un agente retirado no se asigna a otro.
7. La `authority` no la escribe la app: la pone el LRS (`https://tk-coach-prod.lrs.io/keys/<clave>`).

**Detección de salidas de rol** (en el control diario y en la auditoría con el export del LRS):
- **A1:** un `instructor` que no está en el registro indica un agente no autorizado.
- **A2:** un agente en un verbo o flujo que no es el suyo indica una salida de rol. Por ejemplo, cualquier agente distinto del Evaluador en un `completed`.
- **A3:** un agente como actor de una sentencia de aprendizaje.
- **A4:** una llamada registrada (N8 de la spec) sin sentencia o sin `instructor`.

**Cierre:**
- 0 cuentas de agente con otra `homePage`;
- 0 `account.name` fuera del registro;
- 0 agentes como actor de una sentencia de aprendizaje;
- 0 sentencias nuevas con `authority` personal.

**Línea de base (export de Veracity, 10 nov, 2.243 sentencias):**
- `account` como único identificador: 2.243 de 2.243;
- una sola `homePage`, la correcta: 2.243 de 2.243;
- 0 sentencias con `context.instructor`;
- `capi-agent` como actor en 141 `adapted`;
- `tk-coach-engine` en 36 `voided`;
- `authority` = la clave personal de un miembro del equipo, no la de servicio, en 2.243 de 2.243.

**Prueba de cumplimiento** (principio de verificación):
- el ID de una sentencia nueva con `instructor`;
- el extracto de código;
- la fecha desde la que se cumple.

Entra en vigor con las firmas de pedagogía e ingeniería (N12).

## Vocabulario desde imágenes o prompts — doble vía según el tipo de usuario (v1.3)

- **Alumno institucional (piloto) — Vía A (por defecto):** el componente solo puede SELECCIONAR términos que ya existen en el inventario (`en.voc.*`); validación contra allow-list en código; lo que no está, se descarta. El contenido lo fija el programa, para que la medición sea comparable.
- **Alumno institucional — Vía B (vocabulario nuevo):** el componente PROPONE candidatos a una cola de revisión humana; entran al inventario en el próximo bump de versión con fecha desde la que cuentan. El componente nunca escribe en la base.
- **Usuario libre — vía propia (selección del propio usuario):** el input lo genera él (su imagen, su presentación). Sus tarjetas de vocabulario las selecciona **el propio usuario** de entre los términos extraídos de su material; el código valida el formato y exige el origen (`own-image`), sin pasar por la cola del inventario. **Justificación CLIL/AICLE:** la lengua se aprende a través de contenido significativo para el aprendiz; su contexto y su necesidad comunicativa real deciden qué vocabulario se trabaja.
- **Prohibido en ambas vías:** que vocabulario generado por IA alimente tarjetas o drills sin validación en código y origen declarado.
- En ambos casos, el vocabulario de contenido es **práctica sin medición** (decisión 51): maestría objetiva por SRS, nunca banda.

## Alcance del lector OCR y medición en toda interacción (v1.3)

- El lector OCR decide **sobre la imagen, nunca sobre el alumno**: extrae texto y términos del estímulo; no evalúa.
- **Toda interacción** contrasta la producción del usuario con la base completa — 381 descriptores A1–C2 medibles desde texto (inventario de 382; se excluye un descriptor de pronunciación) — con `ext/input-channel` declarado.
- El **nivel real vs declarado** lo computa el código (regla pública del 80 %, umbrales v0.7.2); el Evaluador nunca recibe el nivel declarado (P1, anti-anclaje). Los descriptores que el usuario evidencia con cita literal seleccionan el contenido de la fase Process siguiente (i+1 por código).
- El `progressed` lleva siempre al alumno como actor, y la acreditación del nivel es una validación externa a la app (G-NIVEL-1); **para el usuario libre, rige la regla de la sección «Decisión de nivel del usuario libre, sin profesor» (v1.5).** (Hasta el 11 nov esta línea decía, por error, que estaba pendiente de definir.) El OCR es infraestructura: se registra con `ext/input-channel: ocr` y nunca va en `context.instructor` (R-ID).

## Propuesta de acuñación de IRIs — bump v0.8.4 del registro (v1.6)

Análisis del registro publicado v0.8.3 (153 conceptos) frente a estas normas. **No hacen falta verbos nuevos:** los ADL reusados (`progressed`, `attempted`, `completed`, `passed`, `failed`, `interacted`, `asked`, `answered`) y los 3 acuñados (`pronounced`, `mediated`, `adapted`) cubren todas las propuestas — la aceptación del usuario libre (v1.5) es un `progressed` con actor propio, no un verbo nuevo.

**Urgente — las normas ya los citan y no existen en el registro:**

| IRI propuesto | Tipo | Motivo |
|---|---|---|
| `incident/nivel-sin-decision-humana` | incidente | G-NIVEL-1 lo nombra; la tabla de incidentes no lo tiene |
| `incident/nivel-propuesto-escrito-en-perfil` | incidente | Ídem — hoy son referencias huérfanas |

**Altos — cierran hallazgos de la auditoría:**

| IRI propuesto | Tipo | Motivo |
|---|---|---|
| `ext/descriptor-results` | resultado | Salida por descriptor `{id, evidenciado, cita}`; sin ella no hay evidencia visible para la autoaceptación v1.5 (prevista en v0.9) |
| `ext/vocabulary-origin` | contexto | Valores cerrados: `inventory · correction · prompt · image · summary · own-image`; es el campo que llegaba «undefined» en 16 términos |
| `ext/user-track` | contexto | `pilot · free`; hace auditable la doble vía y la decisión por colectivo |

**Medios — hacen R-MED-1 y N6 comprobables por máquina:**

| IRI propuesto | Tipo | Motivo |
|---|---|---|
| `ext/flow` | contexto | `measurement · pedagogy · activity`; hoy N7 es una regla escrita, no un dato en la LRS |
| `ext/agent-version` · `ext/rules-version` · `ext/prompt-hash` · `ext/kb-version` | contexto | N6/N3/N4 los exigen en cada statement y solo existe `ext/measure-model` |
| `ext/ocr-confidence` | resultado | Análogo a `ext/asr-confidence` para la puerta OCR |

**Campos nuevos dentro de `ext/level-decision` (bump del objeto, no IRI nuevo):** `decisionActor` (self · reviewer; `teacher` sale el 11 nov: la decisión del profesor no entra en la LRS, P4) · `evidenceReviewed` (boolean, P4) · `status` (proposed · accepted · rejected · pending) · `reviewTrigger` (none · jump2plus · c-entry · dispute).

**Lo que NO se acuña:** bajadas sin aceptación, patrones oscuros y menores son reglas de código, UX y onboarding; se auditan en T-NIVEL-1 y en revisión de diseño, no en la LRS. Los IRIs funcionan como identificadores aunque `w3id.org/mllde` siga en PR; conviene resolver el namespace antes de publicar v0.8.4. Propuesta del análisis del 9 nov; entra en vigor con las firmas de pedagogía e ingeniería (N12).

## El guardián (regla específica)

Ningún agente puede **analizar y corregir el sistema por su cuenta**. Un vigilante solo alerta (fail-closed, sin acceso de escritura). Su función la cubre la prueba N3 + CI: auditable, repetible y sin privilegios.

---

*Método MLLDE © 2026 Ana Eslava-Graterol (UPV). Preparado con asistencia de IA y revisado por la autora, en el espíritu del art. 50 del Reglamento (UE) 2024/1689.*
