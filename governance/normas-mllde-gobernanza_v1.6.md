# Normas de gobernanza MLLDE — paquete descargable
**Versión:** 1.6 · **Fecha:** 9 de noviembre de 2026 · **Cambio v1.6:** propuesta de acuñación de IRIs (bump v0.8.4 del registro) tras el análisis del registro publicado v0.8.3 — sin verbos nuevos; 7 extensiones, 4 campos en `ext/level-decision` y 2–3 tipos de incidente. **Cambio v1.5:** regla de decisión de nivel para el usuario libre sin profesor — el código propone y el propio usuario acepta tras ver la evidencia, con revisor humano obligatorio en saltos de dos niveles, entrada en nivel C o disputa; menores excluidos de la autoaceptación. **Cambio v1.4:** regla principal de gobernanza (R-MED-1) — toda medición pasa por el flujo de medición contra la base completa y ningún otro agente mide por su cuenta. **Cambio v1.3:** doble vía de vocabulario según el tipo de usuario (decisión de la autora), alcance del lector OCR (decide sobre la imagen, nunca sobre el alumno) y regla de medición en toda interacción con comparación nivel real vs declarado. **Cambio v1.2:** tabla de equivalencia con la numeración de la spec del Evaluador v2 (§6.1) y nota sobre la referencia huérfana «N14» de la Cartilla de los 7.
**Principio rector:** La base define · la IA localiza · el código calcula · el profesor decide · la LRS lo registra.

> Estas normas gobiernan a todo agente de IA del modelo MLLDE y de sus aplicaciones (p. ej. TK CoachAI). Un agente que no está en el mapa no entra en el loop.

## R-MED-1 — Regla principal: toda medición pasa por el flujo de medición

> **REGLA PRINCIPAL, vinculante para todo agente de IA:** la producción del usuario la contrasta siempre el flujo de medición contra la base completa — **381 descriptores A1–C2 (gram 115 · voc 96 · spk 100 · med 71)** —, con `ext/input-channel` declarado. **Ningún otro agente mide, puntúa ni evalúa al usuario por su cuenta.**

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
| **N5 — Modelos fijos** | Modelo con versión fijada por escrito; contrato no-train verificado; **sin fallback jamás** (lección Gemini, 5–19 oct). |
| **N6 — Trazabilidad** | `agent-id` + `agent-version` + `measure-model` + `rules-version` en cada statement. Meta: 5 de 5 con rastro propio. |
| **N7 — Flujos que no se cruzan** | Medición (1×/sesión), pedagogía (por turno), actividad (loop). La banda solo nace del flujo de medición. |
| **N8 — Fail-closed** | Ante la duda, no emite: puerta ASR 0.70, juez no disponible → sin tip, esquema inválido → descarte. |
| **N9 — PII** | Al modelo solo va UUID + transcripción; nunca nombre, empresa, puesto ni correo. Autoridad LRS = cuenta de servicio, nunca credencial personal. |
| **N10 — Cero cálculos en LLM** | Ningún agente genera números de competencia: notas (5.2/5.3), banda (fórmula del 26/08), i+1 y nivel propuesto los calcula el código. |
| **N11 — Incidentes declarados** | Cada agente define sus tipos de incidente con IRI del registry; van a su registro, nunca a KPIs del alumno. |
| **N12 — Versionado firmado** | Cambio de prompt/modelo/reglas = bump + firma (pedagogía + ingeniería) + entrada en el mapa + fecha desde la que cuenta. |
| **N13 — Pruebas en CI** | Toda prueba de admisión corre en CI en cada despliegue; si falla, el despliegue se bloquea. |

### Equivalencia con la numeración de la spec del Evaluador v2 (§6.1)

> **Aviso de numeración.** La spec del Evaluador v2 (8 nov) numera sus normas de otra forma a partir de N4, y la Cartilla de los 7 (8 nov) cita esa numeración de la spec (p. ej. «N9 = modelo exacto»). Para que el comité no encuentre dos «N9» distintas, esta es la correspondencia oficial:

| Spec Evaluador v2 (§6.1) | Equivalente en este paquete v1.1 |
|---|---|
| N1 · Registro cerrado | **N1** (misma regla) |
| N2 · Puerta única de llamadas a modelos | **N2** (aquí con énfasis en la emisión a la LRS) |
| N3 · Prueba anti-agentes sueltos (incluye prompt-hash) | **N3** (misma regla) |
| N4 · Ficha antes que código (solicitud justificada + dos firmas) | **R-ADM-1 y R-ADM-5** |
| N5 · Una función por agente; ningún agente decide | Principio rector + **N10** |
| N6 · Bloque común obligatorio en cada prompt | ➕ **Ausente en v1.1 — incorporar** (texto literal en la spec §6.2) |
| N7 · La base se hereda por código | **N4** |
| N8 · Trazabilidad (actor = el agente que actúa) | **N6** |
| N9 · Modelos aprobados y fijos, sin respaldo | **N5** |
| N10 · Datos mínimos (sin datos personales) | **N9** |
| N11 · Cambios = versión nueva, con prueba y firmas | **N12** |
| N12 · Auditoría periódica (agentes ↔ llamadas ↔ Veracity) | ➕ **Ausente en v1.1 — incorporar** |
| N13 · Retirada de agentes sin ficha en plazo | ➕ **Ausente en v1.1 — incorporar** |

> **Sobre la «N14» que cita la Cartilla de los 7:** la spec del Evaluador v2 termina en N13; **N14 («necesidad demostrada») no existe en ninguna fuente** — es una referencia huérfana de la cartilla. La necesidad demostrada ya la exige la N4 de la spec (solicitud justificada + dos firmas). Si se quiere como norma propia, se acuña como norma nueva con versión y firmas (N12 de este paquete), no se cita como existente.

## G-NIVEL-1 — El nivel: la IA propone, el profesor decide

- **REGLA:** el nivel lo PROPONE una regla pública — el nivel más alto con **≥80% de descriptores evidenciados con cita literal** (umbrales v0.7.2: A1 48 · A2 52 · B1 63 · B2 58 · C1 48 · C2 40) — y lo DECIDE el profesor, fuera del sistema.
- **P1:** ningún agente recibe el nivel declarado del alumno (anti-anclaje).
- **P2:** ningún modelo devuelve niveles ni notas (un campo `level`/`grade` invalida la respuesta entera).
- **P3:** la propuesta nunca se escribe en el perfil; se muestra como «pendiente de decisión».
- **P4:** todo `progressed` exige actor humano + `evidenceReviewed: true`; si no, la puerta lo rechaza.
- **P5:** el perfil no cambia por desempeño sin decisión humana (R-DESAJUSTE-1: 3 sesiones desajustadas → marca «revisar», perfil intacto).
- **Base legal:** AI Act art. 14 + Anexo III 3(b)/(c) · RGPD art. 22.
- **Incidentes propios:** `incident/nivel-sin-decision-humana` · `incident/nivel-propuesto-escrito-en-perfil` (severidad alta: detienen la emisión).
- **Usuario libre (sin profesor):** ver la sección siguiente (v1.5).

## Decisión de nivel del usuario libre, sin profesor (v1.5)

> **Regla:** para el usuario libre, el código propone y **el propio usuario decide sobre su perfil tras ver la evidencia**; en los casos de mayor impacto la decisión exige **revisor humano**.

- **Propuesta con evidencia:** la propuesta (regla pública del 80 %) se muestra con los descriptores evidenciados y su cita literal; el usuario acepta o no. Si ignora, nada cambia (P3/P5 intactos).
- **P4 cumplido:** todo `progressed` lleva actor = UUID del usuario + `evidenceReviewed: true` + versión de la regla.
- **Revisión humana obligatoria** en tres casos: salto de dos niveles o más (p. ej. A2→B2), entrada en nivel C, o disputa del usuario.
- **Nunca hacia abajo sin aceptación:** una propuesta de bajada se notifica, no se aplica; si se ignora, el perfil se mantiene y R-DESAJUSTE-1 marca «revisar».
- **Sin patrones oscuros:** aceptar no puede ser más atractivo que rechazar; sin presión ni cuenta atrás.
- **Menores:** si el canal libre admite menores, la autoaceptación no es válida — exige mayoría de edad o revisión de un adulto responsable.
- Regla adoptada del análisis del 9 nov (opción híbrida recomendada); entra en vigor con las firmas de pedagogía e ingeniería (N12).

## T-NIVEL-1 — Test automático en cada despliegue

- **a.** Respuesta del modelo con `{"level":"b2"}` → rechazo total + incidente; nada se calcula.
- **b.** `progressed` sin actor humano → rechazado antes de la LRS.
- **c.** 3 sesiones simuladas con evidencia de otro nivel → perfil intacto + «revisar» + incidente.

## R-ADM — Admisión de un agente nuevo (las 5 reglas)

1. **R-ADM-1 · Mapa:** registro previo en el mapa canónico con justificación.
2. **R-ADM-2 · Modelo fijado:** versión concreta, temperatura fijada, sin fallback.
3. **R-ADM-3 · Base cerrada:** solo el bundle oficial; nada de copyright; nada «del modelo».
4. **R-ADM-4 · Prompt con hash (N3):** producción == aprobado o no arranca.
5. **R-ADM-5 · Firma:** ficha firmada por pedagogía e ingeniería antes del despliegue.

## Clasificación de componentes (agente vs. infraestructura)

- ¿Es determinista (misma entrada → misma salida)? → **infraestructura**, no es agente (ASR, OCR, planificador SRS). Se gobierna con puerta de confianza, contrato no-train y sin almacenar la entrada cruda.
- ¿Es generativo y cabe en una pieza canónica? → **se absorbe** (los 4 generadores → pieza 5; la Pista → pieza 1).
- ¿No cabe en ninguna? → **examen R-ADM completo o retirada**.

## Vocabulario desde imágenes o prompts — doble vía según el tipo de usuario (v1.3)

- **Alumno institucional (piloto) — Vía A (por defecto):** el componente solo puede SELECCIONAR términos que ya existen en el inventario (`en.voc.*`); validación contra allow-list en código; lo que no está, se descarta. El contenido lo fija el programa, para que la medición sea comparable.
- **Alumno institucional — Vía B (vocabulario nuevo):** el componente PROPONE candidatos a una cola de revisión humana; entran al inventario en el próximo bump de versión con fecha desde la que cuentan. El componente nunca escribe en la base.
- **Usuario libre — vía propia (selección del propio usuario):** el input lo genera él (su imagen, su presentación). Sus tarjetas de vocabulario las selecciona **el propio usuario** de entre los términos extraídos de su material; el código valida el formato y exige el origen (`own-image`), sin pasar por la cola del inventario. **Justificación CLIL/AICLE:** la lengua se aprende a través de contenido significativo para el aprendiz; su contexto y su necesidad comunicativa real deciden qué vocabulario se trabaja.
- **Prohibido en ambas vías:** que vocabulario generado por IA alimente tarjetas o drills sin validación en código y origen declarado.
- En ambos casos, el vocabulario de contenido es **práctica sin medición** (decisión 51): maestría objetiva por SRS, nunca banda.

## Alcance del lector OCR y medición en toda interacción (v1.3)

- El lector OCR decide **sobre la imagen, nunca sobre el alumno**: extrae texto y términos del estímulo; no evalúa.
- **Toda interacción** contrasta la producción del usuario con la base completa — 381 descriptores A1–C2 (gram 115 · voc 96 · spk 100 · med 71) — con `ext/input-channel` declarado.
- El **nivel real vs declarado** lo computa el código (regla pública del 80 %, umbrales v0.7.2); el Evaluador nunca recibe el nivel declarado (P1, anti-anclaje). Los descriptores que el usuario evidencia con cita literal seleccionan el contenido de la fase Process siguiente (i+1 por código).
- La decisión de cambiar el nivel exige actor humano (G-NIVEL-1): el profesor en el piloto; **para el usuario libre, la regla del actor decisor está pendiente de definir por la autora** — sin ella, la propuesta queda «pendiente de decisión» y el perfil no cambia (P3/P5).

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

**Campos nuevos dentro de `ext/level-decision` (bump del objeto, no IRI nuevo):** `decisionActor` (teacher · self · reviewer) · `evidenceReviewed` (boolean, P4) · `status` (proposed · accepted · rejected · pending) · `reviewTrigger` (none · jump2plus · c-entry · dispute).

**Lo que NO se acuña:** bajadas sin aceptación, patrones oscuros y menores son reglas de código, UX y onboarding; se auditan en T-NIVEL-1 y en revisión de diseño, no en la LRS. Los IRIs funcionan como identificadores aunque `w3id.org/mllde` siga en PR; conviene resolver el namespace antes de publicar v0.8.4. Propuesta del análisis del 9 nov; entra en vigor con las firmas de pedagogía e ingeniería (N12).

## El guardián (regla específica)

Ningún agente puede **analizar y corregir el sistema por su cuenta**. Un vigilante solo alerta (fail-closed, sin acceso de escritura). Su función la cubre la prueba N3 + CI: auditable, repetible y sin privilegios.

---

*Método MLLDE © 2026 Ana Eslava-Graterol (UPV). Preparado con asistencia de IA y revisado por la autora, en el espíritu del art. 50 del Reglamento (UE) 2024/1689.*
