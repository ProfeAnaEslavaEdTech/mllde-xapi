# w3id.org/mllde

**MLLDE** — Measurement Module for Language Learning Data & Evidence.
Namespace de identificadores persistentes (IRIs) para métricas de aprendizaje de
lenguas alineadas al MCER, usadas en statements xAPI.

## Qué identifica este namespace
IRIs bajo `https://w3id.org/mllde/…` para:
- **Verbos** acuñados (`/verb/adapted`, `/verb/mediated`, `/verb/pronounced`).
- **Tipos de actividad** (`/activity-type/mission`, `/grammar-drill`, `/vocabulary-card`, …).
- **Extensiones** de contexto y resultado (`/ext/rubric-scores`, `/ext/asr-confidence`,
  `/ext/evidence-tier`, `/ext/content-ref`, …).
- **Escalas MCER** (`/cefr/level/*`, `/cefr/skill/*`, `/cefr/scale/*`), categorías de
  rúbrica, acciones pedagógicas, tiers de evidencia y tipos de incidente.

Los verbos y tipos que ya existen en ADL se **reusan** (no se re-acuñan aquí):
los verbos ADL van en su forma canónica `http://adlnet.gov/expapi/verbs/*`.

## Política de resolución
Todos los IRIs bajo `/mllde/` redirigen a la documentación legible del registro
(ver `.htaccess`). Los IRIs son identificadores estables: no requieren resolver a
una web, pero se procura que apunten a documentación humana.

## Mantenimiento
- **Responsable:** Ana Eslava-Graterol — MLLDE (Universitat Politècnica de València).
- **GitHub:** profeanaeslavaedtech
- **Contacto:** (añade tu email de contacto aquí)
- **Registro fuente:** MLLDE xAPI IRI Registry v0.8.2.
- **Perfil xAPI:** publicado / en publicación en el ADL xAPI Profile Server.

## Licencia / propiedad
© 2026 Ana Eslava-Graterol. Metodología MLLDE. MCER © Council of Europe;
xAPI © ADL/IEEE (citados como estándares, no redistribuidos).
