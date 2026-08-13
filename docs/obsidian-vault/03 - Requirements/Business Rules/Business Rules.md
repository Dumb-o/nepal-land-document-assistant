# Business Rules — Land-Rent Document Preparation

> **Working Analysis Document** — Business rules derived from the SRS functional requirements (`SRS/SRS.md` §14) and the Land Rent Template Analysis (conditional content §9, calculation patterns §7.2, conditional generation logic §14.2). This document is an intermediate requirements artifact feeding the SRS Gap Analysis and SRS v0.2. It is NOT a finalized specification.
>
> **2026-08-08 update:** Reflected product decisions 004–008. Added BR-037..BR-047 for case persistence, case classification, client reuse, client/case relationships, source-document ownership, and the draft/finalized distinction. Added BR-048..BR-052 for information acquisition (no source-document requirement, OCR as non-authoritative candidate data, first-class manual entry, internal provenance). No legal retention periods are invented; retention/archival/backup/deletion policies remain [TO BE VALIDATED].

| Field | Value |
|---|---|
| **Document Status** | Draft — Initial Analysis Complete |
| **Date** | 2026-08-08 |
| **Derived From** | Functional Requirements (SRS §7, §14), Template Analysis (§7.2, §9, §14.2) |
| **Related SRS** | `SRS/SRS.md` (v0.1 Working Draft) §14 |
| **Related Analysis** | `Land Rent Template Analysis.md` |
| **Related Artifacts** | `Use Cases.md`, `Data Needs.md` |

---

## 1. Rule Classification

| Class | Meaning | Status Marker |
|---|---|---|
| **Human Authority** | Rules enforcing the principle that the system assists, never replaces, the professional | [CONFIRMED] — explicit project principle |
| **Access Control** | Rules governing who may do what | [PROPOSED] |
| **Workflow / State** | Rules governing case and document lifecycle transitions | [PROPOSED] / [TO BE VALIDATED] |
| **Template / Format** | Rules derived from the actual template (formatting, calculations, conditional content) | [TEMPLATE-DERIVED] — requires domain validation |
| **Candidate Legal / Domain** | Legally consequential rules requiring authoritative verification | [UNVERIFIED — CANDIDATE DOMAIN RULE] |

---

## 2. Human Authority Rules

| ID | Rule | Status | Source |
|---|---|---|---|
| BR-001 | Human review is required before document finalization. | [CONFIRMED] | SRS §14.1 |
| BR-004 | The operator retains full control over document content and finalization. | [CONFIRMED] | SRS §14.1 |
| BR-014 | Automated extraction output may never be used in final document generation without operator verification. | [CONFIRMED — extension of BR-001] | SRS FR-014, OCR-004 |

## 3. Access Control Rules

| ID | Rule | Status | Source |
|---|---|---|---|
| BR-003 | Only authorized users may access stored case data and finalized documents. | [PROPOSED] | SRS §14.1, FR-002 |
| BR-005 | A case may be created only by an authorized operator. | [PROPOSED] | SRS §14.2 |
| BR-015 | A finalized document may be viewed or downloaded only by authorized operators. | [PROPOSED] | SRS FR-032, NFR-001 |
| BR-037 | Client records and client-associated source documents are accessible only to authorized operators. | [PROPOSED] | Decision 006; SRS FR-041, FR-047; NFR-SEC-001 |

## 4. Workflow / State Rules

| ID | Rule | Status | Source |
|---|---|---|---|
| BR-002 | Finalized documents must be distinguishable from drafts. | [PROPOSED] | SRS §14.1 |
| BR-006 | A finalized document may not be modified without creating a new version. | [PROPOSED] | SRS §14.2, FR-028 |
| BR-007 | Source documents should be associated with a case before processing. | [PROPOSED] | SRS §14.2 |
| BR-016 | Document generation may proceed only when Verified Case Data exists (data lifecycle precedes document lifecycle). | [PROPOSED] | SRS §10.1 |
| BR-017 | Document generation must be blocked if mandatory template fields are missing from Verified Case Data. | [PROPOSED] | UC-011 alt flow |
| BR-018 | Draft editing does not alter Verified Case Data. Re-generation reuses Verified Case Data. | [PROPOSED] | SRS §10.2 |
| BR-038 | A document becomes a Finalized Document only through explicit human finalization; the system never presents a Source Document or Generated Draft as finalized, and does not imply legal validity. | [PROPOSED] | Decisions 007, 008; FR-LR-035, FR-LR-063 |

## 4.1 Product Decision Rules (Case Persistence, Classification, Client, Document Types)

> These rules derive from agreed product decisions (see [[../../00 - Project Control/Decision Log]] #004–008). They are project rules, not legal rules. No legal retention periods are asserted.

| ID | Rule | Status | Source |
|---|---|---|---|
| BR-039 | Cases are persistent and long-lived: a case and its artifacts remain available after finalization. | [PROPOSED] | Decision 004 |
| BR-040 | Finalized cases and finalized documents are intended to be retained indefinitely for operational use. Exact retention, archival, backup, and deletion policies remain [TO BE VALIDATED]; no specific retention period is asserted here. | [PROPOSED] | Decision 004; Open Questions |
| BR-041 | Every case is classified by a Case Type. The MVP supports a single Case Type: LAND_RENT. Additional Case Types are future scope. | [PROPOSED] | Decision 005 |
| BR-042 | Case Type is distinct from a property's use purpose (agricultural/business/residential) and from document type; these concepts must not be conflated. | [PROPOSED] | Decision 005; Field Dictionary PROP_USE_PURPOSE |
| BR-043 | A Client is distinct from an Application User: the Client is the person/organization on whose behalf a case is processed and is not an operator of the system. | [PROPOSED] | Decision 006 |
| BR-044 | A Client may be associated with one or more Cases; Client records are reusable across Cases. | [PROPOSED] | Decision 006 |
| BR-045 | Source Documents are input/evidence; Generated Drafts and Finalized Documents are system outputs. Source Documents, Generated Drafts, and Finalized Documents are distinct and non-interchangeable. | [PROPOSED] | Decision 007 |
| BR-046 | Source Documents may be associated with a Client and/or a Case. Whether they are stored at the client level, case level, or both is [OPEN QUESTION]. | [PROPOSED] | Decision 006, 007; OQ-DN-08 |
| BR-047 | Finalization is a human decision. The application does not determine legal validity and must not imply that a finalized document is legally valid. | [PROPOSED] | Decision 008; Human Authority Principle |

## 4.2 Information Acquisition Rules

> These rules govern how information about a person, organization, property, or terms may be obtained. They reflect the requirement that no source document, OCR, or Client record is ever a mandatory prerequisite for representing a party or creating a case (Data Needs §2.7). No legal rules are invented.

| ID | Rule | Status | Source |
|---|---|---|---|
| BR-048 | A party's physical presence is not required for the system to capture their information: information may be supplied verbally/written (by the party or another) and entered manually by the operator. | [PROPOSED] | Data Needs §2.7; UC-005 |
| BR-049 | The absence of a source document does not prevent a party from being represented in a case or a case from being created; required information may instead be entered manually and verified. "Client has no source document" must never mean "Client cannot be represented." | [PROPOSED] | Data Needs §2.7, §7.4; OQ-DN-17 |
| BR-050 | Automated extraction (OCR) output is Candidate Data, never authoritative. It becomes usable only after operator review/verification (Verified Case Data). OCR is never a prerequisite for case creation or document generation. | [PROPOSED] | SRS OCR-004; Data Needs §2.7, DN-EXT/DN-VER; BR-014 |
| BR-051 | Manually entered information may be used for document generation where permitted, subject to the same verification requirements as document-derived information. | [PROPOSED] | Data Needs §2.7, §7.4; FR-LR-010/021 |
| BR-052 | Internal provenance (how a value was acquired — manual, OCR, document, Client reuse) is audit/traceability metadata and does not automatically appear in the final legal document content; it is rendered only if the template actually requires it. | [PROPOSED] | Data Needs §2.7, DN-PROV |

## 5. Template-Derived Rules

> These rules are derived from the 7 template instances analyzed. They require domain expert validation before implementation. Status: **[TEMPLATE-DERIVED]**.

### 5.1 Format Rules

| ID | Rule | Evidence | Status |
|---|---|---|---|
| BR-019 | Generated documents shall use the Bikram Sambat (BS) calendar with format: `इतिसम्बत YYYY महिना MMMM GG गते रोज N`. | §8.1 — all dates BS; no AD observed | [TEMPLATE-DERIVED] |
| BR-020 | Land area shall be expressed in Ropani-Anna-Paisa-Dam format (०-०-०-०). | §6.2 | [TEMPLATE-DERIVED] |
| BR-021 | Rent amount shall appear in figures followed by Nepali words in parentheses. | §7.1 — "रु ६५,०००/- (अक्षेरुपिय पैसाठी हजार रुपैया)" | [TEMPLATE-DERIVED] |
| BR-022 | Rent words (अक्षेरुपिय) shall be generated automatically from the numeric amount. | §13.1 `rent.amountWords` — CALCULATED | [TEMPLATE-DERIVED] |
| BR-023 | [TO BE VALIDATED] In legal usage, amount in words overrides the figure amount; the system must therefore keep the words value verified and in agreement with the figures. | §12.1 — high-sensitivity field | [TEMPLATE-DERIVED] |

### 5.2 Calculation Rules

| ID | Rule | Evidence | Status |
|---|---|---|---|
| BR-024 | [TO BE VALIDATED] Annual rent = monthly rent × 12, where annual rent is used. | §7.2 — रु ५,५००/मास × १२ = रु ६६,०००/वार्षिक | [TEMPLATE-DERIVED] |
| BR-025 | [TO BE VALIDATED] Escalation increase = current rent × escalation rate, applied per escalation period. | §7.2 — रु ६५,००० × १०% = रु ६,५०० | [TEMPLATE-DERIVED] |
| BR-026 | [TO BE VALIDATED] Escalation may be compound (चक्रवृद्धि): Year N rent = base × (1+rate)^(N−1). | §7.2 — "चक्रवृद्धि" stated explicitly | [TEMPLATE-DERIVED] |

> **Caution:** The exact calculation method may vary by agreement. These formulas require domain expert confirmation ([TO BE VALIDATED] in Template Analysis §7.2).

### 5.3 Conditional Content Rules

| ID | Rule | Evidence | Status |
|---|---|---|---|
| BR-027 | [TO BE VALIDATED] When `usePurpose = agriculture`, include agriculture-specific clauses (prohibited crops, soil restoration). | §9.1, §14.2 | [TEMPLATE-DERIVED] |
| BR-028 | [TO BE VALIDATED] When `usePurpose = business/residence`, include physical-structure construction/handover clauses. | §9.1, §14.2 | [TEMPLATE-DERIVED] |
| BR-029 | When `rentPeriod = monthly`, generate the monthly rent clause; when `rentPeriod = annual`, generate the annual rent clause. | §14.2 | [TEMPLATE-DERIVED] |
| BR-030 | When the Second Party is a company, include company registration details (name, registration no., date, office, proprietor) in the preamble. | §9.1 — one instance | [TEMPLATE-DERIVED] |
| BR-031 | When the First Party has multiple individuals, repeat the preamble lineage entry and signature block for each co-owner. | §5.1 — 3 co-owners observed | [TEMPLATE-DERIVED] |
| BR-032 | When multiple kitta numbers exist, repeat/list each property reference in Clause 1. | §9.1 — "कित्ता न. ५५१ र ६२६" | [TEMPLATE-DERIVED] |
| BR-033 | [TO BE VALIDATED] When the land is Guthi-registered, include the Guthi reference in the property description. | §9.1 — हरिसिद्धि भवानी गुठि | [TEMPLATE-DERIVED] |
| BR-034 | The template supports 1–3 witnesses; witness section is repeatable. | §5.3 | [TEMPLATE-DERIVED] |

### 5.4 Subletting / Expense Obligations (Standard Clauses)

| ID | Rule | Evidence | Status |
|---|---|---|---|
| BR-035 | [TO BE VALIDATED] The template's standard clauses prohibit subletting by the Second Party. | §3.2 — "Prohibition on subletting" in all instances | [TEMPLATE-DERIVED] |
| BR-036 | [TO BE VALIDATED] Specified expenses (rent tax, electricity, water, construction tax, waste management) are assigned to the Second Party as obligations. | §7.3 | [TEMPLATE-DERIVED] |

---

## 6. Candidate Legal / Domain Rules Requiring Authoritative Verification

> These rules are legally consequential and must **not** be implemented as system-enforced rules until verified by a qualified legal professional or authoritative source.

| ID | Candidate Rule | Why Verification Required | Validation Source | Status |
|---|---|---|---|---|
| BR-008 | A minimum of two witnesses per party is required for a valid lease agreement (per Muluki Civil Code Section 386). | Preliminary research; applicability not authoritatively confirmed. Template shows 1–3 witnesses total, not per party. | Nepali legal professional | [UNVERIFIED — CANDIDATE DOMAIN RULE] |
| BR-009 | Written agreement is mandatory when monthly rent exceeds NPR 20,000. | Interpretation/exceptions require verification. Template includes रु ५,५०० (below threshold). | Nepali legal professional | [UNVERIFIED — CANDIDATE DOMAIN RULE] |
| BR-010 | Registration at Land Revenue Office is required when annual rent exceeds NPR 500,000 or lease exceeds 10 years. | Applicability to lease types requires verification. | Nepali legal professional | [UNVERIFIED — CANDIDATE DOMAIN RULE] |

---

## 7. Legal Rules Requiring Authoritative Verification

| ID | Rule | Status |
|---|---|---|
| BR-011 | Legal validity requirements for the generated document. | [OPEN QUESTION] |
| BR-012 | Whether the system-generated document format is acceptable for notarization. | [OPEN QUESTION] |
| BR-013 | Whether the system-generated document format is acceptable for Malpot registration (if applicable). | [OPEN QUESTION] |

---

## 8. Traceability

| Rule | Related Use Case | Related Data Needs | SRS Reference |
|---|---|---|---|
| BR-014 | UC-009, UC-010 | DN-LIFE-01 | FR-014, OCR-004 |
| BR-016 | UC-010, UC-011 | DN-LIFE-02 | §10.1 |
| BR-017 | UC-011 | DN-P1..DN-RENT | FR-021 |
| BR-019 | UC-013, UC-011 | DN-DOC-01..04 | FR-022 (language), DG-002 |
| BR-020 | UC-006 | DN-PROP-04 | §9.3 |
| BR-021, BR-022 | UC-007, UC-011 | DN-RENT-01, DN-RENT-02 | §9.5 |
| BR-024..BR-026 | UC-007, UC-011 | DN-RENT-04..07 | §9.5 |
| BR-027..BR-033 | UC-011 | DN-PROP-06, DN-P2-12..16, DN-P1 (multi) | FR-024 |
| BR-034 | UC-008 | DN-WIT-01..09 | §9.4 |
| BR-037 | UC-017, UC-018, UC-021 | DN-CLI, DN-SRC-06 | FR-041, FR-047 |
| BR-038 | UC-013, UC-021 | DN-GEN-01 | FR-027, FR-048, FR-049 |
| BR-039, BR-040 | UC-002, UC-003, UC-014 | DN-CASE-09, DN-LIFE-06 | FR-036 |
| BR-041, BR-042 | UC-002, UC-003, UC-014 | DN-CTYPE-01..03, DN-CASE-06 | FR-035 |
| BR-043, BR-044 | UC-017, UC-019 | DN-CLI | FR-041, FR-044, FR-045 |
| BR-045 | UC-021, UC-013, UC-011 | DN-GEN-01, DN-SRC | FR-048, FR-049 |
| BR-046 | UC-021, UC-004 | DN-SRC-04, DN-SRC-06 | FR-047 |
| BR-047 | UC-013 | DN-GEN-01 | FR-049, §2.5 |
| BR-048, BR-049 | UC-002, UC-005 | DN-PTY, DN-P1, DN-P2 | Data Needs §2.7; OQ-DN-17 |
| BR-050 | UC-009, UC-010 | DN-EXT, DN-VER, DN-LIFE-01 | OCR-004; FR-LR-019/020 |
| BR-051 | UC-005, UC-011 | DN-P1, DN-P2, DN-RENT | FR-LR-010, FR-LR-021 |
| BR-052 | UC-011 | DN-PROV | Data Needs §2.7 |

---

## 9. Open Questions

| ID | Question |
|---|---|
| OQ-BR-01 | Which conditional clauses are mandatory vs optional in practice? [OQ-TA-01] |
| OQ-BR-02 | What determines the number of witnesses? Is there a legal minimum? [OQ-TA-03, OQ-TA-14] |
| OQ-BR-03 | Are the escalation calculation formulas correct for all agreements, or do variations exist? [OQ-TA-23] |
| OQ-BR-04 | Are there legally mandated minimum/maximum values (rent, duration, notice) to enforce? [OQ-TA-12] |
| OQ-BR-05 | Should any candidate legal rules (BR-008..BR-010) be enforced by the system once verified? [TO BE DETERMINED] |
| OQ-BR-06 | What is the exact retention, archival, backup, and deletion policy for finalized Cases and finalized documents? Finalized cases are intended to be retained indefinitely for operational use. [TO BE VALIDATED] |
| OQ-BR-07 | Should Source Documents be stored/associated at the Client level, the Case level, or both? [OPEN QUESTION] |
| OQ-BR-09 | How is a person with no reusable Client record and no source document represented — Client record with zero documents, case-scoped Party without Client, or another concept? [OQ-DN-17] |
| OQ-BR-08 | What rules govern updating a Client's information after a Case has been finalized? [OPEN QUESTION] |
