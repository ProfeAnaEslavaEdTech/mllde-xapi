# Registro de identificadores de los agentes MLLDE · TK CoachAI

**Versión:** 1.0 · **Fecha:** 10 nov 2026 · **Regla:** R-ID, en las normas de gobernanza v1.7.

**Qué contiene esta carpeta:** el objeto xAPI exacto de cada agente, para usarlo como plantilla en `context.instructor`.

**Cómo se usa:**
- El actor de toda sentencia de aprendizaje es el alumno.
- El agente que interviene va en `context.instructor` con el objeto de su archivo, **copiado tal cual**.
- Si intervienen dos agentes a la vez, va un `Group` con los dos objetos.

**Fundamento** (xAPI 1.0.3, ADL, xAPI-Data §2.4.6): «Agent (MAY be a Group). Instructor that the Statement relates to, if not included as the Actor of the Statement.»

**Registrado no es aprobado.** Un identificador no autoriza a un agente a actuar. Para eso necesita su ficha aprobada con las dos firmas (N1, N4); los agentes 8–10 necesitan además la N14.

| # | Agente | `account.name` | Plantilla |
|---|---|---|---|
| 1 | Generador de misiones | `mission-agent` | `agentes/mission-agent.json` |
| 2 | Capi | `capi-agent` | `agentes/capi-agent.json` |
| 3 | Corrector | `corrector-agent` | `agentes/corrector-agent.json` |
| 4 | Juez del tip | `judge-agent` | `agentes/judge-agent.json` |
| 5 | Evaluador MLLDE | `evaluator-agent` | `agentes/evaluator-agent.json` |
| 6 | Generador de drills | `drill-agent` | `agentes/drill-agent.json` |
| 7 | Generador de tarjetas | `card-agent` | `agentes/card-agent.json` |
| 8 | Verificador de drills | `drill-judge-agent` | `agentes/drill-judge-agent.json` |
| 9 | Generador de mediación | `mediation-agent` | `agentes/mediation-agent.json` |
| 10 | Redactor del resumen | `summary-agent` | `agentes/summary-agent.json` |
| 11 | Teo | `support-agent` | `agentes/support-agent.json` |
| — | Cuenta de sistema (anulaciones; no es IA) | `tk-coach-engine` | `agentes/tk-coach-engine.json` |

**Forma exacta** (R-ID):
- solo `account`;
- `homePage` = `https://tkcoach.talketika.app`;
- `account.name` tal cual, sin la versión. La versión va en `ext/agent-version`.

Un identificador no se renombra ni se reutiliza.

**El detalle de cada agente** (tipo, pieza, función y dónde puede aparecer) está en `registro-agentes.json`.
