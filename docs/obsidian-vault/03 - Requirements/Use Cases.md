# Use Cases — Land-Rent Document Preparation

> **Working Analysis Document** — Use cases derived from the Field Dictionary (`Land Rent Template Analysis.md` §4) and the SRS functional requirements (`SRS/SRS.md` §7). This document is an intermediate requirements artifact feeding the SRS Gap Analysis and SRS v0.2. It is NOT a finalized specification.

| Field | Value |
|---|---|
| **Document Status** | Draft — Initial Analysis Complete |
| **Date** | 2026-08-08 |
| **Derived From** | Field Dictionary (Template Analysis §4) + SRS v0.1 §7 |
| **Primary Actor** | Document Preparation Operator |
| **Secondary Actor** | Administrator |
| **Related SRS** | `SRS/SRS.md` (v0.1 Working Draft) |
| **Related Analysis** | `Land Rent Template Analysis.md` |

---

## 1. Actors

| Actor | Type | Description |
|---|---|---|
| Operator | Primary | Document-preparation professional (notary / deed writer / land-rent specialist) who creates and finalizes land-rent documents. The project owner's parents are the initial operators. |
| Administrator | Secondary | Manages operator accounts and document templates (see SRS FR-003). |
| System | Supporting | Provides capture, storage, extraction (optional), verification support, generation, and record-keeping. |
| Client | Indirect | Provides source documents and verbal information; not a system user. |

---

## 2. Use Case Summary

| Use Case ID | Use Case Name | Actor | SRS Trace | Field Dictionary Trace |
|---|---|---|---|---|
| UC-001 | Authenticate | Operator, Administrator | FR-001, FR-002 | — |
| UC-002 | Create a Case | Operator | FR-004, FR-005, FR-008 | — |
| UC-003 | View Case List and Status | Operator | FR-006, FR-007 | — |
| UC-004 | Capture / Upload Source Documents | Operator | FR-009, FR-010, FR-011, FR-012, FR-012a | Source documents |
| UC-005 | Enter Party Information | Operator | FR-019 | P1_*, P2_* fields |
| UC-006 | Enter Property Information | Operator | FR-019 | PROP_* fields |
| UC-007 | Enter Rental and Term Information | Operator | FR-019 | RENT_*, TERM_*, NOTICE_* fields |
| UC-008 | Enter Witnesses and Writer | Operator | FR-019 | WITNESS_*, WRITER_NAME |
| UC-009 | Automatically Extract Data (Optional) | System, Operator | FR-013, FR-014, FR-015, OCR-001..006 | Field mapping (§10 of Template Analysis) |
| UC-010 | Verify Candidate Data | Operator | FR-016, FR-017, FR-018 | All candidate fields |
| UC-011 | Generate Document Draft | Operator | FR-021, FR-023, FR-024, DG-001..003 | Template variable model (§13) |
| UC-012 | Review and Edit Draft | Operator | FR-025, FR-026 | — |
| UC-013 | Finalize Document | Operator | FR-027, FR-028, FR-029, FR-030, FR-031 | — |
| UC-014 | Search and Retrieve Past Cases | Operator | FR-032, FR-033 | — |
| UC-015 | Manage Operator Accounts | Administrator | FR-003 | — |
| UC-016 | Update Document Template | Administrator | NFR-010, DG | Template structure (§2 of Template Analysis) |

---

## 3. Detailed Use Cases

### UC-001 — Authenticate

| Field | Description |
|---|---|
| **Actors** | Operator, Administrator |
| **Precondition** | User has valid credentials. |
| **Main Flow** | 1. User opens the system. 2. System prompts for authentication. 3. User provides credentials. 4. System validates identity and role. 5. System grants access to role-appropriate functions. |
| **Alternative Flows** | 4a. Invalid credentials → system denies access and shows an error. |
| **Postcondition** | Authenticated user session with role-based permissions established. |
| **SRS Trace** | FR-001, FR-002 |
| **Validation Needed** | Yes — authentication mechanism (PIN/password/biometric) [TO BE DETERMINED] |

### UC-002 — Create a Case

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Operator authenticated. |
| **Main Flow** | 1. Operator selects "New Case". 2. System creates a case with a unique identifier and records creation date/time and operator identity. 3. System assigns initial status (Created). 4. Operator proceeds to case data collection. |
| **Postcondition** | A new case exists with unique ID, creation metadata, and status Created. |
| **SRS Trace** | FR-004, FR-005, FR-008 |
| **Validation Needed** | Yes — with domain experts |

### UC-003 — View Case List and Status

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Operator authenticated. |
| **Main Flow** | 1. Operator opens the case list. 2. System displays all cases with current status. 3. Operator selects a case to open it. |
| **Alternative Flows** | 3a. No cases exist → system shows an empty state with a "New Case" action. |
| **Postcondition** | Operator has visibility into case statuses. |
| **SRS Trace** | FR-006, FR-007 |
| **Validation Needed** | Yes — lifecycle states and list needs [TO BE VALIDATED] |

### UC-004 — Capture / Upload Source Documents

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | A case exists. Source documents are available (physical or digital). |
| **Main Flow** | 1. Operator selects a case. 2. Operator captures a document image via device camera OR uploads an existing digital image/PDF. 3. [PROPOSED] Operator reviews the captured image before accepting. 4. Operator labels the document with a document type (e.g., Citizenship Certificate, Lalpurja, Company Registration). 5. System associates the document with the case and records metadata. 6. Operator may repeat for additional documents. |
| **Alternative Flows** | 2a. Capture quality unsatisfactory → operator recaptures or replaces. |
| **Postcondition** | Source documents associated with the case, typed, and viewable. |
| **SRS Trace** | FR-009, FR-010, FR-011, FR-012, FR-012a |
| **Field Trace** | Field-to-source mapping in Template Analysis §10.1 |
| **Validation Needed** | Yes — document type labels require template/workflow validation |

### UC-005 — Enter Party Information

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | A case exists. Party source documents (e.g., citizenship certificates) and/or verbal client information available. |
| **Main Flow** | 1. Operator selects a party role (First Party / Second Party). 2. Operator enters party identity fields: full name, grandfather's name, father's name, district, municipality, ward, age. 3. Operator enters citizenship details where present: citizenship number, issue date, issue district. 4. [CONDITIONAL] If the Second Party is a company, operator enters company name, registration number, registration date, registrar office, proprietor. 5. [CONDITIONAL] If there are multiple First Party co-owners, operator repeats party entry for each individual. |
| **Alternative Flows** | 4a. Party is an individual → skip company fields. |
| **Postcondition** | Party information entered as Candidate Data. |
| **SRS Trace** | FR-019 |
| **Field Trace** | P1_FULL_NAME … P1_CITIZENSHIP_DIST, P2_FULL_NAME … P2_COMPANY_PROPRIETOR |
| **Validation Needed** | Yes — lineage field requirement and company variant [TO BE VALIDATED] |

### UC-006 — Enter Property Information

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | A case exists. Lalpurja or land record available. |
| **Main Flow** | 1. Operator enters property district (ल.पु.जि.), ward number. 2. Operator enters kitta number(s). 3. Operator enters land area in Ropani-Anna-Paisa-Dam format (क्षेत्रफल). 4. Operator enters land category/registration type if present (e.g., ज.ध. महल, गुठि). 5. Operator selects the use purpose (कृषि / व्यापार व्यवसाय / बसोबास / mixed). |
| **Alternative Flows** | 2a. Multiple kitta numbers → operator enters all (e.g., "५५१ र ६२६"). |
| **Postcondition** | Property information entered as Candidate Data. |
| **SRS Trace** | FR-019 |
| **Field Trace** | PROP_DISTRICT, PROP_WARD, PROP_KITTA_NUM, PROP_AREA, PROP_TYPE_LAND, PROP_USE_PURPOSE |
| **Validation Needed** | Yes — area format and use-purpose list [TO BE VALIDATED] |

### UC-007 — Enter Rental and Term Information

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | A case exists. Rental terms agreed with client (verbal or written). |
| **Main Flow** | 1. Operator enters rent amount (figures). 2. [CALCULATED] System generates rent amount in Nepali words. 3. Operator selects rent period (मासिक / वार्षिक). 4. Operator enters escalation rate, escalation period, escalation method. 5. Operator enters payment timing (e.g., अग्रिम). 6. Operator enters term duration in years. 7. Operator enters notice period. |
| **Postcondition** | Rental and term information entered as Candidate Data; words version generated. |
| **SRS Trace** | FR-019 |
| **Field Trace** | RENT_AMOUNT, RENT_AMOUNT_WORDS, RENT_PERIOD, RENT_ESCALATION_RATE, RENT_ESCALATION_PERIOD, RENT_PAYMENT_TIMING, RENT_ESCALATION_METHOD, TERM_DURATION, NOTICE_PERIOD |
| **Validation Needed** | Yes — calculation patterns [TO BE VALIDATED] (Template Analysis §7.2) |

### UC-008 — Enter Witnesses and Writer

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | A case exists. Witness and writer information available. |
| **Main Flow** | 1. Operator enters witness data (name, address, age) for 1–3 witnesses. 2. [OPTIONAL] Operator enters writer/लेखक name and, if applicable, professional license number. |
| **Postcondition** | Witness and writer information entered as Candidate Data. |
| **SRS Trace** | FR-019 |
| **Field Trace** | WITNESS_1_NAME … WITNESS_3_AGE, WRITER_NAME |
| **Validation Needed** | Yes — witness count and writer requirements [TO BE VALIDATED] |

### UC-009 — Automatically Extract Data (Optional)

| Field | Description |
|---|---|
| **Actors** | System, Operator |
| **Precondition** | OCR/automated extraction is implemented (subject to Phase 0.8 Technical Research). Source documents captured/uploaded. |
| **Main Flow** | 1. Operator invokes automated extraction on captured source documents. 2. System recognizes text (Devanagari and/or English). 3. System extracts field values mapped to known fields. 4. System presents extracted values as Candidate Data with confidence indicators where feasible. 5. Operator proceeds to verification (UC-010). |
| **Alternative Flows** | 3a. Extraction fails or is unavailable → operator uses manual entry (UC-005 to UC-008). |
| **Postcondition** | Candidate Data produced from automated extraction, pending human verification. |
| **SRS Trace** | FR-013, FR-014, FR-015, OCR-001..OCR-006 |
| **Validation Needed** | Yes — technical feasibility (Phase 0.8); not MVP-mandatory |

### UC-010 — Verify Candidate Data

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Candidate Data exists (from manual entry and/or automated extraction). |
| **Main Flow** | 1. System presents Candidate Data in a structured review interface. 2. Operator views source documents alongside candidate values. 3. Operator confirms each value OR corrects it. 4. System records the operator's confirmation/correction. 5. Upon completion, data becomes Verified Case Data. |
| **Alternative Flows** | 3a. Value missing from sources → operator enters it manually. 3b. Value missing from all sources → operator flags it as unresolved; document generation may be blocked. |
| **Postcondition** | Verified Case Data established; authoritative source for document generation. |
| **SRS Trace** | FR-016, FR-017, FR-018 |
| **Validation Needed** | Yes — with domain experts |

### UC-011 — Generate Document Draft

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Verified Case Data exists. A controlled document template is available. |
| **Main Flow** | 1. Operator selects the template for the case. 2. System populates variable fields from Verified Case Data. 3. System applies conditional sections based on case data (e.g., use purpose, company party, multi-party, multi-kitta). 4. System generates a draft document and records template identity, version, and generation timestamp. 5. System presents the draft to the operator. |
| **Alternative Flows** | 2a. Mandatory field missing → system reports the gap and blocks generation until resolved. |
| **Postcondition** | Draft document generated and associated with template version. |
| **SRS Trace** | FR-021, FR-023, FR-024, DG-001, DG-002, DG-003 |
| **Field Trace** | Template variable model (Template Analysis §13) |
| **Validation Needed** | Yes — template structure and conditional logic [TO BE VALIDATED] |

### UC-012 — Review and Edit Draft

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Draft document generated. |
| **Main Flow** | 1. Operator reviews the draft within the system. 2. Operator makes text-level edits as needed. 3. System tracks edits (if applicable). |
| **Postcondition** | Draft updated and ready for finalization. |
| **SRS Trace** | FR-025, FR-026 |
| **Validation Needed** | Yes — extent of editing [TO BE VALIDATED] |

### UC-013 — Finalize Document

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Draft reviewed and approved by the operator. |
| **Main Flow** | 1. Operator performs the finalization action. 2. System transitions the document from Draft to Finalized System Record. 3. System records finalization timestamp, operator identity, and template version. 4. Finalized record becomes non-editable. |
| **Alternative Flows** | 4a. Revision needed after finalization → new version or new case created; original preserved. |
| **Postcondition** | Finalized System Record stored, immutable, and associated with its case. |
| **SRS Trace** | FR-027, FR-028, FR-029, FR-030, FR-031 |
| **Validation Needed** | Yes — with domain experts |

### UC-014 — Search and Retrieve Past Cases

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Past cases exist. |
| **Main Flow** | 1. Operator enters search criteria (case ID, party name, kitta number, date range — [PROPOSED]). 2. System returns matching cases. 3. Operator opens a case and retrieves its Finalized System Record. |
| **Postcondition** | Operator has retrieved the desired case/document. |
| **SRS Trace** | FR-032, FR-033 |
| **Validation Needed** | Yes — search criteria [TO BE VALIDATED] |

### UC-015 — Manage Operator Accounts

| Field | Description |
|---|---|
| **Actors** | Administrator |
| **Precondition** | Administrator authenticated. |
| **Main Flow** | 1. Administrator creates a new operator account. 2. Administrator configures account permissions/role. 3. Administrator may disable an account. |
| **Postcondition** | Operator accounts managed per role-based policy. |
| **SRS Trace** | FR-003 |

### UC-016 — Update Document Template

| Field | Description |
|---|---|
| **Actors** | Administrator |
| **Precondition** | Administrator authenticated. |
| **Main Flow** | 1. Administrator updates the land-rent document template (static text, variable fields, conditional sections). 2. System assigns a new template version. 3. Previously generated documents retain their original template version association. |
| **Postcondition** | New template version available; historical documents unaffected. |
| **SRS Trace** | NFR-010, DG (Template Versioning §12.3) |
| **Field Trace** | Template structure (Template Analysis §2), conditional content (§9) |

---

## 4. Field Dictionary Traceability

Each use case above references the field groups it consumes, mapped to the Field Dictionary IDs in `Land Rent Template Analysis.md` §4.1. Complete field-level mapping is maintained in the **Data Needs** artifact (`Data Needs.md`) and the **Field-to-Source Mapping** table (Template Analysis §10.1).

## 5. Open Questions

| ID | Question |
|---|---|
| OQ-UC-01 | Should case data entry (parties, property, rental terms) be a single combined step or separate steps? Validated with domain experts. |
| OQ-UC-02 | Is automated extraction (UC-009) an MVP requirement or a post-MVP enhancement? [TO BE DETERMINED] — Phase 0.8 research. |
| OQ-UC-03 | Is the draft edit capability (UC-012) needed for MVP, or is review-only sufficient? [TO BE VALIDATED] |
| OQ-UC-04 | Should witnesses and writer entry be required before document generation, or only before finalization? [TO BE VALIDATED] |
| OQ-UC-05 | Does the operator create separate cases per agreement, or can one case span multiple documents? [TO BE VALIDATED] |
