# Use Cases — Land-Rent Document Preparation

> **Working Analysis Document** — Use cases derived from the Field Dictionary (`Land Rent Template Analysis.md` §4) and the SRS functional requirements (`SRS/SRS.md` §7). This document is an intermediate requirements artifact feeding the SRS Gap Analysis and SRS v0.2. It is NOT a finalized specification.
>
> **2026-08-08 update:** Reflected product decisions 004–008 (persistent Cases, Case Type classification, Client as a distinct reusable concept, typed documents). New use cases UC-017..UC-021 added; UC-002, UC-003, UC-014 refined. Reflected the information-acquisition clarification (Data Needs §2.7): no source document, OCR, or Client record is required to represent a party or create a case; manual entry (incl. Nepali Unicode) is first-class; OCR output is Candidate Data requiring operator verification; acquisition paths may mix within a case; document generation is source-agnostic and internal provenance is not document content.

| Field | Value |
|---|---|
| **Document Status** | Draft — Initial Analysis Complete |
| **Date** | 2026-08-08 |
| **Derived From** | Field Dictionary (Template Analysis §4) + SRS v0.1 §7 |
| **Primary Actor** | Document Preparation Operator |
| **Secondary Actor** | Administrator |
| **Related SRS** | `SRS/SRS.md` (v0.1.1 — requirements synchronization revision) |
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

| Use Case ID | Use Case Name                         | Actor                   | SRS Trace                               | Field Dictionary Trace                       |
| ----------- | ------------------------------------- | ----------------------- | --------------------------------------- | -------------------------------------------- |
| UC-001      | Authenticate                          | Operator, Administrator | FR-001, FR-002                          | —                                            |
| UC-002      | Create a Case                         | Operator                | FR-004, FR-005, FR-008, FR-035, FR-040  | —                                            |
| UC-003      | View Recent Cases, Case List, and Status | Operator              | FR-006, FR-007, FR-037, FR-038, FR-039  | —                                            |
| UC-004      | Capture / Upload Source Documents     | Operator                | FR-009, FR-010, FR-011, FR-012, FR-012a | Source documents                             |
| UC-005      | Enter Party Information               | Operator                | FR-019                                  | P1_*, P2_* fields                            |
| UC-006      | Enter Property Information            | Operator                | FR-019                                  | PROP_* fields                                |
| UC-007      | Enter Rental and Term Information     | Operator                | FR-019                                  | RENT_*, TERM_*, NOTICE_* fields              |
| UC-008      | Enter Witnesses and Writer            | Operator                | FR-019                                  | WITNESS_*, WRITER_NAME                       |
| UC-009      | Automatically Extract Data (Optional) | System, Operator        | FR-013, FR-014, FR-015, OCR-001..006    | Field mapping (§10 of Template Analysis)     |
| UC-010      | Verify Candidate Data                 | Operator                | FR-016, FR-017, FR-018                  | All candidate fields                         |
| UC-011      | Generate Document Draft               | Operator                | FR-021, FR-023, FR-024, DG-001..003     | Template variable model (§13)                |
| UC-012      | Review and Edit Draft                 | Operator                | FR-025, FR-026                          | —                                            |
| UC-013      | Finalize Document                     | Operator                | FR-027, FR-028, FR-029, FR-030, FR-031  | —                                            |
| UC-014      | Search and Retrieve Past Cases        | Operator                | FR-032, FR-033, FR-038, FR-039          | —                                            |
| UC-015      | Manage Operator Accounts              | Administrator           | FR-003                                  | —                                            |
| UC-016      | Update Document Template              | Administrator           | NFR-010, DG                             | Template structure (§2 of Template Analysis) |
| UC-017      | Create Client                         | Operator                | FR-041                                  | P1_*, P2_* identity fields                   |
| UC-018      | View and Search Clients               | Operator                | FR-042, FR-043                          | P1_*, P2_* identity fields                   |
| UC-019      | Associate Client with a Case          | Operator                | FR-044, FR-045                          | P1_*, P2_* identity fields                   |
| UC-020      | View a Client's Cases                 | Operator                | FR-046                                  | —                                            |
| UC-021      | Manage Client Source Documents        | Operator                | FR-047, FR-048, FR-049                  | Source documents                             |

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

| Field                 | Description                                                                                                                                                                                                                                                                                                                             |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Actors**            | Operator                                                                                                                                                                                                                                                                                                                                 |
| **Precondition**      | Operator authenticated.                                                                                                                                                                                                                                                                                                                  |
| **Main Flow**         | 1. Operator selects "New Case". 2. System prompts the operator to select a **Case Type** (the MVP supports LAND_RENT). 3. System creates a case with a unique identifier and records creation date/time and operator identity. 4. System assigns initial status (Created). 5. Operator proceeds to case data collection (optionally associating a Client — see UC-019). |
| **Alternative Flows** | 3a. No source document or OCR available → not a blocker: case creation succeeds regardless; required information is entered manually (UC-005..UC-008) and verified (UC-010). The case must not depend on a successful OCR pass (BR-049/BR-050). |
| **Postcondition**     | A new case exists with unique ID, Case Type, creation metadata, and status Created. The case persists after finalization and remains retrievable (see UC-003). |
| **SRS Trace**         | FR-004, FR-005, FR-008, FR-035, FR-040                                                                                                                                                                                                                                                                                                   |
| **Validation Needed** | Yes — with domain experts                                                                                                                                                                                                                                                                                                                |

### UC-003 — View Recent Cases, Case List, and Status

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Operator authenticated. |
| **Main Flow** | 1. Operator authenticates. 2. System presents the **Recent Cases** view as the post-authentication landing experience. 3. System displays recently accessed/created cases with current status. 4. Operator may open an existing case (including finalized cases) OR select "New Case" (UC-002). 5. Operator may access the broader case directory to browse all cases, optionally filtering by Case Type or other supported criteria. 6. Operator selects a case to open it. |
| **Alternative Flows** | 3a. No cases exist → system shows an empty state with a "New Case" action. 4a. Filter yields no results → system shows an empty state with a clear "New Case" action. |
| **Postcondition** | Operator has visibility into recent and all cases; finalized cases remain visible and retrievable; the operator can resume work or create a new case. |
| **SRS Trace** | FR-006, FR-007, FR-037, FR-038, FR-039 |
| **Validation Needed** | Yes — lifecycle states, list, and directory needs [TO BE VALIDATED] |

### UC-004 — Capture / Upload Source Documents

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | A case exists. Source documents may be available (physical or digital) — **optional**, not required (BR-049). |
| **Main Flow** | 1. Operator selects a case. 2. Operator captures a document image via device camera OR uploads an existing digital image/PDF. 3. [PROPOSED] Operator reviews the captured image before accepting. 4. Operator labels the document with a document type (e.g., Citizenship Certificate, Lalpurja, Company Registration). 5. System associates the document with the case and records metadata. 6. Operator may repeat for additional documents. |
| **Alternative Flows** | 2a. Capture quality unsatisfactory → operator recaptures or replaces. 2b. No source document supplied → case proceeds without any document; information is entered manually (UC-005..UC-008). |
| **Postcondition** | Source documents associated with the case, typed, and viewable — or the case proceeds with zero source documents. |
| **SRS Trace** | FR-009, FR-010, FR-011, FR-012, FR-012a |
| **Field Trace** | Field-to-source mapping in Template Analysis §10.1 |
| **Validation Needed** | Yes — document type labels require template/workflow validation |

### UC-005 — Enter Party Information

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | A case exists. Party source documents (e.g., citizenship certificates) and/or verbal client information available. Manual entry is a first-class acquisition path — it does not require a source document (BR-048/BR-049). |
| **Main Flow** | 1. Operator selects a party role (First Party / Second Party). 2. Operator enters party identity fields: full name, grandfather's name, father's name, district, municipality, ward, age. 3. Operator enters citizenship details where present: citizenship number, issue date, issue district. 4. [CONDITIONAL] If the Second Party is a company, operator enters company name, registration number, registration date, registrar office, proprietor. 5. [CONDITIONAL] If there are multiple First Party co-owners, operator repeats party entry for each individual. |
| **Alternative Flows** | 2a. Party provides no document → operator enters all values from verbal/written information; the party is still fully represented (BR-049). 2b. Values may be entered in **Nepali Unicode** (Devanagari), e.g. नाम: राम बहादुर थापा; बाबुको नाम: श्याम बहादुर थापा (FR-LR-064). 4a. Party is an individual → skip company fields. |
| **Postcondition** | Party information entered as Candidate Data, pending verification (UC-010). |
| **SRS Trace** | FR-019, FR-LR-064, FR-LR-065 |
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
| **Precondition** | OCR/automated extraction is implemented (subject to Phase 0.8 Technical Research). Source documents captured/uploaded. Extraction is **optional**: a case must remain fully processable without it (BR-050). |
| **Main Flow** | 1. Operator invokes automated extraction on captured source documents. 2. System recognizes text (Devanagari and/or English). 3. System extracts field values mapped to known fields. 4. System presents extracted values as **Candidate Data** (not authoritative) with confidence indicators where feasible. 5. Operator proceeds to verification (UC-010). |
| **Alternative Flows** | 3a. Extraction fails or is unavailable → operator uses manual entry (UC-005 to UC-008). 3b. Extraction produces incorrect values → operator reviews and corrects them during verification (UC-010); the corrected values, not the extraction output, become Verified Case Data. |
| **Postcondition** | Candidate Data produced from automated extraction, pending human verification. |
| **SRS Trace** | FR-013, FR-014, FR-015, OCR-001..OCR-006 |
| **Validation Needed** | Yes — technical feasibility (Phase 0.8); not MVP-mandatory |

### UC-010 — Verify Candidate Data

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Candidate Data exists (from manual entry and/or automated extraction). Candidate Data never bypasses this step — OCR output is not authoritative (BR-050). |
| **Main Flow** | 1. System presents Candidate Data in a structured review interface. 2. Operator views source documents alongside candidate values (where available). 3. Operator confirms each value OR corrects it. 4. System records the operator's confirmation/correction. 5. Upon completion, data becomes Verified Case Data. |
| **Alternative Flows** | 3a. Value missing from sources → operator enters it manually. 3b. OCR value incorrect (e.g., misread name) → operator corrects it; the corrected value is what is used in the document. 3c. Value missing from all sources → operator flags it as unresolved; document generation may be blocked. |
| **Postcondition** | Verified Case Data established; authoritative source for document generation. |
| **SRS Trace** | FR-016, FR-017, FR-018 |
| **Validation Needed** | Yes — with domain experts |

### UC-011 — Generate Document Draft

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Verified Case Data exists. A controlled document template is available. Generation is **source-agnostic**: it uses Verified Case Data regardless of whether each value came from manual entry, a source document, OCR, or a reusable Client (BR-051). |
| **Main Flow** | 1. Operator selects the template for the case. 2. System populates variable fields from Verified Case Data. 3. System applies conditional sections based on case data (e.g., use purpose, company party, multi-party, multi-kitta). 4. System generates a draft document and records template identity, version, and generation timestamp. 5. System presents the draft to the operator. |
| **Alternative Flows** | 2a. Mandatory field missing → system reports the gap and blocks generation until resolved. 2b. Internal provenance (how each value was acquired) is not inserted into the document unless the template requires it (BR-052). |
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
| **Main Flow** | 1. Operator enters search criteria (case ID, party name, client name, Case Type, kitta number, date range — [PROPOSED]). 2. System returns matching cases. 3. Operator opens a case and retrieves its Finalized System Record (or resumes in-progress work). |
| **Postcondition** | Operator has retrieved the desired case/document. |
| **SRS Trace** | FR-032, FR-033, FR-038, FR-039 |
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

### UC-017 — Create Client

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Operator authenticated. Client information available (verbal and/or from source documents). No source document is required to create a Client (BR-049; OQ-UC-10). |
| **Main Flow** | 1. Operator selects "New Client". 2. Operator enters client identity information (full name, grandfather, father, address, citizenship details — reusing the Field Dictionary party fields). 3. [CONDITIONAL] If the client is an organization, operator enters organization details (e.g., company name, registration) where applicable. 4. Operator saves the client record. 5. System stores the client record for reuse across cases. |
| **Alternative Flows** | 2a. No source document → operator enters identity from verbal/written information; record is created with zero source documents. |
| **Postcondition** | A reusable Client record exists, distinct from any Application User account. |
| **SRS Trace** | FR-041 |
| **Field Trace** | DN-P1/DN-P2 identity fields (client identity) |
| **Validation Needed** | Yes — exact Client fields [TO BE VALIDATED] (OQ-UC-07) |

### UC-018 — View and Search Clients

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Client records exist. |
| **Main Flow** | 1. Operator opens the client list/search. 2. Operator searches by name, citizenship number, or other supported criteria [PROPOSED]. 3. System returns matching client records. 4. Operator views a client's information. |
| **Postcondition** | Operator can locate and view client records. |
| **SRS Trace** | FR-042, FR-043 |
| **Validation Needed** | Yes — search criteria [TO BE VALIDATED] |

### UC-019 — Associate Client with a Case

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Operator authenticated. A case exists (or is being created). A client record exists, or client information is available to create one. |
| **Main Flow** | 1. Operator opens a case. 2. Operator selects "Add Client". 3. Operator searches for an existing client (UC-018) OR creates a new client record (UC-017). 4. System associates the selected client with the case. 5. Client information may pre-fill party fields. |
| **Alternative Flows** | 3a. No matching client → operator creates a new client record. 3b. No client record is created/selected → the party is still represented in the case without a Client association (DN-PTY-02 is 0..1); the case proceeds with manual party entry (UC-005). How a person with no Client record and no source document is stored long-term is OQ-UC-10 / OQ-DN-17. |
| **Postcondition** | Client associated with the case (where applicable); the client record remains reusable across other cases. |
| **SRS Trace** | FR-044, FR-045 |
| **Validation Needed** | Yes — with domain experts |

### UC-020 — View a Client's Cases

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | Client records with associated cases exist. |
| **Main Flow** | 1. Operator opens a client record. 2. System lists the cases associated with the client. 3. Operator opens a case to view or resume it. |
| **Postcondition** | Operator can see all cases involving a given client. |
| **SRS Trace** | FR-046 |
| **Validation Needed** | Yes — with domain experts |

### UC-021 — Manage Client Source Documents

| Field | Description |
|---|---|
| **Actors** | Operator |
| **Precondition** | A client record exists. Source documents available (physical or digital) — **optional**: a client may have zero source documents (BR-049). |
| **Main Flow** | 1. Operator opens a client record. 2. Operator associates source documents (e.g., citizenship certificate, Lalpurja) with the client [PROPOSED — source document capture/upload is deferred; association may be metadata-only for the MVP]. 3. System records the association. 4. System keeps Source Documents distinct from Generated Drafts and Finalized Documents. |
| **Alternative Flows** | 2a. No source documents for the client → association is skipped; the client remains fully valid and usable. |
| **Postcondition** | Source documents associated with the client where supported; document types remain distinct. |
| **SRS Trace** | FR-047, FR-048, FR-049 |
| **Field Trace** | Source documents |
| **Validation Needed** | Yes — whether source documents live at the client level, case level, or both is [OPEN QUESTION] (OQ-UC-08) |

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
| OQ-UC-06 | Should a client record be required before case creation, or can a case be created first and a client associated later? [TO BE VALIDATED] |
| OQ-UC-07 | Which fields does a reusable Client record contain beyond the Field Dictionary party fields? No new fields are to be invented without validation. [TO BE VALIDATED] |
| OQ-UC-08 | Should Source Documents be associated at the Client level, the Case level, or both? [OPEN QUESTION] |
| OQ-UC-09 | What rules govern updating a Client's information after a finalized case references it? [OPEN QUESTION] |
| OQ-UC-10 | How is a person with **no reusable Client record and no source document** represented — a Client record with zero source documents, a case-scoped Party without a Client, or another concept? (Mirrors OQ-DN-17.) This must not mean the person cannot be represented. [OPEN QUESTION] |

## 6. Information-Acquisition Workflow Coverage

The eight acquisition workflows required by the information-acquisition clarification (Data Needs §2.7) map onto the use cases above. No new use cases were introduced; the existing ones are refined to cover them.

| # | Workflow | Primary Use Case(s) | Coverage |
|---|---|---|---|
| 1 | Create a case with source documents | UC-002, UC-004 | UC-004 steps 1–6; documents optional but captured when available |
| 2 | Create a case without source documents | UC-002 | UC-002 alt 3a — creation never depends on documents/OCR (BR-049/BR-050) |
| 3 | Enter party information manually | UC-005, UC-017 | Manual entry first-class; Nepali Unicode (FR-LR-064); no document required |
| 4 | Extract data from documents | UC-009 (optional) | OCR output is Candidate Data; not authoritative (BR-050) |
| 5 | Review OCR results | UC-009 → UC-010 | Candidate Data presented for structured verification (FR-LR-019) |
| 6 | Correct OCR results | UC-010 | Operator corrects values; corrected values become Verified Case Data (UC-010 alt 3b) |
| 7 | Complete missing information manually | UC-010 alt 3a | Missing values entered manually and verified |
| 8 | Generate document from verified information | UC-011 | Source-agnostic generation from Verified Case Data (BR-051/BR-052) |

Mixed acquisition (some fields from documents/OCR, others manual) is covered by UC-005/009/010 and FR-LR-065; reuse of existing Client information is covered by UC-017..UC-021 and FR-LR-058/059. A party with no Client record and no source document remains representable (UC-019 alt 3b; OQ-UC-10 / OQ-DN-17).
