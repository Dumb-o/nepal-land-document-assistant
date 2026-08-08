# Business Rules — Land-Rent Document Preparation

> **Working Analysis Document** — Business rules derived from the SRS functional requirements (`SRS/SRS.md` §14) and the Land Rent Template Analysis (conditional content §9, calculation patterns §7.2, conditional generation logic §14.2). This document is an intermediate requirements artifact feeding the SRS Gap Analysis and SRS v0.2. It is NOT a finalized specification.

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

## 4. Workflow / State Rules

| ID | Rule | Status | Source |
|---|---|---|---|
| BR-002 | Finalized documents must be distinguishable from drafts. | [PROPOSED] | SRS §14.1 |
| BR-006 | A finalized document may not be modified without creating a new version. | [PROPOSED] | SRS §14.2, FR-028 |
| BR-007 | Source documents should be associated with a case before processing. | [PROPOSED] | SRS §14.2 |
| BR-016 | Document generation may proceed only when Verified Case Data exists (data lifecycle precedes document lifecycle). | [PROPOSED] | SRS §10.1 |
| BR-017 | Document generation must be blocked if mandatory template fields are missing from Verified Case Data. | [PROPOSED] | UC-011 alt flow |
| BR-018 | Draft editing does not alter Verified Case Data. Re-generation reuses Verified Case Data. | [PROPOSED] | SRS §10.2 |

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

---

## 9. Open Questions

| ID | Question |
|---|---|
| OQ-BR-01 | Which conditional clauses are mandatory vs optional in practice? [OQ-TA-01] |
| OQ-BR-02 | What determines the number of witnesses? Is there a legal minimum? [OQ-TA-03, OQ-TA-14] |
| OQ-BR-03 | Are the escalation calculation formulas correct for all agreements, or do variations exist? [OQ-TA-23] |
| OQ-BR-04 | Are there legally mandated minimum/maximum values (rent, duration, notice) to enforce? [OQ-TA-12] |
| OQ-BR-05 | Should any candidate legal rules (BR-008..BR-010) be enforced by the system once verified? [TO BE DETERMINED] |
