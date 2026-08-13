# Clause Library Schema

> **Working Analysis Document** — This document defines the schema, vocabulary, and conventions used by every clause entry in the clause libraries (starting with the [[Agricultural Land Rent Clause Library]]). It is a project-internal analysis artifact, NOT a legal document. It does not assert legal validity or legal authority.

| Field | Value |
|---|---|
| **Document Status** | Draft — Initial Analysis Complete |
| **Date** | 2026-08-13 |
| **Related Analysis** | `Land Rent Template Analysis.md`, `Data Needs.md` §6 |
| **Related Artifacts** | `Agricultural Land Rent Clause Library.md` |
| **Scope** | Schema + conventions for cataloguing clauses extracted from reference documents |

---

## 1. Purpose

The Clause Library is a **source-derived domain-analysis artifact**. It catalogues, in verbatim source wording, every clause found in the project's reference documents, together with:

- the variables each clause references,
- the conditions under which each clause is included,
- traceability to existing Data Needs / Business Rules / Use Cases / Functional Requirements where such mappings genuinely exist,
- explicit marking of gaps, ambiguities, and unvalidated content.

The library is a **description of what the reference documents contain**. It is NOT a specification of what documents "should" contain, and it does not invent legal rules, clauses, variables, or requirements. Where the source material is missing, ambiguous, or inconsistent, the library says so and raises an open question; it never silently fixes the source.

---

## 2. Definitions

| Term | Definition |
|---|---|
| **Clause** | A discrete, numbered provision of a reference document (e.g., a तपसिल item), or a coherent named provision (e.g., the preamble party-identification formula) that recurs across documents. |
| **Source Document** | A reference document from which clauses are extracted. Identified by a stable `SD-###` ID. Multiple instances may exist within a single physical file (the supplied PDF contains 8 instance documents). |
| **Instance** | One filled example document within a reference file. |
| **Canonical Source Text** | The verbatim wording chosen as the library's primary rendering of a clause, with `[VARIABLE_NAME]` placeholders replacing filled values. Where instances differ, the canonical text follows the most representative instance and differences are recorded as variants. |
| **Variant** | A recorded difference in how the same clause is expressed across instances. Classified as **wording** (synonymous phrasing), **structural** (different clause ordering/segmentation), **parameter** (different numeric/enumerated values), or **conditional** (inclusion depends on a condition). A difference only in numeric values is a parameter variant, never a separate clause. |
| **Variable** | A replaceable value referenced by a clause. Named per the project variable conventions (§5) and traced to a Data Need ID where a mapping exists. |
| **Condition** | The circumstance under which a clause is included or under which a clause's obligation applies. |
| **Applicability** | The scope of cases/use purposes to which the clause applies. If not established from the supplied sources, recorded verbatim as "Not established from supplied sources." |
| **Category** | The subject-matter class of the clause. Categories used are those that represent actual source material (see §6); no new categories are invented to force-fit content. |

---

## 3. Clause ID Convention

- Clause IDs use the pattern **`CLAUSE-<DOMAIN>-###`**, where:
  - `<DOMAIN>` identifies the reference-document family. `AGR` = agricultural land-rent agreements.
  - `###` is a zero-padded sequence number (001, 002, ...) assigned in source order of first appearance.
- Examples: `CLAUSE-AGR-001`, `CLAUSE-AGR-015`.
- The `CLAUSE-AGR-###` IDs are **distinct from** the clause-inventory IDs (C01–C13) defined in `Data Needs.md` §6.1. `CLAUSE-AGR-###` identifies a source-derived clause in this library; `C###` identifies a project-level clause-topic inventory entry. Where a real mapping exists, it is recorded in the clause's Related Data Needs / Traceability sections. No forced 1:1 mapping is assumed: this library may find clauses that do not correspond to any C### (reported as a "Potential Data Needs gap"), and some C### topics may not be present in the agricultural sources.
- If a new domain library is created later (e.g., business/residential leases), it uses its own domain tag (e.g., `CLAUSE-LRB-###`) and its own source set.

---

## 4. Status Vocabulary

Every clause carries three status fields:

### 4.1 Clause Status

| Status | Meaning |
|---|---|
| **Draft** | Entry is written but not yet checked against the source or cross-artifacts. |
| **Source-Derived** | Entry reflects a clause actually present in the cited source instance(s); source wording verified against the extraction. |
| **Validated** | Source-derived AND confirmed by domain/legal review (external to this document set). Not achievable from supplied sources alone. |
| **Needs Review** | Entry has an unresolved ambiguity, contradiction, or gap that requires human (domain/legal) review before it may be relied upon. |

### 4.2 Legal Validation Status

| Status | Meaning |
|---|---|
| **Not assessed** | No legal assessment performed (default — this library performs no legal analysis). |
| **Requires legal review** | The clause touches legally consequential matters (validity, enforceability, registration, statutory thresholds). |
| **Legal review pending** | A review has been requested but not completed. |

### 4.3 Domain Validation Status

| Status | Meaning |
|---|---|
| **Source-confirmed** | Presence/behavior confirmed by the supplied source instances. |
| **Domain validation required** | Interpretation, completeness, or real-world frequency requires domain-expert (e.g., the project owner's parents) confirmation. |
| **Domain validation pending** | Validation requested but not completed. |

> This library does NOT perform legal interpretation. Terms such as "valid," "enforceable," or "required by law" never appear as conclusions; where a legal question is raised, it is raised as an open question and marked "Requires legal review."

---

## 5. Variable Naming Convention

- Variables are named using the dotted convention already used in `Land Rent Template Analysis.md` §13.1 (e.g., `party.first.name`, `rent.amount`, `property.kittaNumber[]`, `term.durationYears`).
- Where a variable maps to an existing Data Need, the Data Need ID (e.g., `DN-P1-01`) and the Template Analysis Field ID (e.g., `P1_FULL_NAME`) are recorded alongside the dotted name in the Variables table.
- Where a variable is observed in the source but has no existing Data Need, it is recorded with its dotted name and flagged as a **Potential Data Needs gap** (see §10); it is never silently assigned a new invented Data Need ID.
- Compound values that render as one surface string (e.g., land area `Ropani-Anna-Paisa-Dam`) are noted so the traceability matrix can map the surface variable to the underlying Data Need (e.g., `DN-PROP-04`).

---

## 6. Clause Categories

Categories are drawn from the actual content of the agricultural sources. A clause is assigned the category that best represents its subject matter; category names are reused across clauses only where the subject matter genuinely matches.

| Category | Scope (source-derived) |
|---|---|
| **Preamble — Party** | Party identification, lineage, address, citizenship, party designation formula. |
| **Preamble — Legal Basis & Execution** | Governing-law references, consent, execution/attestation formula. |
| **Property & Grant** | Land description, area, use purpose, term, offer/acceptance. |
| **Rent & Payment** | Rent amount (figures/words), period, escalation, payment timing. |
| **Land Use & Cultivation** | Permitted/prohibited cultivation, agricultural restoration. |
| **Party Obligations** | Uninterrupted use, taxes/expenses, construction permission, structure handover. |
| **Subletting & Third Parties** | Prohibition on re-letting to third parties. |
| **Termination & Notice** | Notice periods, termination conditions. |
| **General Provisions** | Amendment, governing law (residual), breach/remedy, renewal. |

---

## 7. Canonical Source Text Convention

- Canonical Source Text is reproduced **verbatim** from the source instance, preserving original spelling, spacing, punctuation, and Devanagari numerals. Nothing is "cleaned up."
- Filled values are replaced by `[VARIABLE_NAME]` placeholders. The replaced text is noted in the Variables table with the source evidence.
- **Corrupt or ambiguous source text is preserved as-is and explicitly marked** using the `⟨sic⟩` marker immediately after the affected string, with an explanatory note in the clause's Open Questions / Validation Notes. Example: `भाडा डर ⟨sic⟩` — meaning "the source renders this as `डर`; intended `दर` is a reader hypothesis, not a correction." A `<sic>` occurrence is never silently corrected in the canonical text.
- Instances that differ are recorded under **Variants**; the canonical text does not merge them.
- When the extraction itself is uncertain, this is stated (the supplied PDF was extracted with `pdftotext -layout`; Devanagari spacing artifacts such as `द ुवै` are extraction artifacts of the source PDF, not typographical corrections).

---

## 8. Condition Convention

- Conditions are recorded only where the source supports them (presence of a clause only in certain instances; a clause that applies only under stated circumstances).
- If a condition is suspected but not proven by the sources, it is recorded as **"Condition requires validation."** and referenced in the clause's Open Questions / Validation Notes.
- Observed conditional triggers in the agricultural sources include (list is illustrative, per-instance details are in the library):
  - use purpose (agriculture vs other)
  - presence of physical structures / construction
  - party multiplicity (co-owners, company tenant)
  - kitta multiplicity
  - notice-period configuration (uniform vs asymmetric per party)

---

## 9. Variant Convention

Variants are classified and recorded as:

| Variant Type | Meaning | Example (illustrative) |
|---|---|---|
| **Wording** | Synonymous or near-synonymous phrasing of the same provision | `द्रितिय` vs `द्वितीय` for "Second Party"; `सहिंता` vs `संहिता` |
| **Structural** | Different clause ordering, segmentation, or merging | Subletting prohibition embedded in the crop clause vs a separate clause |
| **Parameter** | Different numeric/enumerated values | Notice period 30 vs 60 days; escalation rate 5% vs 10% |
| **Conditional** | Presence/absence governed by a condition | Agricultural-restoration clause present only in agriculture instances |

Rules:
- **A difference only in parameter values is a parameter variant of one clause, never a separate clause.**
- Variants are recorded against the clause they belong to, with the source instances where each form appears.

---

## 10. Gap-Reporting Convention

Gaps are reported using a fixed vocabulary so they are machine-searchable and never silently "fixed":

| Gap label | Meaning |
|---|---|
| `Potential Data Needs gap: [X]` | A variable, clause, or field observed in the source has no existing Data Need mapping (see `Data Needs.md`). |
| `Potential FR gap: [X]` | Functionality implied by the source but not covered by existing Functional Requirements. |
| `Potential SRS inconsistency: [X]` | The source contradicts a statement in the SRS or a derived artifact (never auto-resolved; flagged for review). |
| `Condition requires validation.` | A condition is suspected but not proven by the sources. |
| `Not established from supplied sources.` | Applicability or other fact cannot be determined from the reference documents supplied. |

Additionally, every gap, ambiguity, or unvalidated item is assigned an Open Question ID of the form `OQ-CL-###` in the library's Open Questions section. New questions are added to the master `00 - Project Control/Open Questions.md` only when they are genuinely project-level (not clause-library-local).

---

## 11. Traceability Conventions

### 11.1 Related Artifacts

| Relation | Recorded as | Convention |
|---|---|---|
| Data Needs | Related Data Needs | Existing IDs only (e.g., `DN-P1-01`); gaps use the §10 vocabulary. |
| Business Rules | Related Business Rules | Existing IDs only (e.g., `BR-027`); no rules invented here. |
| Use Cases | Related Use Cases | Existing IDs only (e.g., `UC-011`). |
| Functional Requirements | Related Functional Requirements | Existing IDs only (e.g., `FR-LR-025`). |

No mapping is forced. If a clause has no plausible relation, the field is left empty rather than stretched.

### 11.2 Variable Traceability Chain (per variable)

The chain required for traceability is:

```
Clause (CLAUSE-AGR-###)
  → Variable ([dotted name])
  → Data Need (DN-###)
  → Entity (First Party / Second Party / Property / Term / Witness / Writer / Document)
  → Acquisition Source (OCR / Manual Entry / Existing Client Data / Case Data / Derived-Calculated / Not yet defined)
  → Verification (Required / Not required)
  → Document Output (section of the generated document the variable feeds)
```

Acquisition Source values are restricted to: **OCR**, **Manual Entry**, **Existing Client Data**, **Case Data**, **Derived/Calculated**, or **"Not yet defined."** These follow the Information Acquisition Paths in `Data Needs.md` §2.7. Where acquisition is not determinable from the sources, "Not yet defined." is used.

---

## 12. Validation Notes Convention

Each clause may carry a Validation Notes block split into four labelled parts (absent parts are omitted):

| Label | Meaning |
|---|---|
| **Source-derived fact** | Something directly evidenced by the source instance(s). |
| **Domain interpretation** | A reading/interpretation offered for domain validation; never asserted as fact. |
| **Legal interpretation** | NEVER asserted as fact. Legal questions are raised as open questions requiring legal review. |
| **Project decision** | A decision recorded in the Decision Log relevant to the clause (e.g., Decisions 005, 007, 008). |

---

## 13. Quality Checklist (per library)

Each clause library runs the following checklist before completion. Items are recorded PASS/FAIL/N-A in the library's quality section.

1. Clause IDs follow the `CLAUSE-<DOMAIN>-###` convention; no duplicate IDs.
2. Every clause is backed by verbatim source text or explicitly marked Draft.
3. Canonical Source Text preserves source spelling; `⟨sic⟩` marks used for corrupt/ambiguous text.
4. Variables are named per §5 and traced to Data Need IDs only where real mappings exist.
5. No invented legal rules, clauses, variables, or requirements were added.
6. No existing requirements document (SRS, FR, NFR, Data Needs, BR, UC) was modified.
7. Applicability recorded; "Not established from supplied sources." used when unknown.
8. Conditions recorded; "Condition requires validation." used when unproven.
9. Variants classified (wording/structural/parameter/conditional); parameter-only differences are not separate clauses.
10. Categories used are source-representative; none invented to force-fit content.
11. Gap vocabulary (§10) used; nothing silently fixed.
12. Source Documents table present with stable IDs.
13. Source→Clause matrix present (universal/common/rare/conditional/unique).
14. Clause→Data traceability matrix present with acquisition sources restricted to the §11.2 vocabulary.
15. Coverage Findings section present (counts, universal vs variant coverage, gaps).
16. Contradictions within the library's sources and against other artifacts flagged, not auto-resolved.
17. Open Questions raised for every ambiguity; IDs `OQ-CL-###`.
18. Legal validation status marked; no legal conclusions asserted.
19. Final report with the 10 required counts delivered at the end of the library.
20. No emojis or decorative content; project markdown conventions followed.
