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
| `mllde-xapi-profile_v0.8.3.jsonld` | **Current** xAPI **Profile** (JSON-LD, `conformsTo w3id.org/xapi/profiles#1.0`; 153 concepts, 6 statement templates), ready to import/validate on an xAPI Profile Server or LRS. |
| `mllde-xapi-profile_v0.8.2.jsonld` | Previous Profile — superseded by v0.8.3, kept for provenance. |
| `mllde-xapi-iri-registry_v0.8.2.json` | The IRI registry (JSON): verbs, activity types, extensions, CEFR levels/skills/scales, rubric categories, pedagogical actions, evidence tiers, incident types, acoustic metrics. (A matching v0.8.3 JSON is pending; the v0.8.3 vocabulary is authoritative in `index.html` and in the Profile.) |
| `index.html` | Human-readable registry of every IRI, **v0.8.3** (served via GitHub Pages). |
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
1. **Profile (published, v0.8.3):** `mllde-xapi-profile_v0.8.3.jsonld` — a self-contained JSON-LD document; it does not depend on any external server.
2. **Persistent IRIs:** register `w3id.org/mllde` (PR to `perma-id/w3id.org` using `w3id/mllde/`). This is the durable, vendor-independent home for the vocabulary and the Profile.
3. **Discovery (optional / reference):** `adlnet/xapi-authored-profiles` exists but was **archived (read-only) on 2026-03-12** — it no longer accepts PRs, so it serves as a reference/template (`adl/adl.jsonld`), not a publication target. The xAPI Profiles spec is under review. MLLDE is therefore self-hosted here and resolved via w3id, independent of ADL; submit to a public registry if and when a stable one is available.

## Setup notes
- **GitHub Pages:** Settings → Pages → Source: `main` /`docs`. Docs resolve at
  `https://profeanaeslavaedtech.github.io/mllde-xapi/`.
- The `w3id/mllde/.htaccess` redirects `w3id.org/mllde/*` to that Pages URL.

---
© 2026 Ana Eslava-Graterol — MLLDE (Universitat Politècnica de València).
CEFR © Council of Europe · xAPI © ADL/IEEE · ESCO © European Union · IPA © IPA
(cited as standards, not redistributed). Licensed CC BY 4.0.
