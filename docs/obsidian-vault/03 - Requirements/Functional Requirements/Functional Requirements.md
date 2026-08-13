# Functional Requirements

> **Status:** Working Draft
>
> This document defines the functional requirements for the **Nepal Land Document Assistant — Land-Rent Document Preparation Module** MVP.
>
> These requirements are derived from:
> - **Use Cases** (`03 - Requirements/Use Cases.md`) — primary behavioral source (UC-001..UC-021)
> - **Data Needs** (`03 - Requirements/Data Needs.md`) — field-level data requirements (DN-*)
> - **Business Rules** (`03 - Requirements/Business Rules/Business Rules.md`) — behavioral rules (BR-001..BR-052)
> - **Land Rent Template Analysis** (`02 - Document Analysis/Land Rent Template Analysis.md`) — template structure, conditional content, calculations
> - **Land Rent Field Dictionary** (Template Analysis §4.1) — actual template fields (P1_*, P2_*, PROP_*, RENT_*, WITNESS_*, etc.)
> - **Existing SRS** (`03 - Requirements/SRS/SRS.md`) — legacy FR-001..FR-034, DG-001..003, OCR-001..006, BR-001..013
>
> **Relationship to the SRS:** On 2026-08-08 the SRS was revised as a **requirements-synchronization revision (v0.1.1)** reflecting agreed product decisions (persistent Cases, Case Type, Client concept, typed documents). Legacy SRS requirement IDs are preserved and mapped to the new IDs below (see §2). The SRS remains a working draft and is **not baselined**.

---

## 1. ID Scheme and Conventions

- **Functional requirement IDs:** `FR-LR-###` (LR = Land Rent module).
- **Priority levels:** MUST / SHOULD / COULD / FUTURE.
- **Status levels:** CONFIRMED / PROPOSED / TO BE VALIDATED / OPEN QUESTION.
- **MVP scope:** The MVP is a manual, human-in-the-loop land-rent document preparation workflow. It does **not** include OCR, AI-based extraction, automated document classification, government API integration, automated legal determination, blockchain, complex workflow automation, or advanced analytics. Capabilities that already appear in the project documentation but are outside the MVP are listed in §15 (Future / Deferred Functional Requirements).
- **Terminology:** Consistent with the SRS — "Verified Case Data", "Candidate Data", "Draft", "Finalized Document". The system does not independently determine legal validity.

---

## 2. Mapping from Existing SRS Requirement IDs

The new FR-LR identifiers supersede the legacy SRS FR/DG/OCR identifiers. The mapping is explicit to preserve traceability:

| Legacy SRS ID    | New ID(s)            | Notes                                         |
| ---------------- | -------------------- | --------------------------------------------- |
| FR-001           | FR-LR-001            | Authentication                                |
| FR-002           | FR-LR-002            | Authorization                                 |
| FR-003           | FR-LR-003            | Operator account management                   |
| FR-004           | FR-LR-004            | Create case                                   |
| FR-005           | FR-LR-005            | Unique case identifier                        |
| FR-006           | FR-LR-007            | Case list                                     |
| FR-007           | FR-LR-008            | Case status tracking                          |
| FR-008           | FR-LR-006            | Case creation metadata                        |
| FR-009           | FR-LR-101            | Source document capture — **DEFERRED**        |
| FR-010           | FR-LR-102            | Source document upload — **DEFERRED**         |
| FR-011           | FR-LR-103            | Document type labeling — **DEFERRED**         |
| FR-012           | FR-LR-104            | View source documents — **DEFERRED**          |
| FR-012a          | FR-LR-101            | Capture review/recapture — **DEFERRED**       |
| FR-013           | FR-LR-105, FR-LR-106 | OCR + extraction — **DEFERRED**               |
| FR-014           | FR-LR-107            | Verification of extracted data — **DEFERRED** |
| FR-015           | FR-LR-108            | Confidence indicators — **DEFERRED**          |
| FR-016           | FR-LR-019            | Structured review of case data                |
| FR-017           | FR-LR-110            | Side-by-side source view — **DEFERRED**       |
| FR-018           | FR-LR-020            | Correct case data                             |
| FR-019           | FR-LR-010..FR-LR-016 | Manual data entry                             |
| FR-020           | FR-LR-021, FR-LR-022 | Verified Case Data lifecycle                  |
| FR-021           | FR-LR-023, FR-LR-029 | Template-based generation + template identity |
| FR-022           | FR-LR-028            | Nepali language                               |
| FR-023           | FR-LR-024            | Static + variable template structure          |
| FR-024           | FR-LR-025            | Conditional sections                          |
| FR-025           | FR-LR-032            | Draft review                                  |
| FR-026           | FR-LR-033            | Draft text-level edits                        |
| FR-027           | FR-LR-034            | Explicit finalization                         |
| FR-028           | FR-LR-035, FR-LR-037 | Draft/finalized distinction + immutability    |
| FR-029           | FR-LR-036            | Finalization metadata                         |
| FR-030           | FR-LR-031, FR-LR-038 | Output format + persistence                   |
| FR-031           | FR-LR-039            | Case association                              |
| FR-032           | FR-LR-040            | Retrieval                                     |
| FR-033           | FR-LR-041            | Search criteria                               |
| FR-034           | FR-LR-042            | Audit history                                 |
| DG-001           | FR-LR-023, FR-LR-024 | Template-based generation                     |
| DG-002           | FR-LR-028            | Nepali language                               |
| DG-003           | FR-LR-031            | Printable output format                       |
| OCR-001..OCR-006 | FR-LR-105..FR-LR-108 | OCR-specific — **DEFERRED** |

### New requirements added 2026-08-08 (product decisions 004–008)

The following new FR-LR requirements were added to reflect agreed product decisions. They map to new SRS requirements (FR-035..FR-049) introduced in the SRS v0.1.1 synchronization revision:

| New FR-LR ID | New SRS ID | Product Decision |
|---|---|---|
| FR-LR-049 (Assign Case Type) | FR-035 | Decision 005 |
| FR-LR-050 (Persist Cases After Finalization) | FR-036 | Decision 004 |
| FR-LR-051 (Recent Cases Landing View) | FR-037 | Decision 004 |
| FR-LR-052 (Open Existing Case) | FR-039 | Decision 004 |
| FR-LR-053 (Browse/Organize Cases by Case Type) | FR-038 | Decision 005 |
| FR-LR-054 (Maintain Case Metadata) | FR-040 | Decision 004 |
| FR-LR-055 (Create Client) | FR-041 | Decision 006 |
| FR-LR-056 (View Client) | FR-042 | Decision 006 |
| FR-LR-057 (Search Clients) | FR-043 | Decision 006 |
| FR-LR-058 (Associate Client with Case) | FR-044 | Decision 006 |
| FR-LR-059 (Reuse Client Across Cases) | FR-045 | Decision 006 |
| FR-LR-060 (View Client's Cases) | FR-046 | Decision 006 |
| FR-LR-061 (Manage Client Source Documents) | FR-047 | Decisions 006, 007 |
| FR-LR-062 (Distinguish Document Types) | FR-048 | Decision 007 |
| FR-LR-063 (Only Human-Finalized Documents Are Finalized) | FR-049 | Decisions 007, 008 |

---

## 3. Detailed Functional Requirements

### 3.1 Authentication and Authorization

### FR-LR-001 — Authenticate Operator

**Requirement:**
The system shall require authentication before granting access to system functions and case data.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-001
- Legacy SRS FR-001

**Rationale:**
The system handles sensitive personal and property information. Unauthorized access must be prevented.

**Acceptance Criteria:**
- An unauthenticated user cannot access any case or system function.
- The system validates the operator's identity and role before granting access.
- Invalid credentials result in denied access with an error message.

> Validation needed: authentication mechanism (PIN / password / biometric) is [TO BE DETERMINED].

---

### FR-LR-002 — Enforce Role-Based Access Control

**Requirement:**
The system shall enforce authorization based on the authenticated user's assigned role. The MVP supports at least two roles: Operator and Administrator.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-001
- BR-003
- Legacy SRS FR-002

**Rationale:**
Different responsibilities require different levels of system access. Role-based separation supports the Human Authority Principle.

**Acceptance Criteria:**
- Operator role can create cases, enter/verify data, generate and finalize documents.
- Administrator role can additionally manage operator accounts and templates.
- The system denies any action not permitted for the authenticated role.

> Validation needed: role definitions and permission scope [TO BE VALIDATED] with domain experts.

---

### FR-LR-003 — Manage Operator Accounts

**Requirement:**
The Administrator shall be able to create, disable, and manage operator accounts.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-015
- Legacy SRS FR-003

**Rationale:**
The system must support managing who has access.

**Acceptance Criteria:**
- Administrator can create a new operator account with a role.
- Administrator can disable an operator account so it can no longer authenticate.
- Changes to accounts take effect on subsequent authentication.

---

### 3.2 Case Management

### FR-LR-004 — Create Case

**Requirement:**
The operator shall be able to create a new case for each land-rent document preparation instance. Case creation assigns the case's **Case Type** (see FR-LR-049); the MVP supports LAND_RENT only.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-002
- BR-005, BR-041, BR-049
- DN-CASE-01, DN-CASE-03, DN-CASE-06
- Legacy SRS FR-004

**Rationale:**
Cases provide the organizing structure for all related information and documents. Case classification supports organization and retrieval.

**Acceptance Criteria:**
- An authenticated operator can initiate a new case.
- The operator selects the Case Type (LAND_RENT for the MVP).
- Creating a case does not require any data entry to succeed.
- Creating a case does not require a source document or OCR/extraction to succeed (BR-049/BR-050; §2.7 acquisition paths). A case may be created and populated entirely through manual entry.
- The new case is immediately available for data entry.

---

### FR-LR-005 — Assign Unique Case Identifier

**Requirement:**
Each case shall have a unique identifier for reference and retrieval.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-002
- DN-CASE-01
- Legacy SRS FR-005

**Rationale:**
Unique identification supports case management, retrieval, and audit.

**Acceptance Criteria:**
- Every case has an identifier unique across the system.
- The identifier is assigned automatically at case creation.

---

### FR-LR-006 — Record Case Creation Metadata

**Requirement:**
The system shall record the date and time of case creation and the identity of the creating operator.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-002
- DN-CASE-03
- Legacy SRS FR-008

**Rationale:**
Audit trail requirement.

**Acceptance Criteria:**
- Case creation timestamp is recorded and viewable.
- Creating operator identity is recorded and viewable.

---

### FR-LR-007 — View Case List and Status

**Requirement:**
The operator shall be able to view a list of all cases with their current status.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-003
- DN-CASE-02
- Legacy SRS FR-006

**Rationale:**
Operators need visibility into their active and past cases.

**Acceptance Criteria:**
- The case list shows all cases the operator is authorized to view.
- The list shows each case's current status.
- An empty list is displayed when no cases exist.

---

### FR-LR-008 — Track Case Status Through Lifecycle

**Requirement:**
[PROPOSED] The system shall track the status of each case through its lifecycle (e.g., Created, In Progress, Draft Generated, Under Review, Finalized, Persistent).

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-003
- DN-CASE-02
- Legacy SRS FR-007

**Rationale:**
Status tracking helps operators understand which cases are in progress and what steps remain.

**Acceptance Criteria:**
- Case status is stored and updated as the case progresses.
- Case status is displayed in the case list and case view.

> Validation needed: exact lifecycle states [TO BE VALIDATED] with domain experts.

---

### FR-LR-009 — Record Case Notes

**Requirement:**
The operator shall be able to add and view notes on a case.

**Priority:** COULD

**Status:** PROPOSED

**Source:**
- DN-CASE-05

**Rationale:**
Operators may need to record client-specific information not captured in structured fields.

**Acceptance Criteria:**
- The operator can add a note to a case.
- Existing notes are viewable with the case.
- Notes are not used in document generation unless explicitly required.

---

### FR-LR-049 — Assign Case Type

**Requirement:**
Each case shall be assigned a Case Type at creation. The MVP supports a single Case Type: LAND_RENT. Additional Case Types are future scope.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-002
- BR-041, BR-042
- DN-CTYPE-01, DN-CASE-06
- SRS FR-035 (v0.1.1)

**Rationale:**
Case Type classifies a case and determines its workflow and document requirements (Decision 005). Case Type is distinct from a property's use purpose and from document type.

**Acceptance Criteria:**
- The operator selects a Case Type when creating a case.
- The MVP offers LAND_RENT as the Case Type.
- The selected Case Type is displayed and searchable with the case.

---

### FR-LR-050 — Persist Cases After Finalization

**Requirement:**
Cases shall persist after finalization. Finalized cases and finalized documents are intended to be retained indefinitely for operational use. Exact retention, archival, backup, and deletion policies are [TO BE VALIDATED].

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-003, UC-014
- BR-039, BR-040
- DN-CASE-09, DN-LIFE-06
- SRS FR-036 (v0.1.1)

**Rationale:**
A case and its artifacts must remain available after finalization for operational use (Decision 004). No legal retention period is asserted here.

**Acceptance Criteria:**
- A finalized case remains openable and retrievable after finalization.
- Finalized documents within the case remain retrievable.
- Retention/archival/backup/deletion policy is recorded as [TO BE VALIDATED], not asserted.

---

### FR-LR-051 — Provide Recent Cases Landing View

**Requirement:**
The system shall present a Recent Cases view as the post-authentication landing experience, from which the operator can open an existing case, create a new case, and access the broader case directory.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-003
- SRS FR-037 (v0.1.1)

**Rationale:**
Recent Cases is the primary post-auth experience (Decision 004): open existing or create new.

**Acceptance Criteria:**
- After authentication, the operator lands on a Recent Cases view.
- The view offers "New Case" and "open existing case" actions.
- The operator can navigate to the broader case directory from the landing view.

---

### FR-LR-052 — Open Existing Case

**Requirement:**
The operator shall be able to open an existing case (including finalized cases) to view or resume its contents.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-003, UC-014
- SRS FR-039 (v0.1.1)

**Rationale:**
Operators resume in-progress cases and reference finalized cases (Decision 004).

**Acceptance Criteria:**
- Any case the operator is authorized to view can be opened.
- Finalized cases can be opened and their finalized documents retrieved.
- In-progress cases reopen at their current workflow state.

---

### FR-LR-053 — Browse and Organize Cases by Case Type

**Requirement:**
The system shall allow authorized users to organize, browse, and retrieve cases by Case Type and other supported classification criteria.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-003, UC-014
- BR-041
- SRS FR-038 (v0.1.1)

**Rationale:**
A case directory supports organizing, browsing, and retrieving cases by classification (Decision 005). No specific navigation hierarchy is prescribed by this requirement.

**Acceptance Criteria:**
- Cases can be filtered/grouped by Case Type.
- The operator can browse all cases (broader directory) from the landing view.
- Additional classification criteria are [TO BE VALIDATED] with domain experts.

---

### FR-LR-054 — Maintain Case Metadata

**Requirement:**
The system shall maintain per-case metadata: Case ID, Case Type, Status, Creation date, Last updated, associated Clients, Property, Source Documents, Generated Documents, and Finalized Documents.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-002, UC-003
- DN-CASE-01..09, DN-CLI, DN-PROP, DN-SRC, DN-GEN
- SRS FR-040 (v0.1.1)

**Rationale:**
Complete case metadata supports retrieval, organization, and operational use of persistent cases (Decision 004).

**Acceptance Criteria:**
- Case metadata is recorded and viewable.
- Last-updated is maintained automatically.
- Associated clients, property, source documents, generated drafts, and finalized documents are linked to the case.

---

### 3.3 Manual Data Entry

### FR-LR-010 — Enter Party Information

**Requirement:**
The operator shall be able to manually enter First Party (landowner) and Second Party (tenant) identity information as defined by the Field Dictionary, including full name, grandfather's name, father's name, district, municipality, ward, age, and citizenship details. This is a first-class acquisition path (§2.7 path 3), not a fallback: it must fully support parties who supply no source document (e.g., a tenant who provides information verbally).

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-005
- DN-P1-01..DN-P1-10, DN-P2-01..DN-P2-10
- BR-048, BR-049, BR-051
- Field Dictionary: P1_FULL_NAME..P1_CITIZENSHIP_DIST, P2_FULL_NAME..P2_CITIZENSHIP_DIST
- Legacy SRS FR-019

**Rationale:**
Party identity information is the core variable content of the land-rent preamble. Manual entry is the primary MVP acquisition mechanism. It must not depend on the presence of a source document or on OCR.

**Acceptance Criteria:**
- Operator can enter all individual-party fields defined in DN-P1 and DN-P2.
- Values may be entered in **Nepali Unicode** (Devanagari), e.g. नाम: राम बहादुर थापा; बाबुको नाम: श्याम बहादुर थापा; ठेगाना: ललितपुर महानगरपालिका वडा नं. १५ (FR-LR-064).
- A party with **no source document** can be fully represented by manual entry (BR-049).
- Citizenship fields (number, issue date, issue district) are accepted when present and omittable when absent.
- Entered values are stored as Candidate Data pending verification.

---

### FR-LR-011 — Support Multiple First-Party Co-owners

**Requirement:**
The system shall allow the First Party to consist of multiple individuals (co-owners), with the party information repeated for each co-owner.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-005
- DN-P1 (multiplicity)
- BR-031
- Field Dictionary: multi-party first party (Template Analysis §5.1)

**Rationale:**
Template analysis observed up to three First Party co-owners (Template Analysis §5.1).

**Acceptance Criteria:**
- Operator can add additional First Party individuals to a case.
- Each co-owner's lineage and citizenship fields are captured independently.
- The system can render each co-owner in the preamble and signature area.

---

### FR-LR-012 — Support Company as Second Party

**Requirement:**
The system shall support the Second Party as a company, capturing company name, registration number, registration date, registrar office, and proprietor.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-005
- DN-P2-12..DN-P2-16
- BR-030
- Field Dictionary: P2_COMPANY_NAME..P2_COMPANY_PROPRIETOR

**Rationale:**
Template analysis observed a company as Second Party in one instance (Template Analysis §5.2).

**Acceptance Criteria:**
- Operator can select "company" as the Second Party type.
- Company registration fields are shown when the company type is selected.
- Individual fields are hidden or marked not applicable when company type is selected.

---

### FR-LR-013 — Enter Property Information

**Requirement:**
The operator shall be able to manually enter property information as defined by the Field Dictionary, including property district, ward, kitta number(s), area (Ropani-Anna-Paisa-Dam), land category/registration type, and use purpose.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-006
- DN-PROP-01..DN-PROP-06
- Field Dictionary: PROP_DISTRICT, PROP_WARD, PROP_KITTA_NUM, PROP_AREA, PROP_TYPE_LAND, PROP_USE_PURPOSE
- Legacy SRS FR-019

**Rationale:**
Property description is central to the agreement (Clause 1). The area must support the Ropani-Anna-Paisa-Dam format used by the template.

**Acceptance Criteria:**
- Operator can enter all property fields listed above.
- Area is entered and stored in Ropani-Anna-Paisa-Dam format (०-०-०-०).
- Multiple kitta numbers can be entered for a single property.

---

### FR-LR-014 — Enter Rental and Term Information

**Requirement:**
The operator shall be able to manually enter rental and term information as defined by the Field Dictionary, including rent amount, rent period, escalation rate/period/method, payment timing, term duration, and notice period.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-007
- DN-RENT-01..DN-RENT-09
- Field Dictionary: RENT_*, TERM_DURATION, NOTICE_PERIOD
- Legacy SRS FR-019

**Rationale:**
Rental and term conditions form the financial clauses of the agreement.

**Acceptance Criteria:**
- Operator can enter all rental and term fields listed above.
- Rent period is selected from monthly (मासिक) / annual (वार्षिक).
- Use purpose options include agriculture, business, residence, and mixed where applicable.

---

### FR-LR-015 — Generate Rent Amount in Nepali Words

**Requirement:**
The system shall generate the rent amount in Nepali words (अक्षेरुपिय) from the entered numeric rent amount.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-007, UC-011
- DN-RENT-02
- BR-022
- Field Dictionary: RENT_AMOUNT, RENT_AMOUNT_WORDS
- Legacy SRS FR-019 (CALCULATED field)

**Rationale:**
The template always shows the amount in figures followed by Nepali words (Template Analysis §7.1). The words version is a calculated value.

**Acceptance Criteria:**
- The system produces a Nepali-words rendering of the numeric rent amount.
- The words value is presented for operator verification before finalization.
- The operator can correct the generated words value.

---

### FR-LR-016 — Enter Witness and Writer Information

**Requirement:**
The operator shall be able to enter witness information (1–3 witnesses: name, address, age) and writer/scribe information.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-008
- DN-WIT-01..DN-WIT-09, DN-WRI-01
- BR-034
- Field Dictionary: WITNESS_1..3_*, WRITER_NAME

**Rationale:**
The template includes 1–3 witnesses and a writer identification section.

**Acceptance Criteria:**
- Operator can add between 1 and 3 witnesses with name, address, and age.
- Operator can enter the writer name.
- Witness and writer fields are repeatable/omittable per the template structure.

---

### FR-LR-017 — Distinguish Required vs Optional Fields

**Requirement:**
The system shall distinguish required fields from optional fields for each case, based on the Field Dictionary and any selected variants.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- DN-P1, DN-P2, DN-PROP, DN-RENT (Required column)
- BR-017
- Field Dictionary §4.1 (Required? column)

**Rationale:**
Operators must know which fields are mandatory for a valid document and which are conditional or optional.

**Acceptance Criteria:**
- Required fields are clearly identified in the entry interface.
- The system reports which required fields are still missing when generation is attempted.
- Conditional fields (e.g., company fields) are required only when their condition applies.

---

### FR-LR-018 — Validate Field Values and Formats

**Requirement:**
The system shall validate entered field values against the expected format for the field (e.g., Ropani-Anna-Paisa-Dam area format, BS date format, numeric amounts).

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- DN-PROP-04, DN-RENT-01, DN-DOC-01..04
- BR-019, BR-020
- Field Dictionary §4.1 (Data Type column)

**Rationale:**
Format validation prevents errors that would propagate into generated documents.

**Acceptance Criteria:**
- Area values are checked against the Ropani-Anna-Paisa-Dam format.
- Numeric fields (age, rent, term, notice) reject non-numeric input.
- Date fields accept valid BS dates.
- Invalid values are rejected with a clear message and do not become Verified Case Data.

---

### 3.4 Review and Verification

### FR-LR-019 — Present Case Data for Structured Review

**Requirement:**
The system shall present Candidate Data to the operator in a structured review interface for human verification. The operator must explicitly confirm or correct each data field before it becomes part of Verified Case Data.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-010
- BR-014, BR-016
- DN-LIFE-01, DN-LIFE-02
- Legacy SRS FR-016

**Rationale:**
Human verification is the core human-in-the-loop requirement. No data may be used in document generation before operator confirmation.

**Acceptance Criteria:**
- All Candidate Data fields are presented for review.
- The operator can explicitly confirm a value.
- Only confirmed values are treated as Verified Case Data.
- Unconfirmed values remain Candidate Data and cannot be used in generation.

---

### FR-LR-020 — Correct Case Data During Review

**Requirement:**
The operator shall be able to correct any Candidate Data field during review before it becomes Verified Case Data.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-010
- DN-LIFE-02
- Legacy SRS FR-018

**Rationale:**
The operator must be able to fix inaccuracies before data is used in document generation.

**Acceptance Criteria:**
- Every field in review is editable.
- A corrected value is stored as Candidate Data again or directly as the verified value after operator confirmation.
- The correction history is captured where applicable.

---

### FR-LR-021 — Establish Verified Case Data

**Requirement:**
The system shall maintain Verified Case Data as structured information, separate from source documents and generated documents, and it shall be the authoritative data source for document generation.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-010
- BR-016, BR-018
- DN-LIFE-02
- Legacy SRS FR-020

**Rationale:**
Structured, verified data enables document generation, case retrieval, and reuse.

**Acceptance Criteria:**
- Verified Case Data is stored separately from drafts and finalized documents.
- Document generation reads only Verified Case Data.
- Verification timestamp and verifying operator are recorded.

---

### FR-LR-022 — Record Data Source and Lifecycle State

**Requirement:**
The system shall record the origin of each data value (manual entry, source document, or, in the future, automated extraction; and reuse from existing Client information) and its lifecycle state (Candidate vs Verified).

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- DN-LIFE-01, DN-LIFE-02, DN-PROV
- BR-052
- Legacy SRS FR-020 (§9.7, §9.8)

**Rationale:**
Origin and lifecycle state support auditability and the human-verification principle. Provenance (how each value was acquired) is internal audit/traceability metadata; it is not automatically rendered into the final document content — it appears in the document only if the template actually requires it (BR-052, Data Needs §2.7).

**Acceptance Criteria:**
- Each value is identifiable as Candidate or Verified.
- The origin of each value is recorded where applicable (manual entry, source document, OCR/extraction, existing Client reuse).
- Provenance is available for review/traceability but is not automatically inserted into the generated document (BR-052).
- Whether original Candidate values are retained permanently is [OPEN QUESTION].

---

### 3.5 Document Generation

### FR-LR-023 — Generate Draft from Verified Data and Template

**Requirement:**
The system shall generate a land-rent document draft using Verified Case Data and a controlled land-rent document template.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-011
- BR-016, BR-017, BR-051
- DN-VER, DN-GEN, DN-VAR
- Legacy SRS FR-021, DG-001

**Rationale:**
Template-based document generation is the primary value proposition of the system.

**Acceptance Criteria:**
- Draft generation is available only when Verified Case Data exists.
- The draft is generated from the selected template populated with Verified Case Data.
- Generation is **source-agnostic**: it uses Verified Case Data regardless of whether each value was obtained by manual entry, OCR/extraction, a source document, or reuse from an existing Client record (§2.7; BR-051). No acquisition path is a precondition for generation.
- Draft generation records template identity, template version, and generation timestamp.

---

### FR-LR-024 — Populate Variable Fields

**Requirement:**
The document template shall contain static content (standard clauses) and variable fields (case-specific information), and the system shall populate the variable fields from Verified Case Data.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-011
- Legacy SRS FR-023, DG-001
- Template Variable Model (Template Analysis §13)

**Rationale:**
A template approach separates fixed document structure from case-specific data.

**Acceptance Criteria:**
- Variable fields in the template are filled with the corresponding Verified Case Data values.
- Static content is preserved unchanged.
- Any variable field with no corresponding data is reported rather than silently left blank.

---

### FR-LR-025 — Apply Conditional Sections

**Requirement:**
[PROPOSED] The template may include conditional sections that are included or excluded based on case information (e.g., use purpose, company party, multi-party, multi-kitta).

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-011
- BR-027..BR-033
- Legacy SRS FR-024
- Template Analysis §9, §14.2

**Rationale:**
Different rental situations require different clauses (Template Analysis §9.1).

**Acceptance Criteria:**
- Agriculture use purpose includes agriculture-specific clauses (prohibited crops, soil restoration) per BR-027.
- Business/residence use purpose includes physical-structure clauses per BR-028.
- Company Second Party includes company registration details per BR-030.
- Multi-kitta and multi-party conditions render the appropriate repeated content per BR-031, BR-032.
- Conditional behavior is [TO BE VALIDATED] with domain experts.

---

### FR-LR-026 — Handle Repeated Party and Witness Sections

**Requirement:**
The system shall support repeating party sections (multiple co-owners) and witness sections (1–3 witnesses) in the generated document.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-011
- BR-031, BR-034
- Template Analysis §5.1, §5.3

**Rationale:**
The template renders one signature block per co-owner and one entry per witness.

**Acceptance Criteria:**
- Each First Party co-owner appears in the preamble and signature area.
- Each witness entered appears in the witness section.

---

### FR-LR-027 — Perform Template-Derived Calculations

**Requirement:**
The system shall perform calculations required by the template (rent amount in Nepali words; escalation amounts where applicable) using verified inputs.

**Priority:** SHOULD

**Status:** TO BE VALIDATED

**Source:**
- UC-007, UC-011
- DN-RENT-02
- BR-022, BR-024..BR-026
- Template Analysis §7.2 (calculation patterns)

**Rationale:**
The template implies rent-words generation and escalation formulas. The escalation formulas are [TO BE VALIDATED] with domain experts.

**Acceptance Criteria:**
- Rent words are generated from the verified numeric amount (BR-022).
- If escalation values are generated, the calculation matches the template's implied method.
- All calculated values are presented for operator verification.
- Escalation formulas (BR-024..BR-026) remain [TO BE VALIDATED] before implementation.

---

### FR-LR-028 — Preserve Template Formatting and Nepali Language

**Requirement:**
The generated document shall be in Nepali (Devanagari script) and shall preserve the formatting defined by the template, including Bikram Sambat dates and Ropani-Anna-Paisa-Dam area notation.

**Priority:** MUST

**Status:** TO BE VALIDATED

**Source:**
- UC-011
- BR-019, BR-020
- DN-DOC-01..04
- Legacy SRS FR-022, DG-002
- Template Analysis §8 (dates), §6.2 (area)

**Rationale:**
All template instances are entirely in Nepali with BS dates and R-A-P-D areas.

**Acceptance Criteria:**
- The generated document is rendered in Nepali/Devanagari.
- Dates render in BS format: `इतिसम्बत YYYY महिना MMMM GG गते रोज N`.
- Area renders in Ropani-Anna-Paisa-Dam notation.
- Language and formatting requirements confirmed with domain experts.

---

### FR-LR-029 — Record Template Identity and Version

**Requirement:**
The system shall record, for each generated document, the template identity and template version used at generation time.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-011, UC-016
- DN-DOC-05
- Legacy SRS FR-021 (§12.3 Template Versioning)

**Rationale:**
If a template is updated, previously generated documents must remain associated with the version used at generation time.

**Acceptance Criteria:**
- Each draft records template identity and version.
- Template updates do not change the version recorded on already-generated documents.

---

### FR-LR-030 — Prevent Generation with Incomplete Data

**Requirement:**
The system shall block document generation when required fields for the selected template/variant are missing from Verified Case Data, and shall report the missing fields.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-011 (alternative flow)
- BR-017
- Legacy SRS FR-021

**Rationale:**
Generating a document with missing mandatory fields produces an invalid draft.

**Acceptance Criteria:**
- Generation is blocked when any required field is missing.
- The system identifies which required fields are missing.
- The operator can return to data entry to complete the missing fields.

---

### FR-LR-031 — Generate Output in Printable Format

**Requirement:**
The system shall generate the draft in a format suitable for review and printing.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-011
- Legacy SRS FR-030, DG-003

**Rationale:**
Finalized documents must be available for printing and delivery to clients.

**Acceptance Criteria:**
- The draft is generated in a printable output format.
- The output preserves the template's structure and layout.
- Output format confirmed with domain experts (PDF is proposed, not prescribed).

---

### 3.6 Draft Review and Finalization

### FR-LR-032 — Review Draft Before Finalization

**Requirement:**
The operator shall be able to review the generated document draft within the system before finalization.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-012
- BR-001
- Legacy SRS FR-025

**Rationale:**
Human review of the generated output is a core principle of the workflow.

**Acceptance Criteria:**
- The draft is viewable within the system.
- The draft cannot be finalized without operator review action.

---

### FR-LR-033 — Make Permitted Text-Level Edits to Draft

**Requirement:**
The operator shall be able to make text-level edits to the generated draft where needed.

**Priority:** SHOULD

**Status:** TO BE VALIDATED

**Source:**
- UC-012
- BR-018
- Legacy SRS FR-026

**Rationale:**
The operator may need to adjust formatting, phrasing, or add notes not covered by the template.

**Acceptance Criteria:**
- The operator can edit text in the draft.
- Draft edits do not alter Verified Case Data (BR-018).
- The extent of editing required is [TO BE VALIDATED].

---

### FR-LR-034 — Perform Explicit Finalization

**Requirement:**
The operator shall explicitly perform a finalization action to transition a document from Draft to Finalized Document.

**Priority:** MUST

**Status:** CONFIRMED

**Source:**
- UC-013
- BR-001, BR-004
- Legacy SRS FR-027

**Rationale:**
Finalization is the gate between draft and completed document. It is a deliberate, authorized action.

**Acceptance Criteria:**
- Finalization requires an explicit, deliberate operator action.
- The system confirms the operator's intent to finalize.
- Finalization transitions the document to Finalized Document.

---

### FR-LR-035 — Distinguish Draft from Finalized Document

**Requirement:**
The system shall clearly distinguish Draft documents from Finalized Documents.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-013
- BR-002
- Legacy SRS FR-027, FR-028

**Rationale:**
Finalized documents must be distinguishable from drafts.

**Acceptance Criteria:**
- Drafts and finalized documents are labeled and displayed distinctly.
- Finalized documents cannot be mistaken for drafts in the case view.

---

### FR-LR-036 — Record Finalization Metadata

**Requirement:**
The system shall record the date, time, operator identity, and template version at the time of finalization.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-013
- DN-CASE-04, DN-DOC-06
- Legacy SRS FR-029

**Rationale:**
Audit trail for completed documents.

**Acceptance Criteria:**
- Finalization timestamp is recorded.
- Finalizing operator identity is recorded.
- Template version used is recorded.

---

### FR-LR-037 — Prevent Modification of Finalized Records

**Requirement:**
After finalization, the Finalized Document shall not be directly editable. Any revision must create a new version or a new case, preserving the original finalized record.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-013
- BR-006
- Legacy SRS FR-028

**Rationale:**
Finalized documents must be protected from accidental or unauthorized modification.

**Acceptance Criteria:**
- A finalized record cannot be edited through the draft-editing interface.
- The system does not silently alter finalized records.
- Revision requires an explicit action that preserves the original record.

---

### 3.7 Storage and Retrieval

### FR-LR-038 — Persist Finalized Documents

**Requirement:**
The system shall persistently retain Finalized Documents in a format suitable for printing and delivery.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-013
- DN-LIFE-04
- Legacy SRS FR-030

**Rationale:**
Finalized documents must be available for delivery and record-keeping.

**Acceptance Criteria:**
- Finalized Documents are persisted and survive session restarts.
- Finalized records are retrievable for printing and delivery.

---

### FR-LR-039 — Associate Finalized Document with Case

**Requirement:**
The system shall associate each Finalized Document with its originating case for retrieval.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-013
- Legacy SRS FR-031

**Rationale:**
Case-to-document association enables organized retrieval.

**Acceptance Criteria:**
- Each finalized record references its originating case.
- A case's finalized documents are retrievable from the case.

---

### FR-LR-040 — Retrieve Finalized Documents

**Requirement:**
The operator shall be able to retrieve previously finalized documents associated with a case.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-014
- Legacy SRS FR-032

**Rationale:**
Operators may need to reference or reproduce past documents.

**Acceptance Criteria:**
- The operator can open a past case and view its finalized document(s).
- Finalized documents can be retrieved for viewing/printing.

---

### FR-LR-041 — Search Past Cases

**Requirement:**
[PROPOSED] The operator shall be able to search for past cases using criteria including case ID, party name, property identifier (kitta number), and date range.

**Priority:** SHOULD

**Status:** TO BE VALIDATED

**Source:**
- UC-014
- DN-CASE-01, DN-P1-01, DN-P2-01, DN-PROP-03
- Legacy SRS FR-033

**Rationale:**
These are likely search criteria based on domain research; actual operator needs require validation.

**Acceptance Criteria:**
- Search by case ID returns the matching case.
- Search by party name and kitta number returns matching cases where supported.
- Date-range filtering returns cases created/finalized within the range.
- Search criteria require validation with domain experts.

---

### 3.8 Audit and Template Management

### FR-LR-042 — Maintain Audit History of Significant Events

**Requirement:**
The system shall maintain an Audit History of significant lifecycle events, including case creation, data modification, verification, draft generation, finalization, and access to finalized documents.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-002, UC-010, UC-011, UC-013, UC-014
- DN-LIFE-05
- Legacy SRS FR-034

**Rationale:**
Audit trail supports accountability and troubleshooting.

**Acceptance Criteria:**
- Significant events are recorded with event type, timestamp, and operator identity.
- The audit record references the affected case/document.
- The exact set of audit events is [TO BE VALIDATED] for the MVP.

---

### FR-LR-043 — Support Template Versioning

**Requirement:**
The system shall support updating document templates such that template changes do not require application code changes, and each version is tracked.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-016
- DN-DOC-05
- Legacy SRS NFR-010 (§12.3)

**Rationale:**
Document templates may change due to legal requirements or practice changes. Separating templates from code reduces maintenance burden.

**Acceptance Criteria:**
- Templates can be updated without application code changes.
- Each template change produces a distinct version.
- Generated documents reference the template version used at generation.

---

### 3.9 Error and Exception Behavior

### FR-LR-044 — Report Missing Required Information

**Requirement:**
The system shall report required information that is missing or incomplete, enabling the operator to complete it.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-010 (alternative flow 3b), UC-011 (alternative flow)
- BR-017

**Rationale:**
The operator must know which fields are missing so the case can be completed.

**Acceptance Criteria:**
- Missing required fields are reported at review and/or generation time.
- The operator can navigate to the missing fields to complete them.
- The case can be marked as having unresolved missing information where applicable.

---

### FR-LR-045 — Prevent Finalization of Incomplete or Unreviewed Document

**Requirement:**
The system shall prevent finalization of a draft when required information is missing or the draft has not been reviewed.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-013
- BR-001, BR-017

**Rationale:**
Finalization requires authorized human review; incomplete documents must not be finalized.

**Acceptance Criteria:**
- Finalization is blocked if required fields are missing.
- Finalization is blocked until the operator has reviewed the draft.
- The system explains why finalization is blocked.

---

### FR-LR-046 — Handle Failed Document Generation

**Requirement:**
If document generation fails, the system shall report the failure and preserve the case data so the operator can retry.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-011
- BR-016, BR-017

**Rationale:**
Generation failures should not cause loss of case data or an incorrect draft.

**Acceptance Criteria:**
- A generation failure is reported to the operator with a clear message.
- Verified Case Data is preserved after a failed generation.
- The operator can retry generation.

---

### FR-LR-047 — Handle Failed Storage Operations

**Requirement:**
If a storage operation (e.g., saving a finalized document) fails, the system shall report the failure and not record the operation as successful.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-013
- DN-LIFE-04

**Rationale:**
A failed save must not silently produce a missing or partial record.

**Acceptance Criteria:**
- The operator is informed when a storage operation fails.
- A failed finalization is not presented as finalized.
- The operator can retry the operation.

---

### FR-LR-048 — Deny Access to Unauthorized Case or Document

**Requirement:**
The system shall deny access to a case or document when the requesting user is not authorized.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-014
- BR-003, BR-015
- Legacy SRS FR-002, NFR-001

**Rationale:**
Case data and finalized documents must be accessible only to authorized operators.

**Acceptance Criteria:**
- Unauthorized access attempts are denied.
- The denial is reported without exposing case contents.
- Denied access attempts are recorded in the audit trail where applicable.

---

### 3.10 Client Management

> A **Client** is the person or organization on whose behalf a case is processed — distinct from the **Application User** (operator). Client records are reusable across cases (Decision 006). Client fields reuse the Field Dictionary party identity fields; no new fields are invented without validation.

### FR-LR-055 — Create Client

**Requirement:**
The operator shall be able to create a Client record containing the client's identity information (reusing the Field Dictionary party fields: name, lineage, address, citizenship details; organization details where applicable).

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-017
- BR-043
- DN-CLI-01..DN-CLI-10
- SRS FR-041 (v0.1.1)

**Rationale:**
Clients are reusable domain entities (Decision 006).

**Acceptance Criteria:**
- An authenticated operator can create a client record.
- Client identity fields match the Field Dictionary party fields (no invented fields).
- A client record is stored for reuse across cases.

---

### FR-LR-056 — View Client

**Requirement:**
The operator shall be able to view a Client's stored information.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-018
- BR-037, BR-043
- DN-CLI
- SRS FR-042 (v0.1.1)

**Rationale:**
Operators need to review client information (Decision 006).

**Acceptance Criteria:**
- An authorized operator can open a client record.
- Client records are not exposed to unauthorized users.

---

### FR-LR-057 — Search Clients

**Requirement:**
[PROPOSED] The operator shall be able to search for Client records (e.g., by name, citizenship number, or other supported criteria).

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-018
- DN-CLI-01, DN-CLI-07
- SRS FR-043 (v0.1.1)

**Rationale:**
Locating existing clients enables reuse and avoids duplicate records (Decision 006).

**Acceptance Criteria:**
- Search by name and citizenship number returns matching clients where supported.
- Search criteria are [TO BE VALIDATED] with domain experts.

---

### FR-LR-058 — Associate Client with Case

**Requirement:**
The operator shall be able to associate a Client with a Case. Client information may pre-fill the case's party fields.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-019
- BR-044
- DN-CASE-08
- SRS FR-044 (v0.1.1)

**Rationale:**
A case is processed on behalf of one or more clients (Decision 006).

**Acceptance Criteria:**
- A client can be associated with a case.
- A case can reference one or more clients.
- Associated client information can pre-fill party fields.

---

### FR-LR-059 — Reuse Client Across Cases

**Requirement:**
The operator shall be able to reuse an existing Client record across multiple Cases rather than re-entering client information.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-019
- BR-044
- DN-CLI, DN-CASE-08
- SRS FR-045 (v0.1.1)

**Rationale:**
Client records are reusable (Decision 006); reuse reduces re-entry and inconsistency.

**Acceptance Criteria:**
- An existing client can be selected when creating or editing a case.
- One client can appear in multiple cases.

---

### FR-LR-060 — View a Client's Cases

**Requirement:**
The operator shall be able to view the Cases associated with a given Client.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-020
- DN-CASE-08
- SRS FR-046 (v0.1.1)

**Rationale:**
Operators need to see all cases involving a client (Decision 006).

**Acceptance Criteria:**
- Opening a client record lists the cases associated with it.
- Each listed case can be opened.

---

### FR-LR-061 — Manage Client Source Documents

**Requirement:**
[PROPOSED] The system shall allow Source Documents to be associated with a Client in addition to their Case association. Source document capture/upload itself remains deferred (see FR-LR-101..FR-LR-104); this requirement covers the association model.

**Priority:** SHOULD

**Status:** PROPOSED

**Source:**
- UC-021
- BR-045, BR-046
- DN-SRC-04, DN-SRC-06
- SRS FR-047 (v0.1.1)

**Rationale:**
Source documents are evidence tied to a client and/or a case (Decisions 006, 007). Whether they live at the client level, case level, or both is [OPEN QUESTION].

**Acceptance Criteria:**
- A source document can be associated with a client (where supported).
- Source documents remain distinct from generated drafts and finalized documents.
- Client-level vs case-level storage is resolved by the [OPEN QUESTION] before implementation.

---

### 3.11 Document Types (Source / Draft / Finalized)

### FR-LR-062 — Distinguish Document Types

**Requirement:**
The system shall distinguish Source Documents (supplied/captured), Generated Drafts (produced, not finalized), and Finalized Documents (explicitly finalized by a human) as separate, non-interchangeable document types.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-021, UC-013, UC-011
- BR-045
- DN-GEN-01, DN-SRC
- SRS FR-048 (v0.1.1)

**Rationale:**
The three document types are distinct and not interchangeable (Decision 007).

**Acceptance Criteria:**
- Each document in the system is typed as Source, Draft, or Finalized.
- Document type is displayed and cannot be silently changed.
- Draft and Finalized documents are distinguishable from source documents.

---

### FR-LR-063 — Only Human-Finalized Documents Are Finalized

**Requirement:**
The system shall not present a Source Document or a Generated Draft as a Finalized Document. Only a document explicitly finalized by an authorized human is a Finalized Document, and the system does not imply legal validity.

**Priority:** MUST

**Status:** CONFIRMED

**Source:**
- UC-013, UC-021
- BR-038, BR-047
- DN-GEN-01
- SRS FR-049 (v0.1.1)

**Rationale:**
Finalization is a human decision (Decisions 007, 008; Human Authority Principle).

**Acceptance Criteria:**
- Only explicitly finalized documents are labeled Finalized.
- The system never labels a draft or source document as finalized.
- No system-generated indication of legal validity is presented.

---

### FR-LR-064 — Enter Nepali Unicode Text

**Requirement:**
The system shall support entry and storage of Nepali Unicode (Devanagari) text for all manually entered values (party names, addresses, property details, terms). Example values: नाम: राम बहादुर थापा; बाबुको नाम: श्याम बहादुर थापा; ठेगाना: ललितपुर महानगरपालिका वडा नं. १५.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-005
- BR-048
- Data Needs §2.7 (path 3); FR-LR-028
- Field Dictionary: P1_*, P2_*, PROP_*, RENT_* (all Nepali template fields)

**Rationale:**
All template content and real-world data are in Nepali/Devanagari (FR-LR-028). Manual entry must be able to reproduce that data. This is a functional/data-acquisition requirement; the keyboard/IME mechanism (e.g., Roman-transliteration IME, Unicode layout) is an implementation choice and is not prescribed.

**Acceptance Criteria:**
- Operator can type and store Devanagari values (including Devanagari digits such as १५) in every manually entered field.
- Entered Nepali values round-trip correctly into the generated Nepali document.
- Mixed script is supported (e.g., Nepali names with English numerals where applicable), consistent with template evidence.
- The requirement is satisfied regardless of which keyboard/IME the operator uses.

---

### FR-LR-065 — Support Mixed Acquisition Across a Case

**Requirement:**
The system shall allow a single case to acquire its values through different paths: some fields entered manually, some read from source documents, some (where OCR is available) extracted as Candidate Data, and some pre-filled from existing Client information. No requirement exists that all fields share one acquisition path.

**Priority:** MUST

**Status:** PROPOSED

**Source:**
- UC-005, UC-009, UC-010, UC-017..UC-020
- BR-048..BR-051
- Data Needs §2.7 (path 4), §7.4
- DN-EXT, DN-VER, DN-LIFE-01/02

**Rationale:**
In practice party information arrives through mixed channels (e.g., landlord's name OCR'd from a citizenship certificate, address manually corrected, contact entered manually; tenant entirely manual with no document). Each value must be independently acquirable and verifiable.

**Acceptance Criteria:**
- Each case field can be independently populated by manual entry, source-document reading, OCR Candidate Data (where available), or Client reuse.
- A field's acquisition path does not constrain any other field's path.
- All paths converge on the same Candidate → Review → Verified lifecycle (§2.7; FR-LR-019/020/021).
- Document generation treats all paths equally once values are Verified (FR-LR-023).

---

## 4. MVP Functional Requirements Summary

| Category | FR IDs |
|---|---|
| Authentication and Authorization | FR-LR-001..FR-LR-003 |
| Case Management | FR-LR-004..FR-LR-009, FR-LR-049..FR-LR-054 |
| Manual Data Entry | FR-LR-010..FR-LR-018, FR-LR-064, FR-LR-065 |
| Review and Verification | FR-LR-019..FR-LR-022 |
| Document Generation | FR-LR-023..FR-LR-031 |
| Draft Review and Finalization | FR-LR-032..FR-LR-037 |
| Storage and Retrieval | FR-LR-038..FR-LR-041 |
| Audit and Template Management | FR-LR-042..FR-LR-043 |
| Error and Exception Behavior | FR-LR-044..FR-LR-048 |
| Client Management | FR-LR-055..FR-LR-061 |
| Document Types (Source / Draft / Finalized) | FR-LR-062..FR-LR-063 |

---

## 5. Use Case Traceability

| Use Case | Functional Requirement(s) | Data Need(s) | Business Rule(s) |
|---|---|---|---|
| UC-001 Authenticate | FR-LR-001, FR-LR-002 | — | BR-003 |
| UC-002 Create a Case | FR-LR-004, FR-LR-005, FR-LR-006, FR-LR-049, FR-LR-054 | DN-CASE-01, DN-CASE-03, DN-CASE-06 | BR-005, BR-041, BR-049 |
| UC-003 View Recent Cases, Case List, and Status | FR-LR-007, FR-LR-008, FR-LR-051, FR-LR-052, FR-LR-053 | DN-CASE-02 | BR-039, BR-040 |
| UC-004 Capture/Upload Source Documents | FR-LR-101..FR-LR-104 (DEFERRED) | DN-SRC | BR-007, BR-046 |
| UC-005 Enter Party Information | FR-LR-010, FR-LR-011, FR-LR-012, FR-LR-064, FR-LR-065 | DN-P1, DN-P2 | BR-030, BR-031, BR-048, BR-049, BR-051 |
| UC-006 Enter Property Information | FR-LR-013 | DN-PROP | BR-020 |
| UC-007 Enter Rental and Term Information | FR-LR-014, FR-LR-015 | DN-RENT | BR-022, BR-024..BR-026 |
| UC-008 Enter Witnesses and Writer | FR-LR-016 | DN-WIT, DN-WRI | BR-034 |
| UC-009 Automatically Extract Data | FR-LR-105..FR-LR-108 (DEFERRED), FR-LR-065 | DN-LIFE-01 | BR-014, BR-050 |
| UC-010 Verify Candidate Data | FR-LR-019, FR-LR-020, FR-LR-021, FR-LR-022, FR-LR-044, FR-LR-065 | DN-LIFE-01, DN-LIFE-02 | BR-014, BR-016, BR-050 |
| UC-011 Generate Document Draft | FR-LR-023..FR-LR-031, FR-LR-046 | DN-DOC, DN-RENT-02 | BR-016, BR-017, BR-019..BR-033, BR-051, BR-052 |
| UC-012 Review and Edit Draft | FR-LR-032, FR-LR-033 | — | BR-001, BR-018 |
| UC-013 Finalize Document | FR-LR-034..FR-LR-039, FR-LR-045, FR-LR-047, FR-LR-062, FR-LR-063 | DN-CASE-04, DN-LIFE-04, DN-GEN-01 | BR-001, BR-002, BR-004, BR-006, BR-038, BR-047 |
| UC-014 Search and Retrieve Past Cases | FR-LR-040, FR-LR-041, FR-LR-048, FR-LR-052, FR-LR-053 | DN-CASE-01 | BR-003, BR-015, BR-039, BR-040 |
| UC-015 Manage Operator Accounts | FR-LR-003 | — | — |
| UC-016 Update Document Template | FR-LR-043 | DN-DOC-05 | — |
| UC-017 Create Client | FR-LR-055, FR-LR-065 | DN-CLI | BR-043, BR-049 |
| UC-018 View and Search Clients | FR-LR-056, FR-LR-057 | DN-CLI | BR-037, BR-043 |
| UC-019 Associate Client with a Case | FR-LR-058, FR-LR-059 | DN-CASE-08, DN-CLI | BR-044 |
| UC-020 View a Client's Cases | FR-LR-060 | DN-CASE-08 | BR-044 |
| UC-021 Manage Client Source Documents | FR-LR-061, FR-LR-062, FR-LR-063 | DN-SRC-06, DN-GEN-01 | BR-045, BR-046 |

---

## 6. Traceability Matrix

| FR ID | Use Case | Data Need | Business Rule | Template/Field | Priority | Status |
|---|---|---|---|---|---|---|
| FR-LR-001 | UC-001 | — | BR-003 | — | MUST | PROPOSED |
| FR-LR-002 | UC-001 | — | BR-003 | — | MUST | PROPOSED |
| FR-LR-003 | UC-015 | — | — | — | SHOULD | PROPOSED |
| FR-LR-004 | UC-002 | DN-CASE-01, DN-CASE-03 | BR-005 | — | MUST | PROPOSED |
| FR-LR-005 | UC-002 | DN-CASE-01 | — | — | MUST | PROPOSED |
| FR-LR-006 | UC-002 | DN-CASE-03 | — | — | SHOULD | PROPOSED |
| FR-LR-007 | UC-003 | DN-CASE-02 | — | — | SHOULD | PROPOSED |
| FR-LR-008 | UC-003 | DN-CASE-02 | — | — | SHOULD | PROPOSED |
| FR-LR-009 | — | DN-CASE-05 | — | — | COULD | PROPOSED |
| FR-LR-010 | UC-005 | DN-P1-01..10, DN-P2-01..10 | — | P1_*, P2_* fields | MUST | PROPOSED |
| FR-LR-011 | UC-005 | DN-P1 (multi) | BR-031 | §5.1 multi-party | SHOULD | PROPOSED |
| FR-LR-012 | UC-005 | DN-P2-12..16 | BR-030 | P2_COMPANY_* | SHOULD | PROPOSED |
| FR-LR-013 | UC-006 | DN-PROP-01..06 | BR-020 | PROP_* fields | MUST | PROPOSED |
| FR-LR-014 | UC-007 | DN-RENT-01..09 | — | RENT_*, TERM_DURATION, NOTICE_PERIOD | MUST | PROPOSED |
| FR-LR-015 | UC-007 | DN-RENT-02 | BR-022 | RENT_AMOUNT, RENT_AMOUNT_WORDS | MUST | PROPOSED |
| FR-LR-016 | UC-008 | DN-WIT-01..09, DN-WRI-01 | BR-034 | WITNESS_*, WRITER_NAME | SHOULD | PROPOSED |
| FR-LR-017 | UC-005..08, UC-011 | DN-P1..DN-RENT | BR-017 | §4.1 Required? column | MUST | PROPOSED |
| FR-LR-018 | UC-006, UC-007 | DN-PROP-04, DN-RENT-01, DN-DOC | BR-019, BR-020 | §4.1 Data Type | SHOULD | PROPOSED |
| FR-LR-019 | UC-010 | DN-LIFE-01, DN-LIFE-02 | BR-014, BR-016 | — | MUST | PROPOSED |
| FR-LR-020 | UC-010 | DN-LIFE-02 | — | — | MUST | PROPOSED |
| FR-LR-021 | UC-010 | DN-LIFE-02 | BR-016, BR-018 | — | MUST | PROPOSED |
| FR-LR-022 | UC-010 | DN-LIFE-01, DN-LIFE-02 | — | §11 Field Origin | SHOULD | PROPOSED |
| FR-LR-023 | UC-011 | DN-DOC-05 | BR-016, BR-017 | §13 Variable Model | MUST | PROPOSED |
| FR-LR-024 | UC-011 | DN-P1..DN-RENT | — | §13 Variable Model | MUST | PROPOSED |
| FR-LR-025 | UC-011 | DN-PROP-06, DN-P2-12..16 | BR-027..BR-033 | §9 Conditional Content | SHOULD | PROPOSED |
| FR-LR-026 | UC-011 | DN-P1 (multi), DN-WIT | BR-031, BR-034 | §5.1, §5.3 | SHOULD | PROPOSED |
| FR-LR-027 | UC-007, UC-011 | DN-RENT-02 | BR-022, BR-024..026 | §7.2 Calculations | SHOULD | TO BE VALIDATED |
| FR-LR-028 | UC-011 | DN-DOC-01..04 | BR-019, BR-020 | §8 Dates, §6.2 Area | MUST | TO BE VALIDATED |
| FR-LR-029 | UC-011, UC-016 | DN-DOC-05 | — | §12.3 Versioning | MUST | PROPOSED |
| FR-LR-030 | UC-011 | DN-P1..DN-RENT | BR-017 | — | MUST | PROPOSED |
| FR-LR-031 | UC-011 | DN-LIFE-04 | — | §1.4 Language/Script | MUST | PROPOSED |
| FR-LR-032 | UC-012 | — | BR-001 | — | MUST | PROPOSED |
| FR-LR-033 | UC-012 | — | BR-018 | — | SHOULD | TO BE VALIDATED |
| FR-LR-034 | UC-013 | DN-LIFE-04 | BR-001, BR-004 | — | MUST | CONFIRMED |
| FR-LR-035 | UC-013 | DN-LIFE-04 | BR-002 | — | MUST | PROPOSED |
| FR-LR-036 | UC-013 | DN-CASE-04, DN-DOC-06 | — | — | SHOULD | PROPOSED |
| FR-LR-037 | UC-013 | DN-LIFE-04 | BR-006 | — | MUST | PROPOSED |
| FR-LR-038 | UC-013 | DN-LIFE-04 | — | — | MUST | PROPOSED |
| FR-LR-039 | UC-013 | DN-CASE-01 | — | — | MUST | PROPOSED |
| FR-LR-040 | UC-014 | DN-CASE-01 | BR-003 | — | MUST | PROPOSED |
| FR-LR-041 | UC-014 | DN-CASE-01, DN-P1-01, DN-P2-01, DN-PROP-03 | — | — | SHOULD | TO BE VALIDATED |
| FR-LR-042 | UC-002, UC-010, UC-011, UC-013, UC-014 | DN-LIFE-05 | — | — | SHOULD | PROPOSED |
| FR-LR-043 | UC-016 | DN-DOC-05 | — | §12.3 Versioning | SHOULD | PROPOSED |
| FR-LR-044 | UC-010, UC-011 | DN-P1..DN-RENT | BR-017 | — | MUST | PROPOSED |
| FR-LR-045 | UC-013 | DN-LIFE-04 | BR-001, BR-017 | — | MUST | PROPOSED |
| FR-LR-046 | UC-011 | DN-LIFE-02 | BR-016, BR-017 | — | SHOULD | PROPOSED |
| FR-LR-047 | UC-013 | DN-LIFE-04 | — | — | SHOULD | PROPOSED |
| FR-LR-048 | UC-014 | DN-CASE-01 | BR-003, BR-015 | — | MUST | PROPOSED |
| FR-LR-049 | UC-002 | DN-CTYPE-01, DN-CASE-06 | BR-041, BR-042 | — | MUST | PROPOSED |
| FR-LR-050 | UC-003, UC-014 | DN-CASE-09, DN-LIFE-06 | BR-039, BR-040 | — | MUST | PROPOSED |
| FR-LR-051 | UC-003 | — | — | — | SHOULD | PROPOSED |
| FR-LR-052 | UC-003, UC-014 | DN-CASE-01 | BR-039 | — | MUST | PROPOSED |
| FR-LR-053 | UC-003, UC-014 | DN-CTYPE-01 | BR-041 | — | SHOULD | PROPOSED |
| FR-LR-054 | UC-002, UC-003 | DN-CASE-01..09 | — | — | MUST | PROPOSED |
| FR-LR-055 | UC-017 | DN-CLI-01..10 | BR-043 | P1_*, P2_* identity fields | MUST | PROPOSED |
| FR-LR-056 | UC-018 | DN-CLI | BR-037, BR-043 | — | MUST | PROPOSED |
| FR-LR-057 | UC-018 | DN-CLI-01, DN-CLI-07 | — | — | SHOULD | PROPOSED |
| FR-LR-058 | UC-019 | DN-CASE-08 | BR-044 | — | MUST | PROPOSED |
| FR-LR-059 | UC-019 | DN-CLI, DN-CASE-08 | BR-044 | — | SHOULD | PROPOSED |
| FR-LR-060 | UC-020 | DN-CASE-08 | BR-044 | — | SHOULD | PROPOSED |
| FR-LR-061 | UC-021 | DN-SRC-06 | BR-045, BR-046 | Source documents | SHOULD | PROPOSED |
| FR-LR-062 | UC-013, UC-021 | DN-GEN-01, DN-SRC | BR-045 | — | MUST | PROPOSED |
| FR-LR-063 | UC-013, UC-021 | DN-GEN-01 | BR-038, BR-047 | — | MUST | CONFIRMED |
| FR-LR-064 | UC-005 | DN-P1, DN-P2 | BR-048 | P1_*, P2_* | MUST | PROPOSED |
| FR-LR-065 | UC-005, UC-009, UC-010, UC-017 | DN-P1, DN-P2, DN-PROP, DN-RENT, DN-EXT, DN-VER | BR-048..BR-051 | — | MUST | PROPOSED |

---

## 7. Future / Deferred Functional Requirements

> The following capabilities already appear in the project documentation (SRS v0.1 and/or Template Analysis) but are **deferred** and **not MVP requirements**. Their status is **FUTURE** unless the project later decides otherwise. The MVP must remain fully useful without them. Deferring these capabilities does **not** imply that source documents are required: a case can be created and a document generated entirely from verified manually entered data (BR-049, BR-051, FR-LR-004/023/064/065).

| FR ID | Requirement | Legacy Source | Rationale for Deferral |
|---|---|---|---|
| FR-LR-101 | Source document capture via device camera, including capture review and recapture. | SRS FR-009, FR-012a; UC-004 | MVP core workflow (per task scope §6) does not include digital capture; manual entry is the MVP acquisition mechanism. |
| FR-LR-102 | Upload of existing digital image/PDF source documents. | SRS FR-010; UC-004 | Same as above. |
| FR-LR-103 | Operator-assigned document type labeling for source documents. | SRS FR-011; UC-004 | Depends on source document handling, deferred with capture/upload. |
| FR-LR-104 | Viewing all captured/uploaded source documents for a case. | SRS FR-012; UC-004 | Depends on source document handling. |
| FR-LR-105 | OCR text recognition of printed Nepali (Devanagari) and English text in source documents. | SRS FR-013, OCR-002, OCR-003; UC-009 | Subject to Phase 0.8 Technical Research; MVP does not require OCR. |
| FR-LR-106 | Automated field extraction from recognized text into Candidate Data. | SRS FR-013; UC-009 | Feasibility/accuracy not established; manual entry is the primary path (Decision 009). |
| FR-LR-107 | Presenting extracted data as Candidate Data for human verification. | SRS FR-014, OCR-004 | Applies only if extraction is implemented; the verification principle (FR-LR-019) applies in all cases. |
| FR-LR-108 | Confidence indicators for automatically extracted values. | SRS FR-015; UC-009 | Depends on extraction implementation. |
| FR-LR-109 | Automated document classification. | SRS §7.4 | Only one document type exists in the analyzed template; not needed for MVP. |
| FR-LR-110 | Side-by-side source-document viewing during data verification. | SRS FR-017; UC-010 | Depends on source documents being available in the system (deferred capture/upload). |

> **Note on "automated field suggestions":** This capability was referenced in the task brief but does **not** appear in the project documentation (SRS, Template Analysis, Use Cases, Data Needs, or Business Rules). It is therefore **not listed** as a requirement and is flagged as unsourced — see §7.

---

## 8. Requirement Quality Issues

The following issues were identified during review and are recorded rather than silently rewritten:

### Ambiguous Requirements
| ID | Issue |
|---|---|
| FR-LR-014 | "Notice period" units vary in the template (30 days, 60 days, 3 months, 6 months). The requirement does not resolve the unit model. Flagged [TO BE VALIDATED] via BR-009/OQ-TA-12. |
| FR-LR-025 | The exact set of conditional sections and their triggers is not fully confirmed; depends on domain validation (OQ-TA-01). |

### Duplicate / Overlapping Requirements
| ID | Issue |
|---|---|
| FR-LR-044 vs FR-LR-030 | Both address missing required information (review-time vs generation-time). Kept separate because one is an entry/review behavior and the other a generation gate; consider merging during SRS consolidation. |
| FR-LR-040 vs FR-LR-048 | Both concern access/retrieval authorization. Distinct behaviors (retrieval vs denial) but related; consider consolidation. |
| FR-LR-042 | Overlaps NFR-AUD-01 (auditability). Functional event catalog vs non-functional logging capability; will be reconciled in the SRS pass. |

### Conflicting Requirements / Documentation Conflicts
| ID | Conflict |
|---|---|
| FR-LR-101..104 vs SRS | ~~The SRS marked source document capture/upload (FR-009, FR-010) as **MUST**/PROPOSED while the MVP core workflow (Create → Enter → Review → Generate → Review → Finalize → Store → Retrieve) does not include digital capture.~~ **RESOLVED 2026-08-13 (Decision 009)** — SRS FR-009/FR-010 downgraded to optional supporting capabilities; capture/upload stays outside the MVP core workflow. |
| BR-008 vs template | ~~SRS BR-008 claimed "minimum two witnesses per party"; the template shows 1–3 witnesses total.~~ **RESOLVED 2026-08-13** — rule updated to "minimum one witness per party; name, age, address; citizenship optional" (project owner); still [UNVERIFIED — CANDIDATE DOMAIN RULE] pending legal confirmation. |

### Unsourced Requirements
| ID | Issue |
|---|---|
| FR-LR-009 (Case Notes) | Sourced from DN-CASE-05, which itself is PROPOSED without a template or SRS functional backing. Acceptable for MVP but flagged as weakly sourced. |
| FR-LR-031 (Printable output) | Output format (PDF proposed) is not confirmed with domain experts; marked PROPOSED, [TO BE VALIDATED]. |
| "Automated field suggestions" | Referenced in task brief only; not present in project documentation. **Not included** as a requirement. |

### Requirements Requiring Validation
| ID | Issue |
|---|---|
| FR-LR-027, FR-LR-028, FR-LR-033, FR-LR-041 | Marked TO BE VALIDATED — escalation formulas, language/formatting, draft editing extent, and search criteria all require domain expert confirmation. |
| FR-LR-057 | Client search criteria [TO BE VALIDATED] with domain experts. |
| FR-LR-061 | Client source-document association is PROPOSED; whether source documents are stored at client level, case level, or both is [OPEN QUESTION]. |

### 2026-08-08 Synchronization Notes
| ID | Issue |
|---|---|
| FR-LR-101..104 vs FR-LR-061 | Source document capture/upload remains **DEFERRED**, while FR-LR-061 (client source-document association) is added as a model/association requirement. They do not conflict (association can be metadata-only), but the interplay must be confirmed before implementation. |
| Header note revision | The earlier "SRS is not modified by this task" statement was revised because the SRS was updated on 2026-08-08 as a synchronization revision (v0.1.1), still not baselined. |
| Case Type vs use purpose | FR-LR-049 (Case Type = LAND_RENT) and DN-PROP-06 / BR-027..BR-028 (use purpose = agriculture/business/residence) are distinct concepts; FR-LR-025 and BR-042 state this distinction to prevent conflation. |
| Client vs Application User | FR-LR-055..FR-LR-060 (Client management) are distinct from FR-LR-001..FR-LR-003 (Application User accounts); BR-043 records the distinction. |

### Requirements That May Belong Elsewhere
| ID | Issue |
|---|---|
| FR-LR-018 (validation) | Borderline between functional behavior and NFR (usability of error messages). Kept functional because it specifies observable system behavior; usability messaging is covered by NFR-USE-04. |
| FR-LR-042 (audit) | Partially non-functional; the event catalog is functional, the logging capability is NFR-AUD-01. To be reconciled during SRS consolidation. |

---

*End of Functional Requirements — Working Draft.*
