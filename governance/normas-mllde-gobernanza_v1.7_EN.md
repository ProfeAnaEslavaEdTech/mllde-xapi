# MLLDE governance norms — downloadable package
**Version:** 1.7 · **Date:** 9–12 November 2026 · *English translation of `normas-mllde-gobernanza_v1.7.md`. If the two versions differ, the Spanish text prevails.* · **Change of 11 Nov (G-NIVEL-1):** two user modes, B2B and B2C. In both, `progressed` enters the LRS with the learner as actor, and the teacher's validation is external to the app. The AI does not decide: it compares the evidence with the descriptors. The app's level test is disabled (P6). **Change v1.7:** traceability rule N6-bis — weekly cmi5 audit package (author's decision, meeting of 9 Nov). Reminder in N9 of a prior agreement: the learner's name is added by the app when it presents the report, never by the model. Corrected note on N14: it exists since 8 Nov. Verification principle added next to the guiding principle. Role-invariance principle (temperature is no longer a compliance condition; R-ADM-2 adjusted). Teo (`support-agent`) declared in the registry, under AI Act art. 50(1). Identifier registry with one JSON per agent in `governance/registro-agentes/`. N6 points to `context.instructor`. Legal basis of N5 (AI Act checked against the Official Journal text, GDPR, ISO/IEC 42001). New section **R-ID**: identification of agents in the record (`context.instructor`, xAPI 1.0.3 §2.4.6) and exact form of their identifiers; it replaces the rule "actor = the agent that acts" (decision 53). **Change v1.6:** proposal to mint IRIs (registry bump v0.8.4) after analysing the published registry v0.8.3 — no new verbs; 7 extensions, 4 fields in `ext/level-decision` and 2–3 incident types. **Change v1.5:** level-decision rule for the free user without a teacher — code proposes and the user accepts after seeing the evidence, with a mandatory human reviewer for jumps of two levels, entry into level C or a dispute; minors excluded from self-acceptance. **Change v1.4:** main governance rule (R-MED-1) — every measurement goes through the measurement flow against the full base, and no other agent measures on its own. **Change v1.3:** two-track vocabulary by user type (author's decision), scope of the OCR reader (it decides about the image, never about the learner) and a rule of measurement in every interaction, comparing actual and declared level. **Change v1.2:** equivalence table with the numbering of the Evaluator v2 spec (§6.1) and a note on the orphan reference "N14" in the Primer of the 7.
**Guiding principle:** The base defines · the AI locates · the code computes · the teacher validates · the LRS records it. *(Until 12 Nov it read "the teacher decides"; it changes under G-NIVEL-1: the teacher's validation is external to the app.)*
**Verification principle (Ana Eslava-Graterol):** checking every claim against the data is what exposed TK CoachAI's failures. Had we accepted what was said without checking it, we would still have false figures. Checking is not slowness: it is the audit. In governance, no claim is accepted without its proof (statement IDs in the LRS, the code excerpt and the date from which it holds).
**Role-invariance principle (Ana Eslava-Graterol, 10 Nov):** no agent decides, and every agent keeps to its role, whatever the model, whatever it is called, and whatever temperature the system applies. Code and tests enforce the role (validated schema, ids from the base, common block, R-ID checks A1–A4, stability test), not the model's parameters. The exact model identifier is recorded to audit it, not to trust it.

> These norms govern every AI agent of the MLLDE model and its applications (e.g. TK CoachAI). An agent that is not on the map does not enter the loop.

## R-MED-1 — Main rule: every measurement goes through the measurement flow

> **MAIN RULE, binding on every AI agent:** the user's production is always checked by the measurement flow against the full base — **381 A1–C2 descriptors measurable from text** (the inventory has 382: gram 115 · voc 96 · spk 100 · med 71; one pronunciation descriptor, which cannot be measured from text, is excluded) — with `ext/input-channel` declared. **No other agent measures, scores or assesses the user on its own.**

- An agent that is not the measurement flow may extract, select, write or plan, but **never passes judgement on the user's level or competence** (N10: zero calculations in an LLM; G-NIVEL-1 P2: a `level`/`grade` field invalidates the whole response).
- The comparison **actual vs declared level** is computed by code with the public 80% rule (v0.7.2 thresholds); the Evaluator never receives the declared level (P1, anti-anchoring).
- The descriptors the user evidences with a verbatim quote select the content of the next Process phase (i+1 by code).
- Every write to the profile requires a human actor (G-NIVEL-1, P3–P5).
- Rule coined on 9 Nov by the author's decision; it comes into force with the signatures of pedagogy and engineering (N12).

## N — Structural norms (N1–N13, operational extract)

| Norm | Rule |
|---|---|
| **N1 — Closed registry** | Only the agents on the canonical map may act. A new agent = a proposal with a signed card, not an installation. |
| **N2 — Single gate** | Every write to the LRS goes through the Consolidator (code). No agent writes to the LRS on its own. |
| **N3 — Anti-rogue-agent** | The prompt in production must match the approved one (`prompt-hash`); if it differs, the agent does not start. |
| **N4 — Closed base** | A single knowledge bundle (registry v0.8.3 + inventory v0.7.2), mounted by code, with `kb-version` and `kb-hash` declared. No copyrighted material in the prompt. |
| **N5 — Fixed models** | Model with its version fixed in writing; no-train contract verified; **never any fallback** (Gemini lesson, 5–19 Oct). The exact model identifier goes in every statement (R-ID). **It applies to every agent, not only to the one that measures** (author's decision, 11 Nov), with tracking of the adherence rate per model. Legal basis: see the note under this table. |
| **N6 — Traceability** | The agent in `context.instructor`, with its `account` from the registry (R-ID, v1.7; formerly `agent-id`), + `agent-version` + `measure-model` (exact identifier) + `rules-version` in every statement. Goal: every registered agent with its own trace. The registry is in `governance/registro-agentes/`. |
| **N7 — Flows that never cross** | Measurement (1×/session), pedagogy (per turn), activity (loop). The band arises only from the measurement flow. |
| **N8 — Fail-closed** | When in doubt, nothing is emitted: ASR gate 0.70, judge unavailable → no tip, invalid schema → discard. |
| **N9 — PII** | Only the UUID + transcript go to the model; never name, company, job title or email. LRS authority = service account, never a personal credential. |
| **N10 — Zero calculations in an LLM** | No agent generates competence numbers: marks (5.2/5.3), band (formula of 26/08), i+1 and proposed level are computed by code. |
| **N11 — Declared incidents** | Each agent defines its incident types with an IRI from the registry; they go to its log, never to the learner's KPIs. |
| **N12 — Signed versioning** | A change of prompt/model/rules = version bump + signature (pedagogy + engineering) + entry on the map + the date from which it counts. |
| **N13 — Tests in CI** | Every admission test runs in CI on every deployment; if it fails, the deployment is blocked. |

**Legal basis of N5** (developed in the agent primer, §3.1). The AI Act citations were checked on 11 Nov against the official text in the Official Journal (Regulation (EU) 2024/1689, original version, without the changes of Regulation (EU) 2026/1744):
- **AI Act:**
  - art. 11 and Annex IV 2(a);
  - art. 25(4);
  - art. 53(1)(b) and Annex XII;
  - arts. 12, 15(1), 15(4) and 19;
  - substantial modification: arts. 3(23) and 43(4);
  - art. 86.

  High-risk obligations apply from 2 Dec 2027 (Regulation (EU) 2026/1744).
- **GDPR** (applies today):
  - arts. 5(1)(a), (b), (d) and (f), and art. 5(2);
  - arts. 13(1)(e)–(f);
  - art. 28(3);
  - art. 30(1)(d)–(e);
  - art. 32;
  - art. 35;
  - arts. 44–46.
- **ISO/IEC 42001:** A.6.2.8 and A.10.

> **What the UUID in N9 is (12 Nov).** UUID stands for *Universally Unique Identifier*. It is a code of 32 hexadecimal characters in five groups separated by hyphens, for example `7ba714b6-b6b5-4b7f-8cbd-1ca44b43145e`. It is generated so that the probability of a repeat is practically nil.
>
> **In TK CoachAI** it is the learner's pseudonymous identifier: it appears in the LRS as the actor's `account.name`, instead of their name. Only the UUID and the transcript go to the model: so the model knows which learner a session belongs to without knowing who they are (no name, company, job title or email).
>
> **The short pseudonym in the dashboards**, of the form `TK-7BA714B6`, is the first 8 characters of the UUID in capitals. Checked in the Veracity export of 11 Nov: 577 of 577 statements with a pseudonym.
>
> **A pseudonym is not anonymous:** whoever holds the table that links the UUID to the profile can identify the learner. That is why the UUID is still personal data and is protected as such.

> **Reminder of a prior agreement (N9 · personal data).** If the report has to show the learner's name, it is added by **the app when it presents the report, outside the AI**: the code takes the model's text and adds the name from the profile. So the name appears on screen or in the PDF **without ever passing through the model**. This is what data minimisation requires (GDPR, art. 5(1)(c)).

### N6-bis — Weekly cmi5 audit package (traceability rule, v1.7)

> **Rule:** every week, the environment delivers to the designer a **cmi5 package** of the version in production, downloadable without the developer's involvement. It is imported into **SCORM Cloud** and launched with a test learner; the xAPI statements it emits are compared with the current registry and profile.

- **What is checked:**
  - **a. Continuity of the loop:** Input → Process → Output → Adapt, step by step and in order.
  - **b. Undeclared metrics:** no extension, verb or result that is not in the registry.
  - **c. Duplicate metrics:** one session, one `completed`; no data emitted twice.
  - **d. Unauthorised actors and agents:** no actor or agent that is not on the canonical map. An unknown actor is an incident and is reviewed before going on.
- **Why cmi5 and not SCORM 2004:** cmi5 is based on xAPI, so it shows actors, verbs and objects. SCORM 2004 does not carry xAPI statements and does not allow this check.
- **What the package does not replace:** the package proves what the version **emits**. What **has happened** is audited with the 3 LRS exports (statements, verbs and objects, agents) and with the admin dashboard's JSON (measurement model). The two audits are cross-checked.
- **Record:** each package carries the date, the app version and the agents' `prompt-hash`; it is kept with the result of the check.
- Rule agreed at the meeting of 9 Nov; it comes into force with the signatures of pedagogy and engineering (N12).

### Equivalence with the numbering of the Evaluator v2 spec (§6.1)

> **Numbering notice.** The Evaluator v2 spec (8 Nov) numbers its norms differently from N4 onwards, and the Primer of the 7 (8 Nov) cites that spec numbering (e.g. "N9 = exact model"). So that the committee does not find two different "N9", this is the official correspondence:

| Evaluator v2 spec (§6.1) | Equivalent in this package (v1.1) |
|---|---|
| N1 · Closed registry | **N1** (same rule) |
| N2 · Single gate for model calls | **N2** (here with emphasis on writing to the LRS) |
| N3 · Anti-stray-agent test (includes prompt-hash) | **N3** (same rule) |
| N4 · Card before code (justified request + two signatures) | **R-ADM-1 and R-ADM-5** |
| N5 · One function per agent; no agent decides | Guiding principle + **N10** |
| N6 · Common block mandatory in every prompt | **Missing in v1.1 — to be added** (literal text in spec §6.2) |
| N7 · The base is inherited by code | **N4** |
| N8 · Traceability (actor = the agent that acts) | **N6** + **R-ID** (v1.7: the actor is the learner; the agent goes in `context.instructor`) |
| N9 · Approved, fixed models, no fallback | **N5** |
| N10 · Minimum data (no personal data) | **N9** |
| N11 · Changes = new version, with test and signatures | **N12** |
| N12 · Periodic audit (agents ↔ calls ↔ Veracity) | **Missing in v1.1 — to be added** |
| N13 · Withdrawal of agents without a card on time | **Missing in v1.1 — to be added** |
| N14 · Demonstrated need (8 Nov) | **R-ADM-1**, with the demonstrated-need condition |
| N12-bis · Weekly cmi5 audit package (9 Nov) | **N6-bis** (v1.7) |

> **On the "N14" cited by the Primer of the 7 (corrected in v1.7):** N14 **does exist**. The author added it to the Evaluator v2 spec on 8 Nov, with her decision that the loop needs only 7 agents: **N14 · Demonstrated need** — an agent is approved only if its card shows which part of the loop needs it and why neither code nor one of the 7 loop agents can do it. Its equivalent in this package is **R-ADM-1** (entry on the map with justification), reinforced with that condition. The v1.2 note that called it an orphan was written on an earlier version of the spec. It comes into force with the signatures of pedagogy and engineering (N12).

## G-NIVEL-1 — The level: the app proposes, it never generates the level

**Two user modes (Ana Eslava-Graterol, 11 Nov).** TK CoachAI was built for B2B and for B2C. The specifications always distinguish them:

| | **B2B** (business · `user-track: pilot`) | **B2C** (consumer · `user-track: free`) |
|---|---|---|
| Who is there | The learner and, behind them, a teacher who moderates | The learner alone, without a teacher |
| What the app does | It compares the learner's real evidence with the descriptors: how many are met and at which level, and it emits a band | The same |
| What enters the LRS | **`progressed`, with the learner as actor**: the user who interacts and produces the conversation is always the one who has progressed. It carries their mark and their evidence | The same |
| External validation (outside the app; it does not enter the LRS) | The teacher confirms the level with another assessment, oral and written | If the person wants the level validated, a teacher confirms it outside, with another assessment |
| Setting | Training with a responsible teacher | Outside official education settings |

- **RULE:** the app PROPOSES a measure with a public rule, against the criteria set in the app: the highest level with **≥80% of descriptors evidenced with a verbatim quote** (v0.7.2 thresholds: A1 48 · A2 52 · B1 63 · B2 58 · C1 48 · C2 40). **The AI does not decide:** it does not assess the evidence by its own judgement or by what seems right to it. It compares real data from different sources, the learner's evidence and the descriptors of the base: the AI locates the evidence and code counts and computes the band. **`progressed` is the learner's mark of progress in the app, not the certification of the level:** that is given, where appropriate, by an external validation.
- **P1:** no agent receives the learner's declared level (anti-anchoring).
- **P2:** no model returns levels or marks (a `level`/`grade` field invalidates the whole response).
- **P3:** the proposal is never written into the profile; it is shown as "pending decision".
- **P4 (Ana Eslava-Graterol, 11 Nov): actor of `progressed` = the learner, in B2B and in B2C.** The teacher's validation is external to the app: they confirm the level with another assessment (oral, written) and it does not enter the LRS. That is why the app never emits a `progressed` in the name of the teacher or of an agent. **What the app must guarantee:** that the evidence behind each `progressed` (answers, errors, quotes and descriptors) can be seen in the dashboards. *Replaces:* "every `progressed` requires a human actor + `evidenceReviewed: true`; otherwise the gate rejects it".
- **P5:** the profile does not change through performance without a human decision (R-DESAJUSTE-1: 3 mismatched sessions → "review" flag, profile intact).
- **P6 (Ana Eslava-Graterol, 11 Nov): the app's level test is disabled.** It changed the learner's level without leaving a statement and without a teacher, and the generators used that level.
- **Legal basis:** AI Act art. 14 + Annex III 3(b)/(c) · GDPR art. 22.
- **Own incidents:** `incident/nivel-sin-decision-humana` · `incident/nivel-propuesto-escrito-en-perfil` (high severity: they stop emission).

## Level decision in B2C: the free user, without a teacher (v1.5)

*B2C = free user (`user-track: free`): they have no teacher and are not part of official education settings (Ana, 11 Nov).* *Their `progressed` follows the general rule of G-NIVEL-1 P4: the actor is the learner.*

> **Rule:** for the free user, code proposes and **the user decides about their own profile after seeing the evidence**; in the highest-impact cases the decision requires a **human reviewer**.

- **Proposal with evidence:** the proposal (public 80% rule) is shown with the evidenced descriptors and their verbatim quote; the user accepts or not. If they ignore it, nothing changes (P3/P5 intact).
- **Trace of the free user's decision:** their acceptance does happen inside the app, so their `progressed` carries actor = the user's UUID + `evidenceReviewed: true` + the rule version.
- **Mandatory human review** in three cases: a jump of two levels or more (e.g. A2→B2), entry into level C, or a dispute by the user.
- **Never downwards without acceptance:** a proposal to go down is notified, not applied; if it is ignored, the profile stays and R-DESAJUSTE-1 flags "review".
- **No dark patterns:** accepting cannot be more attractive than declining; no pressure and no countdown.
- **Minors:** if the free channel admits minors, self-acceptance is not valid — it requires legal age or review by a responsible adult.
- Rule adopted from the analysis of 9 Nov (recommended hybrid option); it comes into force with the signatures of pedagogy and engineering (N12).

## T-NIVEL-1 — Automatic test on every deployment

- **a.** Model response with `{"level":"b2"}` → total rejection + incident; nothing is computed.
- **b.** `progressed` whose actor is not the learner (an agent, the app or the teacher) → rejected before the LRS (P4, 11 Nov).
- **c.** 3 simulated sessions with evidence of another level → profile intact + "review" + incident.

## R-ADM — Admission of a new agent (the 5 rules)

1. **R-ADM-1 · Map:** prior entry on the canonical map, with justification.
2. **R-ADM-2 · Fixed model:** a specific version, no fallback. Temperature is not an admission condition (role-invariance principle, 10 Nov): the agent demonstrates its stability with the repeated-input test. Until 10 Nov it read "temperature fixed".
3. **R-ADM-3 · Closed base:** only the official bundle; no copyright; nothing "from the model".
4. **R-ADM-4 · Prompt with hash (N3):** production == approved, or it does not start.
5. **R-ADM-5 · Signature:** card signed by pedagogy and engineering before deployment.

## Classification of components (agent vs infrastructure)

- Is it deterministic (same input → same output)? → **infrastructure**, not an agent (ASR, OCR, SRS scheduler). It is governed with a confidence gate, a no-train contract and without storing the raw input.
- Is it generative and does it fit in a canonical piece? → **it is absorbed** (the 4 generators → piece 5; the Hint → piece 1).
- Does it fit in none? → **full R-ADM examination or withdrawal**.

## R-ID — Identification of agents in the record (v1.7)

**Basis (xAPI 1.0.3 standard published by ADL, xAPI-Data):**
- §2.4.6, context property `instructor`: "Agent (MAY be a Group). Instructor that the Statement relates to, if not included as the Actor of the Statement."
- §2.4.2.1: "An Agent MUST be identified by one (1) of the four types of Inverse Functional Identifiers".
- §2.4.2.4: the `account` object requires `homePage` (IRL of the system) and `name` (unique identifier in that system).

**Actor rule (author's decision, 10 Nov; replaces decision 53):**
- **The actor of every learning statement is the learner.** It applies to `completed`, `answered`, `attempted`, `mediated` and `adapted`.
- **The AI agent that intervenes goes in `context.instructor`**, with its `account`. If two intervene at once (e.g. the Corrector and the Judge), a **Group** with both goes there.
- **Voids (`voided`) have the system account as actor**, `tk-coach-engine`. It is a system act, not an act of an AI agent.
- **The `authority` is set by the LRS** from the service key. The app does not write it (N9).
- **Design basis:** the AI does not grade. The Evaluator provides evidence, code computes (N10) and the teacher validates the level outside the app (G-NIVEL-1). That is why the achievement belongs to the learner and the agent is recorded as the one who intervened.

**What receives an agent identifier (link with the classification of components):**
- **Every generative component that acts in learning or talks to the user.** Each function has an identifier.
- **Teo, the support agent, is declared in the registry** (`support-agent`, author's decision, 10 Nov). It is outside learning, but it talks to the user (art. 50). **It never appears in a learning statement** (if it does, A2 fires); its trace is the call log.
- **They never receive an agent identifier or appear in `instructor`:**
  - infrastructure (ASR, OCR, SRS scheduler);
  - code (consolidator, guardian, rate limit).

**Exact form of identifiers** (equivalent to the IRI rule of 24 Sep: "0 ADL verbs in https://", "0 MLLDE verbs in http://", which still holds):
1. A single identifier, `account`; never `mbox` or `openid`.
2. Exact `homePage`: `https://tkcoach.talketika.app`. With "s", lowercase, no trailing slash and no path.
3. Exact `account.name`, as in the identifier registry: lowercase, with hyphens and ending in `-agent`. The only exception is the system account, `tk-coach-engine`.
4. The `name` label (e.g. "Capi") does not identify; checks always filter by `account.name`.
5. The version never goes in the name (no `capi-agent-v2`): it goes in `ext/agent-version`.
6. An identifier is never renamed or reused; that of a withdrawn agent is not assigned to another.
7. The `authority` is not written by the app: the LRS sets it (`https://tk-coach-prod.lrs.io/keys/<key>`).

**Detection of out-of-role behaviour** (in the daily check and in the audit with the LRS export):
- **A1:** an `instructor` that is not in the registry indicates an unauthorised agent.
- **A2:** an agent in a verb or flow that is not its own indicates out-of-role behaviour. For example, any agent other than the Evaluator in a `completed`.
- **A3:** an agent as actor of a learning statement.
- **A4:** a logged call (N8 of the spec) without a statement or without `instructor`.

**Closure:**
- 0 agent accounts with another `homePage`;
- 0 `account.name` outside the registry;
- 0 agents as actor of a learning statement;
- 0 new statements with a personal `authority`.

**Baseline (Veracity export, 10 Nov, 2,243 statements):**
- `account` as the only identifier: 2,243 of 2,243;
- a single `homePage`, the correct one: 2,243 of 2,243;
- 0 statements with `context.instructor`;
- `capi-agent` as actor in 141 `adapted`;
- `tk-coach-engine` in 36 `voided`;
- `authority` = the personal key of a team member, not the service key, in 2,243 of 2,243.

**Proof of compliance** (verification principle):
- the ID of a new statement with `instructor`;
- the code excerpt;
- the date from which it holds.

It comes into force with the signatures of pedagogy and engineering (N12).

## Vocabulary from images or prompts — two tracks by user type (v1.3)

- **Institutional learner (pilot) — Track A (default):** the component may only SELECT terms that already exist in the inventory (`en.voc.*`); validation against an allow-list in code; what is not there is discarded. The content is set by the programme, so that measurement is comparable.
- **Institutional learner — Track B (new vocabulary):** the component PROPOSES candidates to a human review queue; they enter the inventory in the next version bump, with the date from which they count. The component never writes to the base.
- **Free user — own track (the user's own selection):** the input is generated by the user (their image, their presentation). Their vocabulary cards are selected by **the user** from the terms extracted from their material; code validates the format and requires the origin (`own-image`), without going through the inventory queue. **CLIL justification:** language is learnt through content that is meaningful to the learner; their context and real communicative need decide which vocabulary is worked on.
- **Forbidden in both tracks:** AI-generated vocabulary feeding cards or drills without validation in code and a declared origin.
- In both cases, content vocabulary is **practice without measurement** (decision 51): objective mastery by SRS, never a band.

## Scope of the OCR reader and measurement in every interaction (v1.3)

- The OCR reader decides **about the image, never about the learner**: it extracts text and terms from the stimulus; it does not assess.
- **Every interaction** checks the user's production against the full base — 381 A1–C2 descriptors measurable from text (inventory of 382; one pronunciation descriptor excluded) — with `ext/input-channel` declared.
- The **actual vs declared level** is computed by code (public 80% rule, v0.7.2 thresholds); the Evaluator never receives the declared level (P1, anti-anchoring). The descriptors the user evidences with a verbatim quote select the content of the next Process phase (i+1 by code).
- `progressed` always has the learner as actor, and certification of the level is a validation external to the app (G-NIVEL-1); **for the free user, the rule in the section "Level decision in B2C" (v1.5) applies.** (Until 11 Nov this line said, by mistake, that it was still to be defined.) OCR is infrastructure: it is recorded with `ext/input-channel: ocr` and never goes in `context.instructor` (R-ID).

## Proposal to mint IRIs — registry bump v0.8.4 (v1.6)

Analysis of the published registry v0.8.3 (153 concepts) against these norms. **No new verbs are needed:** the reused ADL verbs (`progressed`, `attempted`, `completed`, `passed`, `failed`, `interacted`, `asked`, `answered`) and the 3 coined ones (`pronounced`, `mediated`, `adapted`) cover every proposal — the free user's acceptance (v1.5) is a `progressed` with its own actor, not a new verb.

**Urgent — the norms already cite them and they do not exist in the registry:**

| Proposed IRI | Type | Reason |
|---|---|---|
| `incident/nivel-sin-decision-humana` | incident | G-NIVEL-1 names it; the incident table does not have it |
| `incident/nivel-propuesto-escrito-en-perfil` | incident | Same — today they are orphan references |

**High — they close audit findings:**

| Proposed IRI | Type | Reason |
|---|---|---|
| `ext/descriptor-results` | result | Output per descriptor `{id, evidenced, quote}`; without it there is no visible evidence for v1.5 self-acceptance (planned in v0.9) |
| `ext/vocabulary-origin` | context | Closed values: `inventory · correction · prompt · image · summary · own-image`; it is the field that arrived "undefined" in 16 terms |
| `ext/user-track` | context | `pilot · free`; it makes the two tracks and the decision by group auditable |

**Medium — they make R-MED-1 and N6 machine-checkable:**

| Proposed IRI | Type | Reason |
|---|---|---|
| `ext/flow` | context | `measurement · pedagogy · activity`; today N7 is a written rule, not data in the LRS |
| `ext/agent-version` · `ext/rules-version` · `ext/prompt-hash` · `ext/kb-version` | context | N6/N3/N4 require them in every statement and only `ext/measure-model` exists |
| `ext/ocr-confidence` | result | Analogous to `ext/asr-confidence` for the OCR gate |

**New fields inside `ext/level-decision` (bump of the object, not a new IRI):** `decisionActor` (self · reviewer; `teacher` removed on 11 Nov: the teacher's decision does not enter the LRS, P4) · `evidenceReviewed` (boolean, P4) · `status` (proposed · accepted · rejected · pending) · `reviewTrigger` (none · jump2plus · c-entry · dispute).

**What is NOT minted:** downgrades without acceptance, dark patterns and minors are rules of code, UX and onboarding; they are audited in T-NIVEL-1 and in design review, not in the LRS. The IRIs work as identifiers even while `w3id.org/mllde` is still in a PR; the namespace should be resolved before publishing v0.8.4. Proposal from the analysis of 9 Nov; it comes into force with the signatures of pedagogy and engineering (N12).

## The guardian (specific rule)

No agent may **analyse and correct the system on its own**. A watcher only alerts (fail-closed, without write access). Its function is covered by the N3 test + CI: auditable, repeatable and without privileges.

---

*MLLDE method © 2026 Ana Eslava-Graterol (UPV). Prepared with AI assistance and reviewed by the author, in the spirit of art. 50 of Regulation (EU) 2024/1689.*
