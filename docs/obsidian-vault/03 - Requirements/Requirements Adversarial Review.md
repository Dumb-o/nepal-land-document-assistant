# Requirements Adversarial Review

> **Status:** Working draft — NOT READY TO BASELINE
> **Scope:** Land-Rent Document Preparation Module (MVP)
> **Date:** 2026-08-13
> **Method:** Adversarial review. This document attempts to **prove the requirements are insufficient** — it does **not** fix, rewrite, add, delete, or renumber any requirement in any other artifact. Recommended resolutions below are limited to **decide / clarify** actions for the project owner and domain experts.
> **Constraint honored:** No requirement file was modified to produce this review. This is the only file created.

---

## 1. Purpose

The purpose of this review is to attack the Land-Rent MVP requirement set before it is baselined, on the assumption that the requirements are **insufficient as written** and that any claims of readiness are false until proven otherwise.

Specifically, this review:

- Treats every `[PROPOSED]`, `[TO BE VALIDATED]`, `[OPEN QUESTION]`, and `[UNRESOLVED]` marker as a **defect of undetermined severity** rather than a harmless note.
- Probes the requirement set from the outside: what can an operator actually do? What can the system actually output? Where does the workflow silently produce a wrong, incomplete, or legally defective document?
- Checks internal consistency across the six artifacts that claim to describe the same system (SRS, Functional Requirements, Data Needs, Business Rules, Use Cases, Template Analysis).
- Grades every finding by the probability and the impact of failure in the real domain (a Nepali land-rent agreement that must be signed, witnessed, and possibly registered).

The deliverable is a verdict — **READY TO BASELINE** or **NOT READY TO BASELINE** — plus a resolution order. Nothing in this document is an instruction to implement anything.

---

## 2. Documents Reviewed

| # | Document | Location | Size |
|---|---|---|---|
| 1 | Software Requirements Specification (v0.1.1) | `docs/obsidian-vault/03 - Requirements/SRS/SRS.md` | 2,066 lines |
| 2 | Functional Requirements | `docs/obsidian-vault/03 - Requirements/Functional Requirements/Functional Requirements.md` | 1,899 lines |
| 3 | Data Needs | `docs/obsidian-vault/03 - Requirements/Data Needs.md` | 2,354 lines |
| 4 | Non-Functional Requirements | `docs/obsidian-vault/03 - Requirements/Non-Functional Requirements/Non-Functional Requirements.md` | 693 lines |
| 5 | Business Rules | `docs/obsidian-vault/03 - Requirements/Business Rules/Business Rules.md` | 195 lines |
| 6 | Use Cases | `docs/obsidian-vault/03 - Requirements/Use Cases.md` | 347 lines |
| 7 | Case Client Document Traceability | `docs/obsidian-vault/03 - Requirements/Traceability/Case Client Document Traceability.md` | — |
| 8 | Land Rent Template Analysis | `docs/obsidian-vault/02 - Document Analysis/Land Rent Template Analysis.md` | 757 lines |
| 9 | Decision Log | `docs/obsidian-vault/00 - Project Control/Decision Log.md` | — |
| 10 | Open Questions | `docs/obsidian-vault/00 - Project Control/Open Questions.md` | — |
| 11 | Project Glossary | `docs/obsidian-vault/00 - Project Control/Project Glossary.md` | — |
| 12 | Project Overview | `docs/obsidian-vault/00 - Project Control/Project Overview.md` | — |
| 13 | Project Roadmap | `docs/obsidian-vault/00 - Project Control/Project Roadmap.md` | — |
| 14 | Reference template (evidence base) | `private/Reference Documents/Land Rent - WIP.pdf` | 7 instances |

**Evidence-base note:** the template analysis rests on **one PDF containing 7 instances** (6 complete, 1 partially blank). For a system whose only output is a legally consequential document, this is a thin sample (see AR-OBS-04).

---

## 3. Review Method

The review applied a fixed probe set to every artifact, cross-checking each chain `Template field → Data Need → FR-LR → Use Case → Business Rule → SRS` in both directions.

**Probes applied:**

1. **Capability assessment** — for each FR-LR in `Functional Requirements.md` §6, is it traceable to a Data Need, a Use Case, and template evidence? Is it testable as written?
2. **Client/Party scenarios A–I** (§10) — the operator's most common situations, derived from Data Needs §2.2/§2.3/§2.7 and OQ-DN-17.
3. **Information acquisition paths A–J** (§11) — every way a value can enter the system, from Data Needs §2.7 and BR-048..052.
4. **Failure probes** — OCR failure (§12), manual Nepali entry (§13), missing data (§14).
5. **Model probes** — clause/variable model (§15), template traceability (§16), land-rent scenario coverage (§17), lifecycle (§18), persistence (§19), security/privacy (§20).
6. **Structural probes** — traceability gaps (§21), contradictions (§22), duplications (§23), over-engineering (§24), under-specification (§25).
7. **Readiness probes** — open questions revealed (§26), requirements that appear sound (§27), resolution order (§28), baseline readiness (§29).

**Finding format:**

```
### AR-XXX — [Short Finding Name]
- **Severity:** CRITICAL | HIGH | MEDIUM | LOW | OBSERVATION
- **Category:** [Scope | Data | Generation | Lifecycle | Legal/Domain | Security/Privacy | Traceability | Quality | Scenario]
- **Evidence:** [exact citations]
- **Problem:** [what is actually wrong]
- **Failure Scenario:** [one concrete story of the wrong outcome]
- **Impact:** [consequence]
- **Current Status:** Open
- **Recommended Resolution:** [decide / clarify only]
```

**Severity semantics used:**

| Severity | Meaning |
|---|---|
| **CRITICAL** | The MVP cannot function as specified, or the artifacts contradict each other on a core workflow, or the system is permitted to produce a legally defective document. Blocks baselining unless the owner explicitly accepts the risk. |
| **HIGH** | A major workflow, data, or document behavior is undefined or inconsistent and will force rework; resolvable only by a decision. |
| **MEDIUM** | A behavior is underspecified; resolvable by clarification without redesign. |
| **LOW** | Minor ambiguity, duplication, or weak sourcing. |
| **OBSERVATION** | Not necessarily a defect; noted for context or for the owner's information. |

**Method note:** the artifacts are unusually honest about their own gaps (dozens of explicit `[TO BE VALIDATED]` / `[OPEN QUESTION]` / `[UNRESOLVED]` markers). This review does not count those markers as "covered" — it treats each one as an open risk that must be resolved or explicitly accepted before baseline.

---

## 4. Executive Summary

**Verdict: NOT READY TO BASELINE.**

The requirement set is exceptionally well-structured, internally traceable, and disciplined about marking its own uncertainties. It is **not**, however, complete or internally consistent enough to build from. The review found **45 findings: 5 CRITICAL, 13 HIGH, 12 MEDIUM, 9 LOW, 6 OBSERVATIONS**.

The five CRITICAL findings are not obscure corner cases. They are the system's **core decisions**:

1. **The MVP boundary is contradictory** — SRS lists source-document capture/upload as MVP (`Must`), while Functional Requirements and Use Cases defer it entirely (AR-001).
2. **The system is permitted to finalize legally blank documents** — the rule for finalizing documents with blank mandatory identity fields is explicitly `[TO BE VALIDATED]` and no fallback decision exists (AR-002).
3. **Generation behavior for an absent party is self-contradictory** — one section allows a blank Second Party where the template permits it, another blocks generation entirely (AR-003).
4. **The financial engine is unvalidated** — rent/escalation formulas on which every financial clause depends are all `[TO BE VALIDATED]` (AR-004).
5. **Figures/words integrity is ungoverned** — the number-to-Nepali-words pairing that carries legal weight can be silently desynchronized by a permitted draft edit (AR-005).

None of these is a "writing quality" issue. Each is a **decision** that has not been made. The artifacts are structurally ready; the decisions are not.

**What is strong (and should be preserved):** the manual-entry-first acquisition model (BR-048..051), the Candidate → Verified two-layer data model, the data-state model with explicit `UNKNOWN`/`N/A`, the missing-variable detection (Data Needs §6.3), the human-finalization gating (BR-038/047, FR-LR-045), and the honest `[TO BE VALIDATED]` marking discipline. Section 27 lists these.

**Bottom line for the owner:** resolving the 5 CRITICAL and the 13 HIGH findings requires domain-expert and legal-expert answers, not more writing. Until those answers exist, baselining would freeze decisions that are currently marked unresolved.

---

## 5. Critical Findings

### AR-001 — MVP boundary is contradictory: source-document capture is both MVP and deferred
- **Severity:** CRITICAL
- **Category:** Scope
- **Evidence:**
  - `SRS.md` §6.1 MVP Scope: "Source document capture via camera or file upload" is listed as MVP.
  - `SRS.md` §7.3 FR-009 (Priority Must) "capture images of source documents using a device camera"; FR-010 (Must) upload existing digital images/PDFs; FR-012a; `SRS.md` §3.4 "The system's ability to capture, upload, and manage source documents is a core proposed capability."
  - `Functional Requirements.md` §7: FR-LR-101..104 (capture/upload) are explicitly **DEFERRED** and "**not MVP requirements**"; `Use Cases.md` UC-004 references only the deferred FR-LR-101..104.
  - `Functional Requirements.md` §8 "Conflicting Requirements": records the conflict ("this document defers capture/upload out of the MVP; the SRS v0.1 treatment must be reconciled") — but reconciles nothing.
- **Problem:** Two artifacts that must be synchronized describe different MVPs. An implementer cannot tell whether the MVP includes camera capture, file upload, capture review, or source-document viewing.
- **Failure Scenario:** The team builds capture per SRS (scope creep, camera + storage + recapture UI), or builds without it per FR (SRS non-compliance and a disappointed operator who expected to photograph documents). Either way one artifact is wrong at baseline.
- **Impact:** Contradictory scope; UI, storage, and interface design fork; schedule risk.
- **Current Status:** Open
- **Recommended Resolution:** Project owner decides the MVP boundary explicitly: (a) capture/upload deferred (manual entry is the acquisition mechanism — consistent with the task's core workflow), and (b) `SRS.md` §6.1, §7.3, §3.4, §15.1 updated to match, or (c) the inverse. One decision, applied to all four SRS locations.

### AR-002 — The system may finalize a document with blank mandatory identity fields; the rule is explicitly undecided
- **Severity:** CRITICAL
- **Category:** Data / Legal-Domain
- **Evidence:**
  - `Data Needs.md` §5.2, row `UNKNOWN`: "Blank placeholder if template permits (e.g., age) — **[TO BE VALIDATED] for mandatory fields**."
  - `Data Needs.md` §7.2 scenarios 4/8/12/16: "Permitted with placeholders… mandatory blanks [TO BE VALIDATED]."
  - `Functional Requirements.md` §7.1 marks citizenship fields (P1_CITIZENSHIP_NUM, P1_CITIZENSHIP_DATE, P1_CITIZENSHIP_DIST) **Optional / PROPOSED**, while `SRS.md` §9.4 lists citizenship as party information — the mandatory/optional authority is ambiguous.
  - FR-LR-045 blocks finalization only of "incomplete or unreviewed" documents; "complete" is never defined against the `UNKNOWN`/blank state.
  - Template evidence: age appears blank as `वर्ष __` in real instances.
- **Problem:** There is no decision rule for whether an operator may finalize a document containing blank legal identity fields (age, citizenship, possibly an entire Second Party). Current wording *permits* it; no requirement forbids it; no requirement defines the alternate path (unresolve-and-hold).
- **Failure Scenario:** Operator marks tenant age `UNKNOWN` → finalizes → document contains `वर्ष __`. Tenant later disputes the agreement; the identity data is absent where the agreement presumes it.
- **Impact:** Direct legal-validity risk on the system's only output; a finalized record that is not a complete agreement.
- **Current Status:** Open
- **Recommended Resolution:** Domain decision per field: which fields are mandatory vs optional for **finalization** (not just for the form), and what the system does when a mandatory field is `UNKNOWN` (block, or produce a visibly marked partial document that cannot be confused with a complete one). Define "document completeness" for FR-LR-045.

### AR-003 — Generation for an absent Second Party is self-contradictory
- **Severity:** CRITICAL
- **Category:** Generation / Scenario
- **Evidence:**
  - `Data Needs.md` §6.3: "If a variable is optional-blank (DN-VAR-02), generation proceeds with a blank placeholder where the template permits it (observed: … **whole Second Party in the blank WIP template**)."
  - `Data Needs.md` §7.2 scenario 5 (M2, First Party present / Second Party absent): "**Blocked (Second Party identity missing)**."
  - `Data Needs.md` §7.2 scenario 8: "Partial draft possible; Second Party still blocks."
  - `Functional Requirements.md` FR-LR-030 (Must) "Prevent Generation with Incomplete Data"; `Business Rules.md` BR-017 "generation must be blocked if mandatory template fields are missing."
- **Problem:** The same artifact asserts both "generation proceeds with a blank Second Party where the template permits" and "generation is blocked when the Second Party's identity is missing." No rule defines when a partial draft is permitted, what it contains, or how it is marked.
- **Failure Scenario:** An implementer follows §6.3 and generates a draft with an empty tenant block; another follows FR-LR-030 and refuses. The observed WIP workflow (blank tenant template) can be produced by one reading but not the other.
- **Impact:** The generation engine's behavior is unspecified at its most common real-world decision point (tenant not yet identified when drafting starts).
- **Current Status:** Open
- **Recommended Resolution:** Define the partial-draft rule explicitly: partial drafts are permitted only for `DN-VAR-02` optional-blank variables, marked visually and in metadata as draft/incomplete, and finalization of a document with a blank mandatory party block is forbidden.

### AR-004 — The financial engine is unvalidated; every generated financial clause depends on formulas marked `[TO BE VALIDATED]`
- **Severity:** CRITICAL
- **Category:** Generation / Legal-Domain
- **Evidence:**
  - `Business Rules.md` BR-024 (annual = monthly × 12), BR-025 (escalation = current rent × rate), BR-026 (compound `चक्रवृद्धि`) — all `[TO BE VALIDATED]`.
  - `Functional Requirements.md` FR-LR-027 — `TO BE VALIDATED`.
  - `Data Needs.md` §6.1, clause C02: "Rent figures + words, period, escalation rate/period/method" — "method [TO BE VALIDATED]".
  - `Land Rent Template Analysis.md` §7.2: calculations are "apparent calculation patterns," formulas inferred.
- **Problem:** The generator's only mathematical behavior — the rent and escalation figures that appear verbatim in every agreement's Clause 2 — is built from inferred formulas. Compound-vs-simple, period alignment (every year vs after N years), rounding, and Devanagari numeral output are all unspecified.
- **Failure Scenario:** Annual rent is computed as monthly × 12, but the observed annual instances use a different basis; every annual-rent document is financially wrong.
- **Impact:** Systematic financial errors in the system's sole deliverable; worst-case a dispute over rent amount.
- **Current Status:** Open
- **Recommended Resolution:** Validate BR-024..026 against all complete template instances and a domain expert before implementation; record the validated formulas (and any exceptions) as CONFIRMED rules, not inferred ones.

### AR-005 — Figures/words integrity is ungoverned after draft edits
- **Severity:** CRITICAL
- **Category:** Generation / Data
- **Evidence:**
  - `Data Needs.md` DN-RENT-02: rent amount in words — `CALCULATED`, required (C02).
  - `Business Rules.md` BR-022 (words auto-generated from figures) and BR-023 `[TO BE VALIDATED]`: "In legal usage, amount in words **overrides** the figure amount; the system must therefore keep the words value verified and in agreement with the figures."
  - `Functional Requirements.md` FR-LR-033: operator may make "permitted text-level edits" to the draft (scope `TO BE VALIDATED`).
  - No requirement states that a figure edit re-triggers word generation, or that the words field is protected from text edits.
- **Problem:** A permitted text-level edit can silently desynchronize figures and words — the exact pairing that carries legal weight (BR-023).
- **Failure Scenario:** Operator edits `रु ६५,०००` to `रु ७०,०००` in the draft, but the अक्षेरुपिय line still reads "पैसाठी हजार रुपैया". Under BR-023's own rule, the words override the figures → the document now states two different rents.
- **Impact:** Financially contradictory legal document; exactly the failure BR-023 warns about.
- **Current Status:** Open
- **Recommended Resolution:** Decide the draft-edit model: `CALCULATED` fields (RENT_AMOUNT_WORDS) are non-editable and re-derived on figure change, or any figure edit forces re-verification of the words by the operator before finalization.

---

## 6. High-Severity Findings

### AR-006 — Retention / archival / backup / deletion policy is undefined for every artifact class
- **Severity:** HIGH
- **Category:** Lifecycle / Security-Privacy
- **Evidence:** `Business Rules.md` BR-040; `SRS.md` §10.5, §10.3 (source docs), §10.4 (drafts), §10.10; NFR-BAC-001/002; NFR-PRI-002; `Data Needs.md` OQ-DN-10, DN-LIFE-01..06; `Business Rules.md` OQ-BR-06.
- **Problem:** "Retain indefinitely" (Decision 004) plus "deletion policy `[TO BE VALIDATED]`" plus NFR-PRI-002 "avoid unnecessary retention" form an unresolved tension. There is no deletion workflow (who may delete, what may be deleted, whether finalized documents are ever deleted), no archival criteria, and no backup mechanism (SRS §15.5 storage is `[TO BE DETERMINED]`).
- **Failure Scenario:** Five years of finalized cases + source images + candidate data accumulate with no deletion rule; a client exercises a deletion request and the system has no defined answer; PII exposure grows without bound.
- **Impact:** Unbounded PII retention; privacy/compliance exposure; backup design ungrounded.
- **Current Status:** Open
- **Recommended Resolution:** Owner + legal decision per artifact class (source docs, candidate data, verified data, drafts, finalized documents): retention period, archival criteria, deletion authority and conditions, backup mechanism and RPO/RTO intent.

### AR-007 — Signature / execution method for the finalized document is undefined
- **Severity:** HIGH
- **Category:** Lifecycle / Legal-Domain
- **Evidence:** Template S04/S05 signature areas with `P1_SIGNATURE_NAME`/`P2_SIGNATURE_NAME`; `Land Rent Template Analysis.md` §17.2 Major Unknown #6 "whether digital signatures or only physical signatures are used"; no FR for printing or e-signing; `SRS.md` §10.5 finalization flow ends at "Finalized System Record."
- **Problem:** The document lifecycle has no defined execution step. A "finalized" PDF that must be signed by both parties, witnesses, and possibly the writer has no defined path back into the system.
- **Failure Scenario:** System finalizes a PDF; the operator prints it, parties sign on paper, and the executed original is filed physically — but the Finalized System Record has no link to the executed copy, so retrieval and audit see only the unsigned generator output.
- **Impact:** Finalized-record ↔ executed-document gap; audit/retrieval of the true agreement undefined.
- **Current Status:** Open
- **Recommended Resolution:** Decide the execution model (print-and-sign, electronic signature, or both) and how the executed copy is associated with and retained against the Finalized System Record.

### AR-008 — Output format and printability are unconfirmed
- **Severity:** HIGH
- **Category:** Generation
- **Evidence:** `Functional Requirements.md` FR-LR-031 (Must, PROPOSED) "Generate Output in Printable Format" — "Output format (PDF proposed) is not confirmed"; FR §8 lists FR-LR-031 as unsourced; no print/layout/A4/pagination/font-embedding requirements.
- **Problem:** The deliverable must be printable, physically signable, and possibly notarized. Without a confirmed format and a rendering contract for Devanagari text, the output cannot be trusted in the real workflow.
- **Failure Scenario:** Generated PDF renders fine on a tablet but prints with broken Devanagari conjuncts or wrong page breaks; the notary rejects it.
- **Impact:** Unusable output; loss of trust in the core value proposition (RSK-004).
- **Current Status:** Open
- **Recommended Resolution:** Confirm output format and add print/layout/font-embedding requirements; validate against a printed sample.

### AR-009 — The use-purpose enumeration driving all conditional clauses is incomplete
- **Severity:** HIGH
- **Category:** Generation / Legal-Domain
- **Evidence:** `Data Needs.md` OQ-DN-05 ("complete list of use purposes"), §7.3 #1 "full list [TO BE VALIDATED]"; `Business Rules.md` BR-027/028 `[TO BE VALIDATED]`; FR-LR-025 "exact set of conditional sections and their triggers is not fully confirmed"; `Data Needs.md` §2.6 conditional pattern driven by `DN-PROP-06`.
- **Problem:** The conditional-content engine (clauses C03, C04, C11, C12 and the mixed `business+residence` case) is switched by a value list that is not final. An unlisted purpose would silently drop legal clauses.
- **Failure Scenario:** A post-baseline case uses a purpose such as industrial use; the generator renders the agriculture/business clause sets — none of which fits — and omits the required clause.
- **Impact:** Wrong or missing legal clauses in the deliverable.
- **Current Status:** Open
- **Recommended Resolution:** Validate the complete use-purpose list with domain experts; define behavior for unlisted/mixed purposes; confirm clause membership per purpose (OQ-BR-01).

### AR-010 — Client-information updates after finalization are ungoverned
- **Severity:** HIGH
- **Category:** Lifecycle / Data
- **Evidence:** `Data Needs.md` OQ-DN-09; `Use Cases.md` OQ-UC-09; `Business Rules.md` OQ-BR-08; FR-LR-055..061; BR-044 (Client reuse).
- **Problem:** A finalized case references Client data (FR-LR-058/059 pre-fill). Whether the Client record may be edited afterward, and what that does to the finalized case's integrity, is undefined: silent mutation, immutable snapshot, or flagged revision.
- **Failure Scenario:** An operator fixes a typo in a Client's citizenship number; a previously finalized agreement that cited the old number now silently shows the new one, or search returns mismatched data.
- **Impact:** Finalized-record integrity and auditability.
- **Current Status:** Open
- **Recommended Resolution:** Decide the Client versioning model (immutable snapshot per case vs flagged revision) and the visibility of changes to finalized cases.

### AR-011 — Source-document association level (Client vs Case vs both) is unresolved
- **Severity:** HIGH
- **Category:** Data / Scope
- **Evidence:** `Data Needs.md` OQ-DN-08 (explicitly `[OPEN QUESTION]`), DN-SRC-04/06; `Business Rules.md` BR-046; `Use Cases.md` OQ-UC-08; `SRS.md` §9.6; FR-LR-061.
- **Problem:** Every source-document requirement (storage, retrieval, deduplication, client reuse) forks on this decision. The data model, storage schema, and UI cannot be finalized without it.
- **Failure Scenario:** Implementation stores source documents at case level; an operator later needs a Client's citizenship across all cases and must re-upload or re-enter it.
- **Impact:** Data-model and storage redesign risk; duplicate storage.
- **Current Status:** Open
- **Recommended Resolution:** Owner decision (recommendation: case-level association with an optional reference link to the Client record, matching the observed single-case workflow).

### AR-012 — Case lifecycle end-state contradicts across artifacts
- **Severity:** HIGH
- **Category:** Lifecycle / Scenario
- **Evidence:** `SRS.md` FR-007 lifecycle includes "**Archived/Closed**"; `Data Needs.md` §5.3 minimum set is `Created → In Progress → Draft Generated → Under Review → Finalized (→ Persistent)` and explicitly demotes the SRS's finer states ("Data Collection", "Verification", "Archived/Closed") to `[PROPOSED]`; `SRS.md` §10.5 archival is `[OPEN QUESTION]`.
- **Problem:** Two artifacts describe different state machines, and they disagree on whether a post-finalization "Archived/Closed" state exists. Status semantics (DN-CASE-02) drive every filter (Recent Cases, directory, search).
- **Failure Scenario:** A status filter written against Data Needs shows all finalized cases as current; one written against SRS hides "archived" cases from the operator.
- **Impact:** Inconsistent case lists and retrieval behavior.
- **Current Status:** Open
- **Recommended Resolution:** Establish one authoritative state machine with a transition map; record it in one place (recommended: Data Needs §5.3) and make the SRS reference it.

### AR-013 — Notice-period unit model is ambiguous
- **Severity:** HIGH
- **Category:** Data / Generation
- **Evidence:** FR-LR-014 flagged "notice period units vary… does not resolve the unit model"; `Data Needs.md` DN-RENT-09 (single field); clause C08; `Land Rent Template Analysis.md` §8.3 (30 days / 60 days / 3 months / 6 months; one instance asymmetric per party).
- **Problem:** No unit field is defined, so "3" is ambiguous (days vs months). The observed per-party asymmetric notice is also unmodeled by a single `NOTICE_PERIOD` field.
- **Failure Scenario:** Operator enters "3" intending months; the clause renders "3 days"; termination notice is legally inadequate.
- **Impact:** Wrong termination clause; potential invalidity.
- **Current Status:** Open
- **Recommended Resolution:** Define notice period as value + unit, with separate fields per party if asymmetric notices are supported.

### AR-014 — Template version changes mid-case are ungoverned
- **Severity:** HIGH
- **Category:** Generation / Lifecycle
- **Evidence:** `SRS.md` §7.9 (template-version association); FR-LR-029/043; DN-DOC-05 / DN-GEN-04; no freeze or migration rule for in-flight cases when a template version changes.
- **Problem:** If the template is updated (e.g., a clause changes) while a case is mid-draft, nothing specifies whether the draft regenerates against the new version, keeps the old, or warns the operator.
- **Failure Scenario:** A clause changes in template v2; a case generated under v1 is finalized days later and silently contains the superseded clause.
- **Impact:** Mixed-version documents; wrong clause content.
- **Current Status:** Open
- **Recommended Resolution:** Decide freeze-on-generation vs explicit migration, and whether the operator must be notified of template changes affecting an in-progress case.

### AR-015 — Offline behavior and deployment/storage architecture are undefined
- **Severity:** HIGH
- **Category:** Security-Privacy / Scope
- **Evidence:** `SRS.md` AS-003 (tablet/smartphone), AS-005 "reliable internet connectivity" `[ASSUMPTION]`; §15.5 storage "local device, cloud, server `[TO BE DETERMINED]`"; NFR-REL-001 availability "appropriate to the deployment model" (model unspecified); NFR-BAC backup mechanism unspecified.
- **Problem:** The primary-device assumption is a mobile tablet, yet the connectivity assumption is "reliable internet" and the storage/deployment model is undecided. If capture is ever restored (AR-001) this matters; even without it, data residency, backup, and availability all depend on the deployment choice.
- **Failure Scenario:** An operator in a district office with intermittent connectivity loses entry work; or the only copy of case data lives on a device that fails (RSK-005).
- **Impact:** Data loss; unusable workflow in the field.
- **Current Status:** Open
- **Recommended Resolution:** Decide deployment model (local/cloud/server), connectivity expectation, and whether offline/queued entry is required; then make NFR-REL-001/NFR-BAC-001 measurable against that model.

### AR-016 — Concurrency control (NFR-DAT-002) contradicts the single-operator assumption
- **Severity:** HIGH
- **Category:** Security-Privacy / Quality
- **Evidence:** NFR-DAT-002 "prevent concurrent conflicting modifications"; `SRS.md` AS-006 "A single operator will work on one case at a time" `[ASSUMPTION]`; SRS §6.2 multi-operator workspace is FUTURE.
- **Problem:** NFR-DAT-002 demands a concurrency mechanism, but AS-006 says concurrency never happens in the MVP. Either the NFR is unverifiable (no scenario exercises it) or the assumption is wrong (two operators in one office, per RSK/multi-operator future).
- **Failure Scenario:** Two operators in the same office open the same case on different devices; last-writer-wins silently overwrites the other's verified corrections.
- **Impact:** Silent data loss, or an unverifiable requirement.
- **Current Status:** Open
- **Recommended Resolution:** Confirm single-operator-per-case for MVP; if so, scope NFR-DAT-002 to "no concurrent sessions modify the same case" (detect and warn) or drop it to future.

### AR-017 — Escalation-period and payment-timing semantics are unstructured
- **Severity:** HIGH
- **Category:** Data / Generation
- **Evidence:** DN-RENT-05 (escalation period) and DN-RENT-06 (payment timing) with no structured semantics; `Data Needs.md` §7.3 #4 escalation periods "every year / every 2 years / after 2 years" and #6 asymmetric notice; clause C02.
- **Problem:** "Every 2 years" vs "after 2 years" produce different compound-escalation math (AR-004), but the period is stored as an unstructured value. Payment timing (`अग्रिम`/`पश्चात्`) has no defined enum.
- **Failure Scenario:** The formula engine interprets "after 2 years" as "every 2 years"; rent escalates one period too early.
- **Impact:** Wrong financial clause.
- **Current Status:** Open
- **Recommended Resolution:** Define structured escalation-period semantics (start offset + interval) and a payment-timing enum, validated with the domain expert alongside AR-004.

### AR-018 — Multiple Second-Party individuals (joint tenants) are unmodeled
- **Severity:** HIGH
- **Category:** Scenario / Data
- **Evidence:** `Data Needs.md` §2.4 "Multiple Second Party individuals: not observed in the evidence; the same repeatable structure applies by symmetry, but this is marked **TO BE VALIDATED**"; FR-LR-011 covers only First-Party co-owners; §7.3 #8.
- **Problem:** If a joint-tenancy agreement is requested, the system has no defined rendering of a repeated Second Party block (S02/S05) and no repeated-entry requirement.
- **Failure Scenario:** A tenant couple asks for one agreement naming both; the operator can only enter one Second Party.
- **Impact:** MVP gap on a plausible, even likely, variation.
- **Current Status:** Open
- **Recommended Resolution:** Domain confirmation; if joint tenancy is in scope, extend FR-LR-011's repeatability symmetrically to the Second Party and verify the template's rendering of two tenants.

---

## 7. Medium-Severity Findings

### AR-019 — Bikram Sambat calendar semantics are undefined
- **Severity:** MEDIUM
- **Category:** Data / Generation
- **Evidence:** FR-LR-028 `TO BE VALIDATED`; BR-019 `[TEMPLATE-DERIVED]` (format `इतिसम्बत YYYY महिना MMMM GG गते रोज N`); OQ-DN-15 (BS vs AD); DN-DOC-01..04; mixed Devanagari/Latin numerals observed in the template.
- **Problem:** No requirement covers BS calendar correctness (month lengths, weekday calculation), BS↔AD conversion if ever needed, or input format. The weekday `रोज N` must be computed, not typed.
- **Failure Scenario:** The system types "रोज ३" or computes the wrong BS weekday for the entered date.
- **Impact:** Wrong date in a signed document.
- **Recommended Resolution:** Define the BS date engine contract (computation of month/weekday, input and display formats, numeral system).

### AR-020 — R-A-P-D structured area storage and validation are unresolved
- **Severity:** MEDIUM
- **Category:** Data
- **Evidence:** `Data Needs.md` DN-PROP-04 — "storage structure `[UNRESOLVED]` (OQ-DN-01)"; BR-020 (Ropani-Anna-Paisa-Dam format); Field Dictionary stores area as a single text; FR-LR-018 mentions R-A-P-D validation.
- **Problem:** Stored as text, per-component validation (Ropani/Anna/Paisa/Dam ranges, carry-over like 16 anna = 1 ropani) is impossible; stored structured, display and input conventions need definition.
- **Failure Scenario:** Operator enters "1-18-0-0" (invalid anna count); the system accepts it and the clause renders an impossible area.
- **Impact:** Invalid property area in the agreement.
- **Recommended Resolution:** Decide structured R-A-P-D storage, define component ranges and carry rules, and add validation to FR-LR-018.

### AR-021 — Draft-edit extent and re-generation behavior are undefined
- **Severity:** MEDIUM
- **Category:** Generation
- **Evidence:** FR-LR-033 `TO BE VALIDATED`; OQ-UC-03 (is draft editing MVP?); BR-018 (re-generation reuses Verified Case Data); FR-LR-046 (generation failure).
- **Problem:** If the operator edits draft text (not data), re-generating either overwrites the edits or the draft detaches from the template — both ungoverned. Combined with AR-005, edits can desynchronize calculated fields.
- **Failure Scenario:** Operator hand-corrects a clause in the draft; a later re-generation silently discards the correction.
- **Impact:** Lost work; divergent drafts.
- **Recommended Resolution:** Define the edit model (data-level vs text-level), whether draft editing is MVP at all, and re-generation behavior for edited drafts.

### AR-022 — Candidate Data retention is open, affecting privacy and re-verification
- **Severity:** MEDIUM
- **Category:** Data / Security-Privacy
- **Evidence:** OQ-DN-06; `SRS.md` §9.8/§7.8 `[OPEN QUESTION]`; DN-LIFE-01; NFR-PRI-002; `SRS.md` §10.2 re-verification open question.
- **Problem:** Whether pre-verification (possibly wrong) values are retained permanently or purged on correction is undecided; this drives both privacy exposure (wrong PII retained) and audit/re-verification capability.
- **Failure Scenario:** A mistyped citizenship number is corrected but the wrong value is retained indefinitely, resurfacing in audits.
- **Impact:** Privacy exposure; inconsistent with NFR-PRI-002.
- **Recommended Resolution:** Decide candidate-layer retention (tie to AR-006).

### AR-023 — Search criteria for past cases are unvalidated
- **Severity:** MEDIUM
- **Category:** Scenario
- **Evidence:** FR-LR-041 `SHOULD / TO BE VALIDATED`; `SRS.md` §20.2 FR-033 "domain inference — not domain-validated"; search dimensions never enumerated.
- **Problem:** Operators cannot reliably locate past cases until search dimensions are defined (party name, kitta, client, date, case type).
- **Failure Scenario:** A client asks "the agreement we made two years ago with the tenant in Ward 5"; the operator must browse every case.
- **Impact:** Retrieval failure in the real workflow.
- **Recommended Resolution:** Enumerate search dimensions with domain experts; confirm which are MVP.

### AR-024 — The audit event catalog is undefined
- **Severity:** MEDIUM
- **Category:** Quality / Security-Privacy
- **Evidence:** FR-LR-042 "significant events" never enumerated; NFR-AUD-001; DN-AUDIT-01 (event type); no event list and no audit-log retention rule.
- **Problem:** "Record significant events" is unverifiable until the events are enumerated, and audit logs will grow without bound with no retention policy (ties to AR-006).
- **Failure Scenario:** A dispute over who finalized a document cannot be resolved because "finalization" was never defined as a logged event, or logs are pruned without a rule.
- **Impact:** Unverifiable requirement; audit gaps.
- **Recommended Resolution:** Enumerate the audit event catalog (create, edit, verify, correct, generate, finalize, open, export, delete) and set log retention.

### AR-025 — Multi-source value conflicts are not surfaced as a workflow
- **Severity:** MEDIUM
- **Category:** Data / Scenario
- **Evidence:** `SRS.md` §11.6 OCR-006 "should support the operator in resolving information inconsistent between source documents" (Priority Could); no conflict-detection requirement for manually-entered or mixed data; Data Needs candidate/verified layer supports correction but not conflict detection.
- **Problem:** When two source documents disagree (e.g., two citizenship numbers), nothing requires the system to present the conflict; the operator discovers it only by reading both documents side by side — which FR-LR-110 (side-by-side view) defers.
- **Failure Scenario:** A Lalpurja and a municipality record give different ward numbers; the operator misses it and the agreement cites the wrong one.
- **Impact:** Unnoticed conflicting data in the final document.
- **Recommended Resolution:** Add a conflict-flagging requirement for values that appear in multiple acquisition sources with different values; decide whether MVP includes side-by-side comparison or a simple "conflicting values detected" warning.

### AR-026 — Case-directory organization criteria are unvalidated
- **Severity:** MEDIUM
- **Category:** Scenario
- **Evidence:** FR-LR-051/052/053; SRS FR-038 "and other supported classification criteria" (unspecified); FR-035 taxonomy `[TO BE VALIDATED]`.
- **Problem:** The directory's organization dimensions beyond Case Type are undefined; Recent Cases + directory + case-type browse overlap.
- **Failure Scenario:** The directory can filter only by LAND_RENT (the sole Case Type), making it functionally a flat list — yet three requirements claim distinct views.
- **Impact:** Redundant, ungrounded navigation requirements.
- **Recommended Resolution:** Define classification criteria or collapse FR-LR-051..053 into a single validated requirement.

### AR-027 — Provenance-query capability may exceed MVP need
- **Severity:** MEDIUM
- **Category:** Over-Engineering
- **Evidence:** DN-PROV-01/02 `PROPOSED`, `[TRACEABILITY REQUIRED]`; BR-052 (provenance is internal audit); no FR for a provenance UI; OCR deferred.
- **Problem:** Full per-value provenance querying, for an MVP whose primary acquisition is manual entry, may be more than the audit log (FR-LR-042) already provides.
- **Failure Scenario:** The team builds a provenance explorer nobody uses; meanwhile the audit trail is incomplete.
- **Impact:** Over-build; diverted effort.
- **Recommended Resolution:** Decide whether provenance query is MVP or satisfied by FR-LR-022 + FR-LR-042.

### AR-028 — Representation of a person with no Client record and no source document is unresolved
- **Severity:** MEDIUM
- **Category:** Data / Scenario
- **Evidence:** `Data Needs.md` OQ-DN-17 (options a/b/c explicitly offered); `Use Cases.md` OQ-UC-10; `Business Rules.md` OQ-BR-09; §2.2 (a Party need not be Client-backed).
- **Problem:** The requirements correctly guarantee that such a person *can* be represented, but not *how* (Client with zero documents, case-scoped Party, or other). The choice affects Client reuse, storage, and search.
- **Failure Scenario:** Every tenant in a "no-document" case is created as a permanent Client record cluttering the Client list; or the alternative — case-scoped Parties — makes Client search miss them.
- **Impact:** Data-model inconsistency.
- **Recommended Resolution:** Choose one representation model and document it (recommendation: case-scoped Party without a mandatory Client record).

### AR-029 — There is no "source document unusable" state
- **Severity:** MEDIUM
- **Category:** Scenario / Data
- **Evidence:** OCR-005 covers "expected information missing"; `SRS.md` §11.4 handwriting `[OPEN QUESTION]`; no requirement lets the operator mark a document as illegible/unusable and proceed manually with a recorded reason.
- **Problem:** When a document cannot be read (faded, stamped, handwritten), the operator's only recourse is silent manual re-entry — losing the link between the value and its provenance (BR-052).
- **Failure Scenario:** A faded Lalpurja is re-keyed from memory; the operator cannot record "document unreadable," and later review cannot tell the value came from an unreadable source.
- **Impact:** Provenance integrity gap.
- **Recommended Resolution:** Add an "unusable/unreadable" marker on source documents with a reason, feeding DN-SRC/DN-PROV.

### AR-030 — Devanagari / Latin numeral normalization is undefined
- **Severity:** MEDIUM
- **Category:** Data
- **Evidence:** Template uses mixed numerals (BS year in Devanagari, amounts with Latin digits); DN-RENT-01 figures; FR-LR-064 (Nepali Unicode entry); no canonical representation rule.
- **Problem:** Stored values may mix `०-९` and `0-9`; validation, rendering, and search behave inconsistently.
- **Failure Scenario:** An operator types the rent in Latin digits; another in Devanagari; the same case rendered two ways; search by amount misses one.
- **Impact:** Data integrity and retrieval issues.
- **Recommended Resolution:** Define a canonical numeral representation for storage and conversion rules for input/display.

---

## 8. Low-Severity Findings

### AR-031 — FR-LR-044 duplicates FR-LR-030 (missing-information reporting)
- **Severity:** LOW
- **Category:** Quality
- **Evidence:** FR-LR-044 (review-time) vs FR-LR-030 (generation-time); FR §8 flags both.
- **Problem:** Two requirements describe the same missing-field reporting behavior at different workflow points; risk of two divergent implementations.
- **Recommended Resolution:** Keep both behaviors but specify they share one missing-field reporting mechanism.

### AR-032 — FR-LR-040 and FR-LR-048 overlap (retrieval vs denial)
- **Severity:** LOW
- **Category:** Quality
- **Evidence:** FR-LR-040 (retrieve) and FR-LR-048 (deny unauthorized access); FR §8.
- **Recommended Resolution:** Confirm they describe one access-controlled retrieval behavior.

### AR-033 — FR-LR-042 overlaps NFR-AUD-001 (auditability)
- **Severity:** LOW
- **Category:** Quality
- **Evidence:** FR-LR-042 (event catalog) vs NFR-AUD-001 (logging capability); FR §8.
- **Recommended Resolution:** Resolve at SRS consolidation: one event catalog + one logging capability.

### AR-034 — NFR-PRI-003 duplicates NFR-SEC-004 (transfer protection)
- **Severity:** LOW
- **Category:** Quality
- **Evidence:** NFR-PRI-003 "Protect Information During Transfer (Privacy)" vs NFR-SEC-004 "Protect Information During Transfer."
- **Recommended Resolution:** Merge into one transfer-protection requirement referenced by both categories.

### AR-035 — DN-DOC-05 duplicates DN-GEN-04 (template identity/version)
- **Severity:** LOW
- **Category:** Quality
- **Evidence:** DN-DOC-05 (template identity and version) vs DN-GEN-04 (template identity and version); both CONFIRMED.
- **Recommended Resolution:** Keep one canonical template-version data need; reference it from both groups.

### AR-036 — FR-LR-009 (Case Notes) is weakly sourced
- **Severity:** LOW
- **Category:** Traceability
- **Evidence:** FR-LR-009 sourced only to DN-CASE-05, itself `PROPOSED` without SRS/template backing; FR §8.
- **Recommended Resolution:** Confirm Case Notes is MVP; otherwise defer.

### AR-037 — RBAC Administrator role + account management may exceed the assumed single-operator office
- **Severity:** LOW
- **Category:** Over-Engineering
- **Evidence:** FR-LR-002/003; AS-006 single operator; SRS §5.1.2 Administrator class.
- **Recommended Resolution:** Confirm whether account management (FR-LR-003) is MVP for a single-operator deployment, or defer.

### AR-038 — NFR-PER-001 and NFR-REL-002 are unmeasurable as written
- **Severity:** LOW
- **Category:** Quality
- **Evidence:** NFR-PER-001 "responsive interactions"; NFR-REL-002 "preserve data integrity during use"; the NFR document is intentionally qualitative-only with no numeric targets.
- **Recommended Resolution:** Accept as qualitative intent for the MVP, but record that they cannot be verified without targets.

### AR-039 — Authentication mechanism `[TO BE DETERMINED]` leaves security NFRs unverifiable
- **Severity:** LOW
- **Category:** Security-Privacy
- **Evidence:** `SRS.md` §7.1 auth mechanism `[TO BE DETERMINED]`; NFR-SEC-002/003/004; BR-003.
- **Recommended Resolution:** Select an authentication approach (even a provisional one) so NFR-SEC-002/003/004 become verifiable, or explicitly defer verification.

---

## 9. Observations

### AR-OBS-01 — OCR failure handling is conceptually sound
- **Severity:** OBSERVATION
- **Category:** Scenario
- **Evidence:** SRS §7.5/§11.1 manual-fallback paths; BR-050 (OCR never authoritative); BR-049/051 (manual entry first-class); FR-LR-065.
- **Observation:** The design correctly neutralizes the OCR risks (RSK-001/002) by making manual entry the primary path and OCR an optional enhancement. The residual gaps are AR-025 (conflict detection) and AR-029 (unusable-document marker), not the fallback itself.

### AR-OBS-02 — The volume of open questions is inconsistent with a baselineable MVP
- **Severity:** OBSERVATION
- **Category:** Quality
- **Evidence:** SRS §19 (46 open questions), Template Analysis §15 (28 OQ-TA), Data Needs §9 (17 OQ-DN), Business Rules §9 (9 OQ-BR), Use Cases §5 (10 OQ-UC), plus `Open Questions.md` (OQ-CM-*).
- **Observation:** More than 100 recorded open questions across artifacts. Individual markers are honest, but collectively they mean the requirement set is a strong *exploration* document and a weak *baseline* document.

### AR-OBS-03 — "Required when present" verification semantics are not enforced
- **Severity:** OBSERVATION
- **Category:** Data
- **Evidence:** Data Needs §7.1 marks fields like age "Required when present"; DN-VER verification model; no UI flow requirement for conditional verification prompts.
- **Observation:** The data model defines the state; the workflow requirement that the operator is *prompted* to verify a present high-sensitivity value is implicit, not required.

### AR-OBS-04 — The template evidence base is thin for a legally consequential generator
- **Severity:** OBSERVATION
- **Category:** Evidence
- **Evidence:** One reference PDF, 7 instances (6 complete); RSK-003 acknowledges template risk.
- **Observation:** A system that auto-generates legal agreements from a single observed template family should validate against more instances and other preparers before claiming clause completeness.

### AR-OBS-05 — No requirement covers professional accountability / second review
- **Severity:** OBSERVATION
- **Category:** Lifecycle
- **Evidence:** No second-operator review, handoff, or accountability requirement for finalization (only single-operator verification per AS-006).
- **Observation:** In a notarial workflow, a second pair of eyes before finalization is common. Not a defect for MVP, but the owner should consciously decide whether single-operator finalization is acceptable.

### AR-OBS-06 — "Automated field suggestions" was correctly rejected as unsourced
- **Severity:** OBSERVATION
- **Category:** Quality
- **Evidence:** FR §7 note: the task brief's "automated field suggestions" appears in no project document and was excluded.
- **Observation:** Good scoping discipline; no action.

---

## 10. Client/Party Scenario Analysis

Nine client/party scenarios were probed, combining whether a Client record exists, whether the person has source documents, and role multiplicity. These are derived from Data Needs §2.2 (Client vs Party), §2.3 (party presence modes), §2.7 (acquisition paths) and OQ-DN-17.

| # | Scenario | Requirements | Verdict |
|---|---|---|---|
| A | Landowner exists as a Client, is First Party, has source documents | DN-CLI, DN-P1 reuse, FR-LR-058/059, acquisition paths 1/2 | **Supported** |
| B | Tenant exists as a Client, is Second Party, has **no** source documents | BR-049 (no-doc representable), manual entry path 3 | **Supported** |
| C | No Client record; both parties entered directly as case Parties | Data Needs §2.2 (Party need not be Client-backed), FR-LR-010 | **Supported** |
| D | Same person is First Party in Case 1 and Second Party in Case 2 | §2.2 role-per-case model, BR-044 | **Supported** |
| E | Client record created **after** case creation | OQ-UC-06 open | **Partially specified** — order of association is undecided |
| F | Company as Second Party with registration | FR-LR-012, DN-P2-12..16 (conditional), BR-030 | **Supported (CONDITIONAL)** |
| G | Three co-owners as First Party, each also a Client | FR-LR-011, BR-031, §2.4 repeatable P1 | **Supported** |
| H | Person with no Client record and no source document (verbally supplied data) | OQ-DN-17 (options a/b/c), BR-048/049 | **Guaranteed representable, but representation model unresolved** (AR-028) |
| I | A finalized case's Client is later corrected/updated | OQ-DN-09, OQ-BR-08 | **Unspecified** (AR-010) |

**Result:** 6 of 9 scenarios are fully supported; scenario E (association order), H (representation model), and I (post-finalization update) are open decisions. None of the open ones blocks basic operation, but E and I affect data-model stability and should be decided before implementation.

---

## 11. Information Acquisition Analysis

Ten acquisition paths were probed, mapped to Data Needs §2.7 (five modeled paths) and BR-048..052.

| # | Path | Flow | Requirements | Verdict |
|---|---|---|---|---|
| A | Source document provided, operator copies values | Doc → manual copy → PROVIDED → verify | Path 1; DN-EXT-06 | **Supported** |
| B | Source document + OCR extraction | Doc → OCR → EXTRACTED → verify | FR-LR-105..108 (DEFERRED), DN-EXT | **Modeled; deferred** |
| C | Manual entry only, no document | Verbal/written → manual → PROVIDED → verify | BR-049/051, path 3 | **Supported** |
| D | Mixed: some fields from document, others manual | Per-value states → verify | Path 4; FR-LR-065 | **Supported** |
| E | Client-record pre-fill | Client → PROVIDED → verify | FR-LR-058/059, path 5 | **Supported** |
| F | Client reuse + additional manual fields | Client + manual → verify | FR-LR-058/059, UC-005 | **Supported** |
| G | Company-registration document | Doc → company fields (conditional) | FR-LR-012, DN-P2-12..16 | **Supported (CONDITIONAL)** |
| H | Two documents disagree on one value | Conflict → operator resolves | OCR-006 (Could) | **Partially specified** (AR-025) |
| I | No document, no Client → manual | Manual → PROVIDED → verify | BR-049, OQ-DN-17 | **Supported** |
| J | Document illegible → manual override | Unreadable doc → manual, reason lost | (none) | **Gap** (AR-029) |

**Result:** 8 of 10 paths are supported. The two gaps — conflict surfacing (H) and unusable-document marking (J) — are Medium-severity findings (AR-025, AR-029). The five-path model in Data Needs §2.7 is sound and the strongest part of the acquisition design.

---

## 12. OCR Failure Analysis

**Context:** OCR and automated extraction are deferred (FR-LR-105..108), so OCR failure is handled structurally by design rather than by a failure path: extraction, when it exists, produces Candidate Data that must be verified (BR-050, OCR-004), and manual entry is always available (BR-049/051).

**Failure modes probed:**

| Mode | Handling | Verdict |
|---|---|---|
| OCR produces wrong value | Candidate layer + mandatory verification (BR-050) | **Sound** |
| OCR unavailable / fails entirely | Manual entry fallback always available (SRS §7.5, §11.1) | **Sound** |
| OCR output has low confidence | FR-015 confidence indicators (DEFERRED with OCR) | **Deferred, acceptable** |
| Document unreadable (faded/handwritten) | No explicit marker (OCR-005 covers "info missing," not "doc unreadable") | **Gap** (AR-029) |
| Two documents conflict | OCR-006 "support the operator" (Could), no workflow | **Gap** (AR-025) |
| Handwriting recognition | SRS §11.4 `[OPEN QUESTION]` | **Acceptable while OCR deferred** |

**Result:** The architectural response to OCR risk is excellent — the MVP remains fully useful without OCR, exactly as required. The only real weaknesses are the two Medium findings (AR-025, AR-029). OCR itself is correctly gated on Phase 0.8 research.

---

## 13. Manual Nepali Entry Analysis

**Design strength:** Manual entry is first-class, not a fallback (Data Needs §2.7 path 3, BR-048/049/051). FR-LR-064 requires Nepali Unicode entry (MUST). NFR-USE-004 requires Nepali in the interface. The keyboard/IME is deliberately not prescribed — correct scoping.

**Gaps found:**

1. **Numeral normalization** (AR-030, MEDIUM): template mixes Devanagari and Latin numerals; no canonical representation.
2. **BS date entry** (AR-019, MEDIUM): entry format for `इतिसम्बत ... गते रोज` dates undefined.
3. **Structured area entry** (AR-020, MEDIUM): R-A-P-D entry/validation unresolved.
4. **"Required when present" prompts** (AR-OBS-03): the operator is not *required* to be prompted to verify present high-sensitivity fields.

**Result:** Manual entry is the best-covered area of the requirements. The three supporting data-semantics findings (AR-019/020/030) are clarification-level, not structural.

---

## 14. Missing Data Analysis

**Design strength:** The data-state model (Data Needs §2.3, §5.1) explicitly distinguishes `NOT_PROVIDED` / `PENDING` / `UNKNOWN` / `N/A` and treats "missing" differently per state. Missing-variable detection (§6.3) is aligned with FR-LR-030 and BR-017. The 16-scenario matrix (§7.2) is comprehensive.

**Gaps found — all at the decision boundary, where it matters most:**

1. **Blank mandatory-field finalization** (AR-002, CRITICAL): the rule is `[TO BE VALIDATED]`.
2. **Partial draft vs blocked generation** (AR-003, CRITICAL): self-contradictory.
3. **Missing-field reporting duplicated** (AR-031, LOW).
4. **"Complete" is undefined for FR-LR-045** (part of AR-002).

**Result:** The model correctly prevents *silent* missing data (NOT_PROVIDED is never treated as "no data"). What it does not do is decide what happens at the edges — blank placeholders in mandatory fields, and partially-identified parties. Those are the CRITICAL findings.

---

## 15. Clause/Variable Analysis

**Design strength:** The clause/variable model (Data Needs §6) is well-built: clause inventory C01–C13, the variable chain `DN → DN-VAR → DN-CLAUSE → DN-GEN`, conditional pattern `Condition → Required Data → Clause → Output`, and missing-variable detection.

**Findings affecting the clause model:**

| # | Issue | Finding |
|---|---|---|
| 1 | Use-purpose trigger set incomplete/unvalidated | AR-009 (HIGH) |
| 2 | Financial formulas (C02) unvalidated | AR-004 (CRITICAL) |
| 3 | Escalation-period semantics unstructured (C02) | AR-017 (HIGH) |
| 4 | Notice-period units ambiguous (C08) | AR-013 (HIGH) |
| 5 | Renewal clause C13 observed once, `TO BE VALIDATED` | (open) — see §26 |
| 6 | Which clauses are mandatory vs optional per purpose (OQ-BR-01) | (open) — see §26 |
| 7 | Deposit/utilities modeling conflict (C06, deposit absent) | §22 C6 |

**Result:** The clause *architecture* is sound and traceable. The clause *content* (which clauses, under which conditions, computed how) is the unresolved part — all validation-grade findings.

---

## 16. Template Traceability Analysis

**Design strength:** Every Field Dictionary field (56/56) is mapped to a Data Need (Data Needs §7.1); the traceability matrix (FR §6) is complete to field level; variable names in Template Analysis §13 map to DN-VAR bindings.

**Gaps:**

1. **6 `[UNRESOLVED]` template/SRS fields** remain unmapped or contradicted: writer license number (OQ-DN-03), deposit amount, lease start date, utility responsibilities, party contact, witness citizenship (Data Needs §7.1).
2. **Group-level traceability gaps** explicitly marked `[TRACEABILITY REQUIRED]`: DN-PTY, DN-OWN, DN-PAY, DN-PROV, DN-WRI-02 (Data Needs §8.1) — no dedicated FR or SRS §9 entry.
3. **DN-WRI-02** (writer license) has no dedicated functional requirement; FR-LR-016 covers witnesses and writer but not the license field.

**Result:** The traceability *coverage* is strong; the gaps are honest and marked. But "flagged [UNRESOLVED]" is not "resolved" — six template-relevant fields and five data groups have no clean home at baseline. See §21 for the consolidated gap list.

---

## 17. Land Rent Scenario Coverage

**Design strength:** Data Needs §7.2 covers 16 party-presence × data-state scenarios and §7.3 covers 16 land-rent variations, all with per-scenario generation/finalization outcomes and evidence.

**Where the coverage is actually decided vs deferred:**

| Scenario class | Covered as a *decision* | Covered as `[TO BE VALIDATED]` |
|---|---|---|
| Both parties present, all data verified | ✓ (normal agreement) | — |
| Data pending verification | ✓ (blocked until verified) | — |
| Required data missing | ✓ (blocked, gaps reported) | — |
| Data `UNKNOWN` (blank) | — | ✓ (4, 8, 12, 16) — AR-002 |
| Absent Second Party | ✗ (self-contradictory) | ✓ — AR-003 |
| Partial draft | — | ✓ (8, 12) — AR-003 |
| Multiple Second Parties | — | ✓ (§2.4) — AR-018 |
| Guthi land | — | ✓ (BR-033) |
| Use purpose list | — | ✓ (OQ-DN-05) — AR-009 |

**Result:** The matrix is comprehensive *as an analysis*. As a baseline, it encodes undecided behavior as `[TO BE VALIDATED]` in exactly the places that matter (blank mandatory fields, absent parties). This is the strongest evidence supporting the NOT READY verdict.

---

## 18. Document Lifecycle Analysis

**Design strength:** Two-lifecycle separation (data lifecycle vs document lifecycle, SRS §10.1/§10.2, Data Needs §2.5) is clean. Draft → review → explicit human finalization is well-gated (FR-LR-032..039, BR-001/002/006/038/047).

**Findings affecting the lifecycle:**

1. **Execution step missing** — signature/execution method undefined (AR-007, HIGH).
2. **Output format unconfirmed** (AR-008, HIGH).
3. **Draft-version retention** open (SRS §10.4) and **revision model** open (SRS §10.7: new version vs new case) — unresolved (see §26).
4. **Draft editing extent** undefined (AR-021, MEDIUM).
5. **Re-verification flow** open (SRS §10.2: does new info always flow through the full lifecycle?) — unresolved (see §26).
6. **Figures/words integrity** under edit (AR-005, CRITICAL).

**Result:** The lifecycle is sound up to the moment of generation; the gaps cluster at the edges — what the operator can do to a draft, and what happens after finalization.

---

## 19. Case Persistence Analysis

**Design strength:** Decision 004 (persistent cases), BR-039/040, FR-LR-050, DN-CASE-09/DN-LIFE-06 all agree: cases and finalized documents persist and are retrievable after finalization.

**Findings affecting persistence:**

1. **Retention/archival/backup/deletion policy absent** (AR-006, HIGH) — the single biggest persistence gap; acknowledged everywhere as `[TO BE VALIDATED]`.
2. **Lifecycle end-state contradiction** (AR-012, HIGH) — Archived/Closed in SRS vs no archival state in Data Needs.
3. **Candidate-data retention open** (AR-022, MEDIUM).
4. **Audit-log retention open** (AR-024, MEDIUM).
5. **Storage architecture undecided** (SRS §15.5) — feeds AR-006 and AR-015.

**Result:** The *intent* of persistence is clear and consistent; the *policy* that makes it safe (retention, deletion, backup) is absent. Since retention conflicts with NFR-PRI-002 (minimization), this is a decision the owner must make, not a gap the team can fill.

---

## 20. Security/Privacy Analysis

(Header completed from the brief's truncation.)

**AuthN/AuthZ:** FR-LR-001..003 define authentication and RBAC (Operator/Administrator); BR-003/015/037 define access rules; NFR-SEC-002 requires authentication. The mechanism is `[TO BE DETERMINED]` (SRS §7.1) — acceptable as non-prescriptive, but it leaves NFR-SEC-002/003/004 unverifiable (AR-039). No case-level or client-level access-control requirement exists (all-or-nothing at the account level).

**Data protection:** NFR-SEC-001 (protect stored data), NFR-SEC-004 / NFR-PRI-003 (transfer) — the latter two duplicate each other (AR-034). NFR-PRI-001/004/005 govern access to personal and finalized-document data. No encryption requirement is stated explicitly; "protect" is qualitative.

**Privacy vs retention tension:** NFR-PRI-002 ("avoid unnecessary retention") directly conflicts with the "retain indefinitely" intent (BR-040) until a retention policy exists (AR-006). Sensitive PII (citizenship numbers, lineage, property details) is retained with no deletion rule.

**Human-authority boundary:** BR-038/047 correctly keep legal-validity determination with the human; SRS §3.5 and §10.5 disclaim system-determined validity. This is the strongest security-relevant design decision.

**Assessment:** The security requirements are sound at the principle level and weak at the verifiable-specification level. The two decisions that matter are the retention policy (AR-006) and the authentication mechanism (AR-039). No finding rises above HIGH in this section, and neither is about a design flaw — both are about absent decisions.

---

## 21. Traceability Gaps

Consolidated list of values and groups with no clean requirement home at baseline:

| Gap | Where marked | Consequence | Finding |
|---|---|---|---|
| DN-PTY (party role model) | Data Needs §8.1 `[TRACEABILITY REQUIRED]` | Role model not explicit in SRS §9 | — |
| DN-OWN (ownership) | Data Needs §8.1 `[TRACEABILITY REQUIRED]` | No dedicated FR; only BR-033 | — |
| DN-PAY (payment/receipt) | Data Needs §8.1 `[TRACEABILITY REQUIRED]` (partial) | No dedicated FR | — |
| DN-PROV (provenance) | Data Needs §8.1 `[TRACEABILITY REQUIRED]` | No dedicated FR/UI | AR-027 |
| DN-WRI-02 (writer license) | Data Needs §7.1 `[UNRESOLVED]`, OQ-DN-03 | No FR covers the license field | — |
| Writer license, deposit, lease-start, utilities, contact, witness citizenship | Data Needs §7.1 `[UNRESOLVED]` (6 fields) | Unmapped/contradicted template or SRS fields | §22 C4–C6 |
| FR-LR-009 (Case Notes) | FR §8 weakly sourced | PROPOSED-only backing | AR-036 |
| FR-LR-031 (output format) | FR §8 unsourced | Unconfirmed format | AR-008 |
| SRS §20.2 unsourced set | SRS §20.2 | Auth mechanism, search criteria, UI language, performance targets lack validated source | AR-039, AR-023 |
| Cross-document numbering drift | Data Needs §11 | One stale reference fixed; FR-LR scheme (FR-LR-###) vs SRS scheme (FR-###) remain dual | — |

**Result:** Every gap is honestly marked in the artifacts — which is good — but a traceability gap is still a gap: 5 groups and 6 fields have no authoritative functional requirement, and 2 ID schemes are in live use across artifacts.

---

## 22. Contradictions

| # | Artifact A | Artifact B | Issue | Finding |
|---|---|---|---|---|
| C1 | SRS §6.1/§7.3/§3.4: capture/upload is MVP (Must) | FR §7: FR-LR-101..104 DEFERRED | MVP boundary differs between synchronized artifacts | **AR-001 (CRITICAL)** |
| C2 | Data Needs §6.3: blank Second Party proceeds where template permits | Data Needs §7.2 (scenario 5) + FR-LR-030/BR-017: generation blocked when party missing | Partial-draft behavior self-contradictory | **AR-003 (CRITICAL)** |
| C3 | SRS FR-007: lifecycle includes "Archived/Closed" | Data Needs §5.3: no archival state; SRS finer states demoted to PROPOSED | Two state machines, different end-states | **AR-012 (HIGH)** |
| C4 | SRS §9.4: parties include "contact" | Template: no contact field exists | SRS field has no template backing | AR — flagged `[UNRESOLVED]` OQ-DN-11 |
| C5 | SRS §9.4: witness citizenship + "at least two per party" | Template: witnesses carry name/address/age only, 1–3 total; BR-008 unverified | Legal rule vs observed template | AR — flagged OQ-DN-12, BR-008 |
| C6 | SRS §9.5: deposit + utility responsibilities as rental terms | Template: no deposit field; utilities are clause-level (C06) | Deposit not template-backed | AR — flagged OQ-DN-13 |
| C7 | SRS §9.4: citizenship as party information | Data Needs §7.1: citizenship Optional/PROPOSED | Mandatory-ness authority ambiguous | AR-002 (CRITICAL) tie-in |
| C8 | NFR-PRI-002: avoid unnecessary retention | BR-040/Decision 004: retain indefinitely | No policy reconciles the two | AR-006 (HIGH) tie-in |
| C9 | SRS §21: FR+NFR counts (FR-001..049, 13 NFR) | FR doc: FR-LR-001..065; NFR doc: 26 NFRs | Two ID schemes and count bases in live use | — (note only) |

**Result:** 3 contradictions are self-flagged by the artifacts (C4–C6) and 6 are found by this review (C1–C3, C7–C9). The three artifact-vs-artifact contradictions (C1–C3) are the ones that must be fixed at baseline because they describe the MVP differently.

---

## 23. Duplications

| # | Item A | Item B | Finding |
|---|---|---|---|
| D1 | FR-LR-044 (missing info at review) | FR-LR-030 (missing info at generation) | AR-031 |
| D2 | FR-LR-040 (retrieval) | FR-LR-048 (deny unauthorized) | AR-032 |
| D3 | FR-LR-042 (audit events) | NFR-AUD-001 (logging capability) | AR-033 |
| D4 | NFR-PRI-003 (transfer, privacy) | NFR-SEC-004 (transfer, security) | AR-034 |
| D5 | DN-DOC-05 (template identity/version) | DN-GEN-04 (template identity/version) | AR-035 |
| D6 | FR-LR-035 / FR-LR-062 / FR-LR-063 (document-type distinction) | — | overlapping trio |
| D7 | FR-LR-036 (finalization metadata) / DN-DOC-06 / DN-GEN-03 | — | same metadata in 3 places |
| D8 | SRS §13.5 (secure transmission) | NFR-SEC-004 | cross-artifact duplicate |
| D9 | FR-LR-051/052/053 (recent cases, open existing, browse by type) | — | three views, one underlying list (see AR-026) |

**Result:** No duplication is harmful alone; the pattern indicates the artifacts were written independently and merged. All are LOW-severity and resolvable at SRS consolidation — none blocks baseline except as part of the general "unreconciled duplicates" quality debt.

---

## 24. Over-Engineering

| # | Item | Why over-built for MVP | Finding |
|---|---|---|---|
| O1 | Full provenance-query capability (DN-PROV-02) | Manual-entry MVP; audit log may suffice | AR-027 |
| O2 | RBAC Administrator role + account management (FR-LR-002/003) | Single-operator office assumed (AS-006) | AR-037 |
| O3 | Case-directory + browse-by-type (FR-LR-051..053) | Only one Case Type exists (LAND_RENT); directory is a flat list | AR-026 |
| O4 | NFR-PER-001 / NFR-REL-002 | No targets, no deployment model → unmeasurable | AR-038 |
| O5 | Candidate/Verified/Provenance/Audit stack (133 data needs) | Defensible architecture, but heavy for manual entry | (observation — justified) |
| O6 | Case Type abstraction (DN-CTYPE) | Single type today | (observation — justified future-proofing) |

**Result:** Over-engineering is mild and mostly LOW. The notable risk is the opposite direction — see §25. O1–O4 are trimmable; O5/O6 are defensible.

---

## 25. Under-Specification

| # | Area | What is missing | Finding |
|---|---|---|---|
| U1 | Execution of the document | Signature method (physical/digital); link to executed copy | AR-007 (HIGH) |
| U2 | Output contract | Format, print layout, Devanagari font/rendering, pagination | AR-008 (HIGH) |
| U3 | Conditional triggers | Complete use-purpose list; clause membership per purpose | AR-009 (HIGH) |
| U4 | Notice period | Value+unit; per-party asymmetry | AR-013 (HIGH) |
| U5 | Escalation semantics | Period math ("every 2 years" vs "after 2 years"), payment-timing enum | AR-017 (HIGH) |
| U6 | BS calendar | Month/weekday computation, input format, numeral system | AR-019 (MEDIUM) |
| U7 | R-A-P-D area | Structured storage, component ranges, carry rules | AR-020 (MEDIUM) |
| U8 | Draft editing | Allowed edit types; re-generation behavior | AR-021 (MEDIUM) |
| U9 | Candidate retention | Purge vs retain on correction | AR-022 (MEDIUM) |
| U10 | Search | Search dimensions | AR-023 (MEDIUM) |
| U11 | Audit events | Event catalog; log retention | AR-024 (MEDIUM) |
| U12 | Conflict handling | Multi-source conflict surfacing | AR-025 (MEDIUM) |
| U13 | Unusable documents | "Unreadable" marker + reason | AR-029 (MEDIUM) |
| U14 | Draft versions / revision model | Retain previous drafts? New version vs new case on revision? | (SRS §10.4/§10.7 open) |
| U15 | Re-verification flow | Does new info re-enter the lifecycle? | (SRS §10.2 open) |

**Result:** Under-specification outnumbers over-engineering by a wide margin and dominates the HIGH tier. The pattern is consistent: the requirements specify the *model* precisely and the *decisions* hardly at all.

---

## 26. Open Questions Revealed

Beyond the ~100 questions the artifacts already record, this review surfaced the following new or sharpened questions that must be answered for baseline:

| # | Question | Origin |
|---|---|---|
| Q1 | When a manually-entered value conflicts with a source document, which wins by default, and who decides? | AR-025 (OCR-006 covers only OCR) |
| Q2 | Are amount figures stored canonically in Latin or Devanagari numerals? | AR-030 |
| Q3 | Does the system retain a copy of the *executed* (signed/notarized) document, or only the generated Finalized System Record? | AR-007 |
| Q4 | What exactly is the audit event catalog? | AR-024 |
| Q5 | What happens to in-flight cases and open drafts when a template version is superseded? | AR-014 |
| Q6 | Is single-operator-per-case enforced, or merely assumed? | AR-016 |
| Q7 | May finalized documents ever be deleted — and by whom? | AR-006 |
| Q8 | What are the exact semantics of escalation "period" (start offset + interval) for compound math? | AR-017 |
| Q9 | Is "residence" a distinct purpose with its own clause set, and is "business+residence" a composite? | AR-009, Data Needs §7.3 #1 |
| Q10 | Is there a second-operator review step before finalization (professional accountability)? | AR-OBS-05 |

---

## 27. Requirements That Appear Sound

The following survived adversarial probing and should be preserved unchanged:

1. **Product decisions 004–008** (persistent cases; Case Type; Client distinct from Application User and Party; Source/Draft/Finalized document types; human-only finalization) — coherent and consistently applied across all artifacts.
2. **Human Authority Principle and its enforcement** — BR-001, BR-004, BR-014, BR-038, BR-047; FR-LR-045; SRS §3.5/§10.5 disclaimers. The system never presents automated output as final and never claims legal validity.
3. **Manual-entry-first acquisition model** — BR-048..051, FR-LR-064/065, Data Needs §2.7. "No document" never means "not representable."
4. **Candidate → Verified two-layer data model** — DN-EXT/DN-VER; extraction is never authoritative; verification is mandatory before generation.
5. **Data-state model with explicit `UNKNOWN`/`N/A`** — Data Needs §2.3/§5.1; missing values are never silently treated as "no data."
6. **Missing-variable detection** — Data Needs §6.3, aligned with FR-LR-030 and BR-017 (its internal contradiction with §7.2 notwithstanding).
7. **Template-derived format rules** — BR-019 (BS date format), BR-020 (R-A-P-D), BR-021/022 (words-after-figures) are grounded in observed instances.
8. **The 16-scenario and 16-variation matrices** (Data Needs §7.2/§7.3) — comprehensive analysis artifacts; keep as-is.
9. **Honest marking discipline** — `[TO BE VALIDATED]`/`[UNRESOLVED]`/`[OPEN QUESTION]` everywhere the evidence runs out. Rare and valuable.

---

## 28. Recommended Resolution Order

The owner should resolve these in dependency order, not alphabetical order. Each step consumes the previous decision.

1. **MVP boundary decision** (AR-001): capture/upload in or out of MVP; synchronize SRS §6.1/§7.3/§3.4/§15.1 and the FR deferral list. *Everything downstream depends on this.*
2. **Document-completeness rule** (AR-002 + AR-003): define mandatory-vs-optional per field for *finalization*; define partial-draft policy and blank-placeholder rule; resolve the §6.3 vs §7.2 contradiction. This is a domain-expert decision.
3. **Financial validation** (AR-004 + AR-017): validate BR-024..026 and escalation-period semantics against complete instances with a domain expert.
4. **Words/figures integrity** (AR-005 + AR-021): decide the draft-edit model and calculated-field protection.
5. **Legal-rule decisions** (AR-009, BR-008 witness rule, AR-013 notice units, AR-018 joint tenancy): legal-expert confirmation for conditional clauses, witness counts, and party multiplicity.
6. **Execution + output contract** (AR-007 + AR-008): signature method, output format, print layout, executed-copy retention.
7. **Retention/archival/backup/deletion policy** (AR-006 + AR-022 + AR-024): one policy decision covering every artifact class; feeds NFR-BAC/PRI.
8. **Client/Case model decisions** (AR-010, AR-011, AR-028): post-finalization Client updates, source-doc association level, no-document person representation.
9. **Data-semantics clarifications** (AR-019 BS calendar, AR-020 R-A-P-D, AR-030 numerals): spec-level, quick.
10. **Lifecycle + deployment** (AR-012, AR-015, AR-016): authoritative state machine; deployment/connectivity model; concurrency scope.

LOW items (AR-031..039) and duplications (§23) can be resolved during the SRS consolidation pass without blocking anything.

---

## 29. Baseline Readiness Assessment

**Verdict: NOT READY TO BASELINE.**

**Rationale:** Five CRITICAL findings — the contradictory MVP boundary (AR-001), the permitted finalization of blank mandatory fields (AR-002), the self-contradictory partial-draft behavior (AR-003), the unvalidated financial engine (AR-004), and the ungoverned figures/words integrity (AR-005) — each independently block a defensible baseline. Thirteen HIGH findings add major undefined behaviors that would force rework during development.

**What must happen before baseline:**

1. All 5 CRITICAL findings resolved (decision made and recorded in the Decision Log with a named owner and date), **or** explicitly accepted by the project owner with the risk documented.
2. The 13 HIGH findings either resolved or explicitly deferred with a recorded rationale.
3. The three artifact-vs-artifact contradictions (§22 C1–C3) reconciled so every artifact describes the same MVP.

**What does NOT need to happen before baseline:** LOW findings, duplications, and the security-mechanism choices (AR-039) can wait for the SRS consolidation pass.

**On the possibility of "accepted risk":** If the owner chooses to baseline with open CRITICAL items, that acceptance must be explicit, per-item, and recorded in the Decision Log — not absorbed silently into a "baseline approved" statement. The artifacts themselves are honest enough to be baselined as *documents*; the *decisions* they defer are not.

**Closing note:** This review found the requirement set to be unusually strong in structure and unusually honest about its gaps. The reason it is not ready to baseline is not poor writing — it is the absence of roughly 15 domain, legal, and product decisions that no amount of requirement drafting can substitute for. The fastest path to a baseline is a set of domain-expert and legal-expert sessions covering §§28.1–28.7, after which the artifacts can be synchronized and re-reviewed in an afternoon.

---

*End of Requirements Adversarial Review — Working Draft, 2026-08-13.*
*No requirement file was modified in the production of this review.*
