# MLLDE xAPI

**MLLDE** (Measurement Module for Language Learning Data & Evidence) — an xAPI
vocabulary and Profile for measuring **voice-based language learning** against the
**CEFR** descriptor scales (Companion Volume, 2020).

> No official IRI vocabulary exists for CEFR skills, subskills or mediation, and no
> language-learning xAPI Profile exists in ADL's registry. MLLDE mints its own
> namespace under `w3id.org/mllde`, **reuses** established ADL/w3id IRIs where the
> meaning matches, and records CEFR / ESCO / Europass alignments as metadata.

## Contents
| File | What it is |
|---|---|
| `mllde-xapi-iri-registry_v0.8.2.json` | The IRI registry: verbs, activity types, extensions, CEFR levels/skills/scales, rubric categories, pedagogical actions, evidence tiers, incident types, acoustic metrics. |
| `mllde-xapi-profile_v0.8.2.jsonld` | The xAPI **Profile** (JSON-LD, `conformsTo w3id.org/xapi/profiles#1.0`), ready to import/validate on the ADL xAPI Profile Server. |
| `docs/index.html` | Human-readable documentation of every IRI (served via GitHub Pages). |
| `w3id/mllde/` | Files for the `w3id.org/mllde` namespace Pull Request (`.htaccess` + `README.md`). |
| `LICENSE` | CC BY 4.0. |

## Scheme rule (one canonical IRI per authority)
- **Reused ADL verbs** (`completed`, `attempted`, `answered`, …) → canonical **`http://adlnet.gov/expapi/verbs/*`**.
- **Minted MLLDE terms** (`adapted`, `mediated`, `pronounced`, all `ext/*`) → **`https://w3id.org/mllde/*`** (w3id is https).

## The measurement firewall
The competence **band** comes **only** from the `completed` statement (an evaluated
spoken session, `rubric-scores` 0–10). Grammar drills and vocabulary cards emit
practice signals (`item-score`, `srs-outcome`) that feed the loop and spaced
repetition — **never a band**.

## Roadmap
1. **Profile (done):** `mllde-xapi-profile_v0.8.2.jsonld`.
2. **Persistent IRIs:** register `w3id.org/mllde` (PR to `perma-id/w3id.org` using `w3id/mllde/`).
3. **Authored Profile:** publish on the ADL xAPI Profile Server (`profiles.adlnet.gov`).

## Setup notes
- **GitHub Pages:** Settings → Pages → Source: `main` /`docs`. Docs resolve at
  `https://profeanaeslavaedtech.github.io/mllde-xapi/`.
- The `w3id/mllde/.htaccess` redirects `w3id.org/mllde/*` to that Pages URL.

---
© 2026 Ana Eslava-Graterol — MLLDE (Universitat Politècnica de València).
CEFR © Council of Europe · xAPI © ADL/IEEE · ESCO © European Union · IPA © IPA
(cited as standards, not redistributed). Licensed CC BY 4.0.
