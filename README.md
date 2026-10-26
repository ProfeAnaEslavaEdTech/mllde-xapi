# MLLDE xAPI

**MLLDE** (Mobile Language Learning Design Environment) is a framework for
designing language-learning products in which AI agents **measure** and a
deterministic engine and a human **decide**. This repository is MLLDE's
**measurement module**: the xAPI vocabulary, the machine-readable Profile, and
the human-readable registry used to measure **voice-based language learning**
against the **CEFR** descriptor scales (Companion Volume, 2020).

> No official IRI vocabulary exists for CEFR skills, subskills or mediation, and
> no language-learning xAPI Profile exists in ADL's registry. MLLDE mints its own
> namespace under `w3id.org/mllde`, **reuses** established ADL/w3id IRIs where the
> meaning matches, and records CEFR / ESCO / Europass alignments as metadata.

## Two versioning axes

Cite the work on two independent axes — do not conflate them:

| Axis | Version | What it is | Where it lives |
|---|---|---|---|
| **Content inventory** | **v0.7.1** | *What is taught* — 271 CEFR content descriptors (115 grammar, 86 vocabulary, 43 speaking, 27 mediation), A1–C1. | the application repository |
| **Measurement model** | **v0.8.3** | *How it is measured and recorded* — this registry and Profile. | **this repository** |

## Contents

| File | What it is |
|---|---|
| `mllde-xapi-profile_v0.8.3.jsonld` | **Current** xAPI **Profile** (JSON-LD, `conformsTo w3id.org/xapi/profiles#1.0`; 153 concepts, 6 statement templates). Import/validate on an xAPI Profile Server or LRS. |
| `mllde-xapi-profile_v0.8.2.jsonld` | Previous Profile — superseded by v0.8.3, kept for provenance. |
| `mllde-xapi-iri-registry_v0.8.2.json` | The IRI registry (JSON): verbs, activity types, extensions, CEFR levels/skills/scales, rubric categories, pedagogical actions, evidence tiers, incident types, acoustic metrics. A matching v0.8.3 JSON is pending; the v0.8.3 vocabulary is authoritative in `index.html` and in the Profile. |
| `index.html` | Human-readable registry of every IRI, **v0.8.3** (served via GitHub Pages). |
| `tk-coachai-mllde.html` | Interactive TK CoachAI · MLLDE visual. |
| `w3id/ids/mllde/` | Payload for the `w3id.org/mllde` namespace pull request (`.htaccess` + `README.md`), mirroring the destination path in `perma-id/w3id.org`. |
| `LICENSE` | CC BY 4.0. |

## Scheme rule (one canonical IRI per authority)

- **Reused ADL verbs** (`completed`, `attempted`, `answered`, `progressed`, …) → canonical **`http://adlnet.gov/expapi/verbs/*`**. MLLDE coins a verb only when ADL has no equivalent.
- **Minted MLLDE terms** (`adapted`, `mediated`, `pronounced`, all `ext/*`, CEFR skills/levels/scales, rubric, tiers, incidents) → **`https://w3id.org/mllde/*`** (w3id is https).
- The verb `answered` has a **single source**: it is defined only as the ADL IRI; any `w3id.org/mllde/verb/answered` is historical and is not in the Profile.

## The measurement firewall

The competence **band** comes **only** from the `completed` statement (an
evaluated spoken session, `rubric-scores` 0–10). Grammar drills and vocabulary
cards emit practice signals (`item-score`, `srs-outcome`) that feed the loop and
spaced repetition — **never a band**. The firewall is encoded in the Profile's
statement templates (`attempted-card-firewall`, `answered-practice-firewall`,
`completed-measurement`), so an analyst reading the LRS can tell measurement from
practice **from the template alone**.

The CEFR-anchored band is produced **once per completed session**, not per turn.
It is read from the session transcript, so a turn scores whether spoken or typed;
only the repetition (pronunciation) exercise requires audio, and the ASR-confidence
gate (0.70) applies to voice turns alone (`ext/input-channel`). Mediation is scored
within the same session rubric, so the session band reflects both spoken
interaction and mediation.

## Availability

- The **vocabulary, registry and Profile (v0.8.3)** are public under **CC BY 4.0** at
  `https://profeanaeslavaedtech.github.io/mllde-xapi/` — open the registry for
  review, or import `mllde-xapi-profile_v0.8.3.jsonld` for use.
- **Learner-level xAPI records** are not released here, for data-protection
  reasons, and are available on reasonable request in anonymised, aggregated form.

## Roadmap

1. **Profile (published, v0.8.3):** `mllde-xapi-profile_v0.8.3.jsonld` — a self-contained JSON-LD document; it does not depend on any external server.
2. **Persistent IRIs (PR prepared):** the payload in `w3id/ids/mllde/` is ready; open a pull request to `perma-id/w3id.org` adding the directory **`ids/mllde/`** (identifiers live under `ids/`, not the repo root) with this `.htaccess`. On merge, `w3id.org/mllde/*` resolves: `/profile` → the JSON-LD Profile, all other paths → the registry (302). This is the durable, vendor-independent home for the vocabulary.
3. **Discovery (reference only):** `adlnet/xapi-authored-profiles` was **archived (read-only) on 2026-03-12** and no longer accepts PRs; it serves as a template, not a publication target. MLLDE is therefore self-hosted here and resolved via w3id, independent of ADL; submit to a public registry if and when a stable one is available.

## Setup notes

- **GitHub Pages:** Settings → Pages → Source serves the registry at
  `https://profeanaeslavaedtech.github.io/mllde-xapi/`.
- `w3id/ids/mllde/.htaccess` (destined for `ids/mllde/.htaccess` in `perma-id/w3id.org`) redirects `w3id.org/mllde/*` to that Pages URL.

---
© 2026 Ana Eslava-Graterol — MLLDE (Universitat Politècnica de València).
CEFR © Council of Europe · xAPI © ADL/IEEE · ESCO © European Union · IPA © IPA
(cited as standards, not redistributed). Licensed CC BY 4.0.
