# Software Requirements Specification

## Nepal Land Document Assistant — Land-Rent Document Preparation Module

> **SRS v0.1.1 is a working requirements hypothesis and discovery document.** It provides an initial structure for requirements engineering but is not yet a validated or baselined specification. Requirements will evolve through domain expert validation, land-rent template analysis, source-document analysis, domain research, legal/regulatory verification, and technical feasibility research.
>
> **2026-08-08 — Requirements Synchronization Revision (v0.1.1):** This revision reflects agreed product decisions (persistent Cases, Case Type classification, Client as a distinct reusable concept, typed Source/Generated/Finalized documents, human authority, Land Rent stays the MVP). It is a synchronization update, **not a rewrite**: existing content, IDs, and structure are preserved. The document remains a working draft and is **not baselined**.

---

## 1. Document Control

| Field | Value |
|---|---|
| Document Title | Software Requirements Specification — Land-Rent Document Preparation Module |
| Project Name | Nepal Land Document Assistant |
| Version | 0.1.1 |
| Status | Working Draft |
| Date | 2026-08-08 |
| Author | Project Team |
| Document Purpose | To define the initial functional and non-functional requirements for the land-rent document preparation module. This is a working draft and has not been baselined. |

### Revision History

| Version | Date | Author | Description |
|---|---|---|---|
| 0.1 | 2026-07-27 | Project Team | Initial working draft |
| 0.1.1 | 2026-08-08 | Project Team | Requirements synchronization revision reflecting product decisions: persistent Cases, Case Type classification (MVP: LAND_RENT), Client as a distinct reusable concept, distinct Source / Generated Draft / Finalized document types, human authority. Not baselined. |

---

## 2. Introduction

### 2.1 Purpose

This Software Requirements Specification (SRS) describes the functional and non-functional requirements for the Nepal Land Document Assistant, focusing on the initial use case: **automated preparation of land-rent documents**.

> [TO BE VALIDATED] The terms "land rent" and "land lease" may refer to legally distinct arrangements under Nepali law. This document uses "land-rent document" as a neutral descriptor until the applicable legal terminology is confirmed. The equivalence of these terms should not be assumed.

The document is intended to:

- Define the scope of the initial release (MVP).
- Specify the system's behavior from the perspective of its users.
- Provide a basis for system design, development, and testing.
- Capture unresolved questions requiring further research and validation.

This is version 0.1.1 — a working draft updated as a requirements-synchronization revision. Requirements marked [PROPOSED], [TO BE VALIDATED], or [OPEN QUESTION] are not confirmed and require further investigation before the SRS can be baselined.

### 2.2 Intended Audience

| Audience | Relationship |
|---|---|
| Project Owner | Decision-maker; primary validator of requirements |
| Primary Domain Experts (including the project owner's parents, who are document-preparation professionals) | Primary sources of domain knowledge; their real-world workflow will be used to validate requirements; they are also intended initial users of the system |
| Developers | Will use the SRS as input to system design and implementation |
| Software Architects | Will use the SRS to inform architecture and design decisions |
| Testers | Will use the SRS to derive test cases |
| Other Document-Preparation Professionals | Future reviewers and potential end users |
| Future Stakeholders | May refer to this document for project understanding |

**Primary Intended Users:** Professionals who currently prepare land-related documents and whose real-world workflows will be used to validate system requirements. The project owner's parents are primary domain experts and initial intended users.

**Direct System Users (MVP):** Document preparation operators (see Section 5.1).

**Indirect Stakeholders:** Clients whose information is processed through the system, and other parties who are not direct system users.

> Note: Not all document-preparation professionals work identically. The workflows of the primary domain experts will inform initial requirements, but the system should accommodate variation.

### 2.3 Product Scope

**Primary Scope (MVP):**

The system shall assist authorized document-preparation professionals in the automated preparation of land-rent documents for property in Nepal. The system will:

1. Allow an operator to create and manage **persistent, classified cases** (Case Type; MVP: LAND_RENT), including viewing Recent Cases after authentication, opening existing cases, and accessing a broader case directory.
2. Manage reusable **Client** records (create, view, search, associate with cases, reuse) — a Client is distinct from the Application User.
3. Accept source documents via capture or upload.
4. Support information acquisition from source documents, which may include manual data entry and/or automated information extraction (automated extraction is subject to technical feasibility research).
5. Maintain structured, verified case information.
6. Generate a land-rent document using a controlled template.
7. Support document review and finalization, distinguishing **Source Documents**, **Generated Drafts**, and **Finalized Documents**.
8. Store finalized documents and finalized cases persistently, intended to be retained indefinitely for operational use (exact retention/archival/backup/deletion policies [TO BE VALIDATED]), with appropriate access control.

**Future Potential Scope:**

- Land sale / trade document preparation
- Land transfer document preparation
- Additional document types and templates
- Additional automation features
- Multi-user collaboration features

**Out of Scope (MVP and currently foreseeable future):**

- Interaction with government land-registration systems
- Automatic submission of documents to government offices
- Legal validation or guarantee of document legal validity
- Provision of legal advice
- Automatic ownership verification
- Replacement of professional judgment
- Replacement of government processes

### 2.4 Product Vision

The Nepal Land Document Assistant aims to improve the efficiency, accuracy, and consistency of land-document preparation in Nepal by providing a structured, human-in-the-loop document automation platform. The system is designed to assist — not replace — the professionals who currently prepare these documents manually.

[PROPOSED] The initial focus is on reducing repetitive manual work in land-rent document preparation while maintaining the operator's full control over content and finalization.

### 2.5 Human Authority Principle

The system operates under the following principle:

- The system assists professionals with information processing and document preparation.
- The system does not independently determine legal validity.
- The system does not make legal decisions.
- The system does not replace professional judgment.
- An authorized human must review information before finalization.
- The system does not independently finalize legally consequential documents.

This principle does not guarantee legal validity. It defines the intended relationship between the system and its human operators. This principle is referenced where relevant throughout the document.

### 2.6 Definitions, Acronyms, and Terminology

| Term | Definition |
|---|---|
| Application User | A person who operates the system (e.g., a document-preparation operator or administrator). An Application User is distinct from a **Client**. |
| Client | The person or organization on whose behalf a case is processed (e.g., a landowner or tenant in a land-rent case). A Client is not an Application User and does not necessarily log in to the system. A Client's information may be reused across one or more Cases. |
| Case | A long-lived, self-contained matter (e.g., a land-rent document preparation instance) comprising source documents, acquired data, verified data, drafts, and the finalized document. A Case persists after finalization and is classified by a Case Type. |
| Case Type | The classification of a Case that determines its workflow and document requirements. The MVP supports a single Case Type: LAND_RENT. Future Case Types are possible but out of scope for the MVP. A Case Type is distinct from a property's **use purpose** (agriculture, business, residence, mixed) and from document type. |
| Operator | The authorized professional who uses the system to prepare documents |
| Source Document | A physical or digital document provided by the client that serves as input to the document preparation process (e.g., citizenship certificate, Lalpurja) |
| Candidate Data | Data that has been acquired (via automated extraction, manual entry, or import) but has not yet been verified by the operator |
| Verified Case Data | Data that has been reviewed, corrected (if needed), and explicitly confirmed by the operator |
| Draft | A preliminary version of the generated document pending final review (a **Generated Draft**) |
| Finalized Document | The completed document explicitly finalized by an authorized operator for delivery to the client. Finalization is a human decision; the application does not determine legal validity |
| Generated Draft | A document produced by the system (or operator) from Case and Client information that has not yet been finalized |
| Land-Rent Document | A document establishing the terms of a land or property rental/lease agreement |
| Human-in-the-Loop | A workflow design where automated processes produce outputs that require human review before they are considered final |
| MVP | Minimum Viable Product — the smallest functional release that delivers value |
| OCR | Optical Character Recognition — proposed technology for extracting text from images |

> Terms requiring domain verification: **Land-Rent Document** — the exact Nepali legal terminology and required content for this document type is [TO BE VALIDATED].

### 2.7 References

| Document | Source | Relationship |
|---|---|---|
| Domain Overview — Nepali Land Documentation | `01 - Domain Research/Domain Overview.md` | Domain research foundation for requirements |
| Domain Expert Interview — Land Rent | `01 - Domain Research/Domain Expert Interview - Land Rent.md` | Proposed interview instrument for workflow validation |
| Project Roadmap | `00 - Project Control/Project Roadmap.md` | Overall project plan and phase definitions |
| Project Overview | `00 - Project Control/Project Overview.md` | High-level project description |

---

## 3. Product Overview

### 3.1 Product Perspective

The proposed system is a **document automation tool** intended to augment the existing manual document-preparation workflow.

> **Evidence levels:** The initial requirements are based primarily on the project owner's product vision, available project research, and preliminary domain understanding. The actual workflow of the initial target users has not yet been formally validated. The following distinctions apply throughout this document:
>
> - **Directly Known Project Facts:** Explicitly confirmed by the project owner or derived from authoritative project decisions.
> - **Domain Hypotheses / Assumptions:** Reasonable inferences based on the project owner's domain familiarity but not formally validated.
> - **General Domain Claims Requiring External Validation:** Statements about how notaries, deed writers, lawyers, or other professionals in Nepal work that require confirmation from domain experts or external research.

[ASSUMPTION] Currently, land-rent documents in Nepal are typically prepared manually by notaries, deed writers (lekhandas), lawyers, or the parties themselves. The process involves examining source documents, extracting relevant information, and typing or writing the agreement using word-processing software or by hand.

The proposed system seeks to provide a structured digital workflow for this process, with potential automation at the information-acquisition and document-generation stages.

### 3.2 Hypothesized As-Is Workflow

> **This section describes a hypothesized workflow that has not yet been formally validated.** It is based on the current understanding of the project, available domain research, and the project owner's domain familiarity. It must be validated with the primary domain experts before being treated as an authoritative description of the existing process.

[TO BE VALIDATED — requires domain expert interview]

1. Client approaches a document-preparation professional requesting a land-rent agreement.
2. Professional asks the client for required information and supporting documents.
3. Client provides source documents.
4. Professional reviews source documents and extracts key information.
5. Professional drafts the agreement using a word processor or template.
6. Professional reviews the draft for accuracy.
7. [ASSUMPTION] Client reviews the draft, may request changes.
8. [ASSUMPTION] Final version is printed and signed by parties and witnesses.
9. [ASSUMPTION] Copy is retained by the professional; original is given to the client.

[ASSUMPTION] The extent of digital tool usage in this workflow is unknown and [TO BE VALIDATED].

The specific source documents required, the sequence of signing, and the retention practices are [TO BE VALIDATED] and should not be assumed to be universal.

### 3.3 Validated As-Is Workflow

*This section is reserved for the validated workflow after domain expert interviews and will be populated when available.*

### 3.4 Proposed System Concept

> **Note:** Sections 3.2 and 3.3 cover the existing (hypothesized) workflow. This section describes the proposed future system concept.

The following conceptual workflow is [PROPOSED] and requires validation with domain experts:

```
Authentication
    ↓
Recent Cases / Home (post-auth landing experience)
    ├── Open an existing Case (in-progress or finalized)
    └── Create a new Case (assign Case Type; MVP: LAND_RENT)
                ↓
Source Documents (client-provided, associated with Client and/or Case)
    ↓
Capture / Upload (via camera or file) — optional supporting capability
    ↓
Manual Data Entry (primary information-acquisition mechanism)
    ├── [FUTURE ENHANCEMENT] Automated Information Extraction (subject to technical research;
    │    may use OCR or other technologies; not part of the MVP — Decision 009)
    ↓
Candidate Data (presented to operator)
    ↓
Human Verification and Correction (operator reviews and corrects)
    ↓
Verified Case Data
    ↓
[TEMPLATE-BASED] Document Generation
    ↓
Draft Document (Generated Draft)
    ↓
Human Review (operator reviews generated document)
    ↓
Operator Finalization
    ↓
Finalized Document
    ↓
Persistent Storage (Case and finalized documents retained indefinitely for
                    operational use; retention/archival/backup/deletion
                    policies [TO BE VALIDATED])
```

**Post-authentication experience:** Recent Cases is the primary landing view after authentication (Decision 004). The operator can open an existing case (including finalized cases) or create a new one, and can access a broader case directory organized by Case Type and other supported classification criteria (see FR-037, FR-038).

**Clients:** A Case is processed on behalf of one or more Clients. Client records are reusable across Cases and are distinct from Application User accounts (Decision 006; see Section 7.15).

**Case Type:** Every Case is classified by a Case Type. The MVP supports a single Case Type — LAND_RENT. Case Type is distinct from a property's use purpose (Decision 005; see FR-035).

Source document capture/upload is an **optional supporting capability**: a case can be created and populated entirely through manual entry without any source document. Automated information extraction (which may use OCR or other technologies) is a **future enhancement** — not part of the MVP — but is required before full deployment (Decision 009).

[RESOLVED — Decision 009] Manual data entry is the **primary information-acquisition mechanism** for the initial release. Automated extraction (OCR or other technologies) is a future enhancement whose feasibility is subject to Technical Research (Phase 0.8) and domain expert feedback.

### 3.5 Product Boundaries

| Within Scope (MVP) | Outside Scope |
|---|---|
| Assist in preparing land-rent documents | Perform official government land registration |
| Extract and manage structured case information | Submit documents to government systems |
| Generate documents from templates | Provide legal advice |
| Support human review and correction | Guarantee legal validity of documents |
| Store finalized documents | Replace qualified legal professionals |
| Track case history and final documents | Automatically verify property ownership |
| Provide access control for authorized operators | Make legal decisions without human review |
| Process information from source documents | Independently determine whether a source document is legally authentic, genuine, or valid |

> **Document authenticity clarification:** The system may process information from a source document (e.g., extract text from a Lalpurja image), but this does not mean the system has verified the document's authenticity or legal validity. Extracting information from a document is distinct from:
> - **Verifying information** (confirming extracted data is correct)
> - **Verifying document authenticity** (confirming a document is genuine and not forged)
> - **Verifying legal validity** (confirming a document meets legal requirements)
>
> The system is not designed to detect forged documents unless such functionality is explicitly researched, validated, and integrated.

---

## 4. Stakeholders

> **Stakeholder ≠ System User.** A stakeholder may have an interest in the system without having an account or directly interacting with it. For example, a client/property owner is an indirect stakeholder whose information is processed but who may never use the system directly.

### 4.1 Project Owner

| Attribute | Description |
|---|---|
| Role | Funds and directs the project; primary decision-maker |
| Relationship | Decision-maker |
| Influence | High |

### 4.2 Primary Domain Experts and Primary Intended Users

| Attribute | Description |
|---|---|
| Role | Professionals who currently prepare land-related documents. The project owner's parents are primary domain experts and initial intended users. Their real-world workflow will inform requirements validation. |
| Relationship | Direct system users (Document Preparation Operators — see Section 5.1) |
| Stakeholder Type | Direct user |
| Influence | High |

### 4.3 Potential Future Users

| Stakeholder | Potential Role | Relationship | Influence |
|---|---|---|---|
| Other Document-Preparation Professionals | May use the system if adopted beyond the initial context | Potential direct user | Medium |
| Office Staff | May assist with data entry or document management | Potential direct user (future) | Medium |
| System Administrator | Manages user accounts and system configuration | Direct user | Medium |

### 4.4 Indirect Stakeholders

| Stakeholder | Interest | Relationship |
|---|---|---|
| Client (Property Owner / Lessor) | Provides source documents; receives the finalized agreement | Indirect stakeholder — not a system user |
| Tenant / Lessee | Accurate reflection of agreed terms in the document | Indirect stakeholder — not a system user |
| Witnesses | May sign the final document | Indirect stakeholder — not a system user |

### 4.5 External Reviewers and Authorities

| Stakeholder | Interest | Relationship |
|---|---|---|
| Domain Experts (beyond primary experts) | Validate requirements and domain assumptions | External reviewer |
| Legal Professionals | May review documents prepared using the system for legal soundness | Indirect potential reviewer |
| Land Revenue Office (Malpot) | May receive certain lease registrations for high-value/long-term leases | External authority |

---

## 5. User Classes and Characteristics

### 5.1 MVP User Classes

The MVP defines two primary user classes:

#### 5.1.1 Document Preparation Operator

| Attribute | Description |
|---|---|
| Description | The primary system user. A professional (notary, deed writer, document preparation professional) who uses the system to prepare land-rent documents for clients. The project owner's parents are the initial operators whose workflow will inform requirements validation. |
| Technical Skill | [ASSUMPTION] Varies; may be comfortable with basic mobile apps and document workflows |
| Domain Knowledge | [ASSUMPTION] Familiar with land-rent document requirements and terminology |
| Primary Tasks | Create cases, capture/upload source documents, acquire information (manually or with system assistance), verify information, generate documents, review drafts, finalize documents |
| Frequency of Use | [TO BE VALIDATED] Likely daily or multiple times per week |
| Devices | [PROPOSED] Mobile tablet or smartphone; potentially desktop/laptop |

#### 5.1.2 Administrator

| Attribute | Description |
|---|---|
| Description | Person responsible for managing user accounts, system configuration, and template updates |
| Technical Skill | [ASSUMPTION] Comfortable with system administration tasks |
| Primary Tasks | Manage operator accounts, configure system settings, update document templates as needed |
| Frequency of Use | Infrequent; as needed |

### 5.2 Future / Potential User Classes (Not MVP)

The following user classes are [FUTURE SCOPE] unless there is confirmed evidence they are required for the MVP:

| User Class | Description | Status |
|---|---|---|
| Office Manager | May oversee cases and review operator work | [FUTURE SCOPE] |
| Client Self-Service | Future possibility — clients preparing documents directly | [FUTURE SCOPE] |
| Additional Operator Roles | Specialized operator types (e.g., trainee, reviewer) | [FUTURE SCOPE] |

A client can be a stakeholder (see Section 4.4) without being a system user. The MVP is primarily intended for professionals preparing documents.

---

## 6. System Scope

### 6.1 MVP Scope

The MVP covers the complete workflow for **land-rent document preparation** by an authorized operator:

- Case creation and management, with **Case Type** classification (MVP: LAND_RENT only)
- **Persistent cases**: cases and finalized documents are retained after finalization and remain retrievable (retention/archival/backup/deletion policies [TO BE VALIDATED])
- **Recent Cases** as the post-authentication landing experience (open existing or create new) and a case directory for browsing by Case Type
- **Client management**: create, view, search, associate with cases, and reuse Client records (a Client is distinct from the Application User)
- Manual data entry (primary information-acquisition mechanism; cases can be created and populated without any source document)
- Source document capture via camera or file upload (optional supporting capability)
- Human verification and correction of Candidate Data
- Structured storage of Verified Case Data
- Template-based document generation
- Draft review by the operator
- Operator-driven finalization
- Storage of finalized documents with access control
- Distinction between **Source Documents**, **Generated Drafts**, and **Finalized Documents**

[RESOLVED — Decision 009] OCR and automated extraction are **not** part of the MVP. They are future enhancements required before full deployment, subject to Phase 0.8 Technical Research.

### 6.2 Future Scope

| Module | Description | Priority |
|---|---|---|
| Land Sale / Trade | Document preparation for property sale transactions | Future |
| Land Transfer | Document preparation for inheritance, gift, and family transfers | Future |
| Additional Document Types | Support for other land-related documents | Future |
| Multi-Operator Workspace | Shared case access across multiple operators in an office | Future |
| Client Portal | Potential self-service view for clients | Future consideration |

These are future possibilities and are not part of the MVP unless later approved.

### 6.3 Out of Scope

- Government registration or submission
- Integration with government land systems (LIMS, Mero Kitta, etc.)
- Provision of legal advice
- Autonomous legal decision-making
- Guarantee of legal validity
- Replacement of professional human judgment
- Replacement of government administrative processes

---

## 7. Functional Requirements

### 7.1 User Authentication and Authorization

**Conceptual separation:** Authentication establishes who the user is. Authorization determines what the user is permitted to do. The system shall use role-based access control conceptually, assigning permissions based on an authenticated user's assigned role. The MVP conceptually supports at least two roles: Operator and Administrator.

> Note: No implementation detail (PIN, password, biometric, token-based, session-based) is implied by these requirements. The exact authentication mechanism and permission model are [TO BE DETERMINED].

| Field                 | Description                                                                                                |
| --------------------- | ---------------------------------------------------------------------------------------------------------- |
| **ID**                | FR-001                                                                                                     |
| **Requirement**       | The system shall require authentication before granting access to system functions and case data.          |
| **Priority**          | Must                                                                                                       |
| **Status**            | [PROPOSED]                                                                                                 |
| **Rationale**         | The system will handle sensitive personal and property information. Unauthorized access must be prevented. |
| **Source**            | Stakeholder need (privacy, security)                                                                       |
| **Validation Needed** | Yes — authentication method (PIN, password, biometric) [TO BE DETERMINED]                                  |

| Field                 | Description                                                                                                                                                   |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ID**                | FR-002                                                                                                                                                        |
| **Requirement**       | The system shall enforce authorization based on the authenticated user's assigned role. The MVP shall support at least two roles: Operator and Administrator. |
| **Priority**          | Must                                                                                                                                                          |
| **Status**            | [PROPOSED]                                                                                                                                                    |
| **Rationale**         | Different responsibilities require different levels of system access. Role-based separation supports the Human Authority Principle.                           |
| **Source**            | Reasonable security practice                                                                                                                                  |
| **Validation Needed** | Yes — role definitions and permission scope [TO BE VALIDATED] with domain experts                                                                             |

| Field | Description |
|---|---|
| **ID** | FR-003 |
| **Requirement** | The Administrator shall be able to create, disable, and manage operator accounts. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | The system must support managing who has access. |
| **Source** | Reasonable practice for multi-user systems |
| **Validation Needed** | Yes |

### 7.2 Case Management

The Case is a first-class domain concept that organizes all information and artifacts related to a single land-rent document preparation instance. The conceptual model is:

```
CASE
├── Case Type (MVP: LAND_RENT)
├── Clients (reusable; distinct from Application Users)
├── Parties
├── Property Information
├── Source Documents
├── Candidate / Entered Data
├── Verified Case Data
├── Draft Documents (Generated Drafts)
├── Finalized Documents
└── Audit History
```

> The lifecycle below is [PROPOSED] and has not been validated with domain experts. The exact states and transitions may differ from actual practice. Cases persist after finalization.

A conceptual lifecycle aligned across artifacts (see Glossary — Lifecycle):

```
Created
→ In Progress
→ Draft Generated
→ Under Review
→ Finalized
→ Persistent (retained for operational use; archival is [OPEN QUESTION])
```

| Field | Description |
|---|---|
| **ID** | FR-004 |
| **Requirement** | The operator shall be able to create a new case for each land-rent document preparation instance. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Cases provide the organizing structure for all related information and documents. |
| **Source** | Product vision |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-005 |
| **Requirement** | Each case shall have a unique identifier for reference and retrieval. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Unique identification supports case management, retrieval, and audit. |
| **Source** | Reasonable practice |
| **Validation Needed** | No |

| Field | Description |
|---|---|
| **ID** | FR-006 |
| **Requirement** | The operator shall be able to view a list of all cases with their current status. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Operators need visibility into their active and past cases. |
| **Source** | Reasonable practice |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-007 |
| **Requirement** | [PROPOSED] The system shall track the status of each case through its lifecycle (e.g., Created, In Progress, Draft Generated, Under Review, Finalized, Persistent). |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Status tracking helps operators understand which cases are in progress and what steps remain. |
| **Source** | Proposed lifecycle |
| **Validation Needed** | Yes — lifecycle states must be validated with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-008 |
| **Requirement** | The system shall record the date and time of case creation and the identity of the creating operator. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Audit trail requirement. |
| **Source** | Reasonable practice |
| **Validation Needed** | No |

| Field | Description |
|---|---|
| **ID** | FR-035 |
| **Requirement** | Each case shall be assigned a Case Type at creation. The MVP supports a single Case Type: LAND_RENT. Additional Case Types are future scope. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Case Type classifies a case and determines its workflow and document requirements (Decision 005). It is distinct from a property's use purpose and from document type. |
| **Source** | Product decision 005 |
| **Validation Needed** | Yes — classification taxonomy [TO BE VALIDATED] |

| Field | Description |
|---|---|
| **ID** | FR-036 |
| **Requirement** | Cases shall persist after finalization. Finalized cases and finalized documents are intended to be retained indefinitely for operational use. Exact retention, archival, backup, and deletion policies are [TO BE VALIDATED]. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | A case and its artifacts remain available after finalization for operational use (Decision 004). No legal retention period is asserted. |
| **Source** | Product decision 004 |
| **Validation Needed** | Yes — retention/archival/backup/deletion policy [TO BE VALIDATED] |

| Field | Description |
|---|---|
| **ID** | FR-037 |
| **Requirement** | The system shall present Recent Cases as the post-authentication landing experience, from which the operator can open an existing case, create a new case, and access the broader case directory. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Recent Cases is the primary post-auth experience: open existing or create new (Decision 004). |
| **Source** | Product decision 004 |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-038 |
| **Requirement** | The system shall allow authorized users to organize, browse, and retrieve cases by Case Type and other supported classification criteria. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | A case directory supports organizing, browsing, and retrieving cases by classification (Decision 005). No specific navigation hierarchy is prescribed. |
| **Source** | Product decision 005 |
| **Validation Needed** | Yes — classification criteria [TO BE VALIDATED] |

| Field | Description |
|---|---|
| **ID** | FR-039 |
| **Requirement** | The operator shall be able to open an existing case (including finalized cases) to view or resume its contents. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Operators resume in-progress cases and reference finalized cases (Decision 004). |
| **Source** | Product decision 004 |
| **Validation Needed** | No |

| Field | Description |
|---|---|
| **ID** | FR-040 |
| **Requirement** | The system shall maintain per-case metadata: Case ID, Case Type, Status, Creation date, Last updated, associated Clients, Property, Source Documents, Generated Documents, and Finalized Documents. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Complete case metadata supports retrieval, organization, and operational use of persistent cases (Decision 004). |
| **Source** | Product decision 004 |
| **Validation Needed** | No |

### 7.3 Source Document Capture and Upload

Camera capture of source documents is a core part of the product vision. File upload of existing digital images or PDFs is also a proposed capability. The operator should be able to review a captured image before accepting it for processing, and recapture or replace a poor-quality capture.

> The exact set of source document types expected in a land-rent case is [TO BE VALIDATED] and should not be assumed until the actual templates and workflow are analyzed.

| Field | Description |
|---|---|
| **ID** | FR-009 |
| **Requirement** | The operator shall be able to capture images of source documents using a device camera. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Capture is an optional supporting capability (Decision 009); manual data entry does not depend on it. |
| **Source** | Product vision |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-010 |
| **Requirement** | The operator shall be able to upload existing digital images or PDF files of source documents. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Some source documents may already be available in digital form. Upload is an optional supporting capability (Decision 009). |
| **Source** | Product vision |
| **Validation Needed** | Yes |

| Field | Description |
|---|---|
| **ID** | FR-011 |
| **Requirement** | [TO BE VALIDATED] The operator shall be able to associate each captured/uploaded source document with a document type label. The exact document type labels are [TO BE VALIDATED] and depend on the actual land-rent workflow and required source documents. |
| **Priority** | Should |
| **Status** | [TO BE VALIDATED] |
| **Rationale** | Document type association supports later processing and retrieval. The exact document type labels are unknown without analyzing the actual templates and workflow. |
| **Source** | Product vision |
| **Validation Needed** | Yes — document types require template and workflow analysis |

| Field | Description |
|---|---|
| **ID** | FR-012 |
| **Requirement** | The operator shall be able to view all captured/uploaded source documents for a case. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Operators need to review source documents during information extraction. |
| **Source** | Reasonable practice |
| **Validation Needed** | No |

| Field | Description |
|---|---|
| **ID** | FR-012a |
| **Requirement** | [PROPOSED] The operator shall be able to review a captured image before accepting it for processing. The operator should be able to recapture or replace an unsatisfactory capture. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Image quality affects readability and potential OCR processing. The operator should confirm the capture is usable before proceeding. |
| **Source** | Reasonable design practice |
| **Validation Needed** | Yes — with domain experts |

### 7.4 Document Classification

For the MVP, manual document classification (the operator labelling each captured/uploaded source document with a type) is sufficient. Automated document classification (the system determining the document type from the image) is a future capability.

- **Manual Document Labeling:** The operator identifies and labels source documents (see FR-011). This is the proposed MVP approach.
- **Automated Document Classification:** [FUTURE SCOPE] The system could automatically identify document types. Not required for MVP.

[OPEN QUESTION] Whether automated document classification is required or valuable for the initial release has not been determined.

### 7.5 OCR and Information Extraction

**Conceptual separation:** OCR (optical character recognition) converts document images into raw text. Field extraction (also called structured information extraction) identifies specific data values within that text and maps them to structured fields. These are distinct capabilities and are addressed separately.

**Automated extraction is optional.** OCR and automated extraction must NOT be mandatory prerequisites for the system. The system must conceptually support both paths:

| Path | Flow |
|---|---|
| Automated extraction succeeds | Source Document → OCR / Text Recognition → Raw Text → Field Extraction → Candidate Data → Human Verification → Verified Case Data |
| Automated extraction unavailable or fails | Source Document → Manual Data Entry → Candidate Data → Human Verification → Verified Case Data |

The MVP product must remain useful without OCR. Automated extraction (including OCR, AI-based extraction, or other technologies) is defined as an optional automation mechanism whose feasibility is subject to technical research.

> No OCR engine, vendor, library, or AI model is selected by this document. Technology choices will be informed by Phase 0.8 Technical Research.

| Field | Description |
|---|---|
| **ID** | FR-013 |
| **Requirement** | [PROPOSED] The system may incorporate automated information extraction from source document images (using OCR or other technologies) to produce Candidate Data. This is an optional capability. |
| **Priority** | Could |
| **Status** | [PROPOSED] |
| **Rationale** | Automated extraction could reduce manual data entry effort, but the feasibility and accuracy have not been established. |
| **Source** | Product vision |
| **Validation Needed** | Yes — OCR feasibility and accuracy for Nepali (Devanagari) land documents is the subject of Phase 0.8 Technical Research. |

| Field | Description |
|---|---|
| **ID** | FR-014 |
| **Requirement** | If automated extraction is implemented, the system shall present the resulting Candidate Data to the operator for human verification before it may be used in document generation. |
| **Priority** | Must (if automated extraction is implemented) |
| **Status** | [PROPOSED] |
| **Rationale** | Human verification is a core principle. Automated extraction may contain errors. Even if automated extraction is implemented, manual entry remains the primary acquisition path (Decision 009) and must remain available. |
| **Source** | Product vision: human-in-the-loop |
| **Validation Needed** | Yes |

| Field | Description |
|---|---|
| **ID** | FR-015 |
| **Requirement** | [PROPOSED] If automated extraction is implemented, the system may indicate confidence levels for extracted values where feasible. |
| **Priority** | Could |
| **Status** | [PROPOSED] |
| **Rationale** | Confidence information helps the operator prioritize verification effort on uncertain values. |
| **Source** | Reasonable practice for OCR/extraction systems |
| **Validation Needed** | Yes — technical feasibility |

### 7.6 Human Verification

**Core principle:** No automatically extracted, inferred, or system-generated information may be used in final document generation until it has been reviewed and confirmed by an authorized operator. This applies to all automation mechanisms, including OCR, AI-based extraction, automated document classification, and automated field inference.

The conceptual verification workflow is:

```
Source Documents
→ Candidate Data (from any source: automated extraction, manual entry, import)
→ Human Verification and Correction
→ Verified Case Data
→ Document Generation
```

Human verification is a core system requirement — not merely an optional adjunct to OCR. The system must facilitate the operator's review of Candidate Data against the source documents.

| Field | Description |
|---|---|
| **ID** | FR-016 |
| **Requirement** | The system shall present Candidate Data to the operator in a structured review interface for human verification. The operator must explicitly confirm or correct each data field before it becomes part of Verified Case Data. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | The operator must review all information before it is used in document generation. This is the core human-in-the-loop requirement. |
| **Source** | Product vision: Human Authority Principle |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-017 |
| **Requirement** | The operator shall be able to view source documents alongside Candidate Data during human verification. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Side-by-side comparison supports accurate verification against original documents. |
| **Source** | Reasonable design practice |
| **Validation Needed** | Yes — with domain experts |

### 7.7 Data Correction and Manual Entry

Candidate Data (whether from automated extraction or manual entry) may contain errors or omissions. The operator must be able to review, correct, and complete all data before it becomes Verified Case Data. The distinction:

- **Candidate Data:** Information before human verification — may originate from automated extraction, manual entry, or import.
- **Verified Case Data:** Information confirmed by the authorized operator during human verification. This is the authoritative structured data used for document generation.

| Field | Description |
|---|---|
| **ID** | FR-018 |
| **Requirement** | The operator shall be able to correct any Candidate Data field during human verification. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | The human-in-the-loop principle requires that the operator can correct any inaccuracies before data becomes Verified Case Data. |
| **Source** | Product vision |
| **Validation Needed** | No |

| Field | Description |
|---|---|
| **ID** | FR-019 |
| **Requirement** | The operator shall be able to manually enter data for fields that are not present in or cannot be extracted from source documents. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Not all required information may be present in source documents; some will come from the client verbally. Manual entry is the primary acquisition mechanism and must not depend on source documents or automated extraction (Decision 009). |
| **Source** | Product vision |
| **Validation Needed** | Yes — with domain experts |

### 7.8 Candidate and Verified Case Data

The system conceptually maintains two levels of structured data:

- **Candidate Data:** Information that has been extracted or entered but not yet verified by the authorized operator.
- **Verified Case Data:** Information that has been reviewed, corrected, and explicitly confirmed by the authorized operator. Verified Case Data is the authoritative structured data source for document generation.

[OPEN QUESTION] Whether original Candidate Data values must be retained permanently for audit or reference purposes is not yet determined.

| Field | Description |
|---|---|
| **ID** | FR-020 |
| **Requirement** | The system shall maintain Verified Case Data as structured information separate from source documents and generated documents. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Structured, verified data enables document generation, case retrieval, and potential reuse. It is the core of the proposed system concept. |
| **Source** | Product vision |
| **Validation Needed** | Yes |

### 7.9 Land-Rent Document Generation

Document generation uses Verified Case Data and a controlled template to produce a draft document. Every generated document should be associated with:

- Template identity
- Template version
- Generation timestamp
- Finalization timestamp (if applicable)
- Finalizing operator (if applicable)

The conceptual workflow:

```
Verified Case Data + Template (identified version)
→ Draft Document
→ Human Review
→ Finalized Document
```

> Template versioning is important: if a template is updated (e.g., clauses change), previously generated documents should remain associated with the template version used at generation time.

| Field | Description |
|---|---|
| **ID** | FR-021 |
| **Requirement** | The system shall generate a land-rent document draft using Verified Case Data and a controlled document template. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Automated document generation is the primary value proposition of the system. |
| **Source** | Product vision |
| **Validation Needed** | Yes — the exact template structure and content require analysis of actual land-rent document templates. |

| Field | Description |
|---|---|
| **ID** | FR-022 |
| **Requirement** | [TO BE VALIDATED] The generated document shall be in the Nepali language. |
| **Priority** | Must |
| **Status** | [TO BE VALIDATED] |
| **Rationale** | Land-rent documents in Nepal are expected to be in Nepali. |
| **Source** | Domain research |
| **Validation Needed** | Yes — confirm language requirements with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-023 |
| **Requirement** | [PROPOSED] The document template shall contain static content (standard clauses) and variable fields (case-specific information). |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | A template approach separates fixed document structure from case-specific data. |
| **Source** | Product vision |
| **Validation Needed** | Yes — template structure requires analysis |

| Field | Description |
|---|---|
| **ID** | FR-024 |
| **Requirement** | [PROPOSED] The document template may include conditional sections that are included or excluded based on case information. |
| **Priority** | Could |
| **Status** | [PROPOSED] |
| **Rationale** | Different rental situations may require different clauses. |
| **Source** | Reasonable inference from domain research |
| **Validation Needed** | Yes — requires analysis of actual template variations |

### 7.10 Draft Document Review

The generated document starts as a Draft. The operator reviews the draft before finalization. Draft review is distinct from human verification of data (Section 7.6); the operator should review the assembled document for correctness, completeness, and presentation.

| Field | Description |
|---|---|
| **ID** | FR-025 |
| **Requirement** | The operator shall be able to review the generated document draft within the system before finalization. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Human review of the generated output is a core principle of the proposed workflow. |
| **Source** | Product vision |
| **Validation Needed** | Yes |

| Field | Description |
|---|---|
| **ID** | FR-026 |
| **Requirement** | The operator shall be able to make text-level edits to the generated draft. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | The operator may need to adjust formatting, phrasing, or add notes not covered by the template. |
| **Source** | Reasonable practice |
| **Validation Needed** | Yes — the extent of editing required is [TO BE VALIDATED] |

### 7.11 Document Finalization

Finalization is a **state transition**, not merely saving a file. The conceptual transition is:

```
DRAFT
→ Authorized Human Review
→ FINALIZED (Finalized Document)
```

Once finalized, the Finalized Document must not be silently or directly modified. The finalized record retains associated metadata:

- Finalization timestamp
- Finalizing operator identity
- Template version used for generation
- Case association

> Terminology: The system record of a finalized document is called a **Finalized Document** (formerly "Finalized Document"). This does not imply legal validity. The system does not independently determine legal validity (see Section 2.5 Human Authority Principle).

| Field | Description |
|---|---|
| **ID** | FR-027 |
| **Requirement** | The operator shall explicitly perform a finalization action to transition a document from Draft to Finalized Document. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Finalization is the gate between draft and completed document. It is a deliberate, authorized action. |
| **Source** | Product vision |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-028 |
| **Requirement** | After finalization, the Finalized Document shall not be directly editable. Any revision must create a new version or a new case, preserving the original finalized record. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Finalized documents must be distinguishable from drafts and protected from accidental or unauthorized modification. |
| **Source** | Product vision, document integrity |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-029 |
| **Requirement** | The system shall record the date, time, operator identity, and template version at the time of finalization. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Audit trail for completed documents. |
| **Source** | Reasonable practice |
| **Validation Needed** | No |

### 7.12 Finalized Document Storage

Finalized documents shall be persistently retained as the system's Finalized Documents. The retention policy for other artifacts — source documents, Candidate Data, Verified Case Data, draft documents, and intermediate processing artifacts — is not yet determined.

> [OPEN QUESTION] Retention policies for source documents, Candidate Data, drafts, and intermediate artifacts are not yet determined. See Section 10.

| Field | Description |
|---|---|
| **ID** | FR-030 |
| **Requirement** | The system shall persistently retain Finalized Documents in a format suitable for printing and delivery. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Finalized documents must be available for delivery to clients and for record-keeping. |
| **Source** | Product vision |
| **Validation Needed** | Yes — output format [TO BE VALIDATED] with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-031 |
| **Requirement** | The system shall associate each Finalized Document with its originating case for retrieval. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Case-to-document association enables organized retrieval. |
| **Source** | Reasonable practice |
| **Validation Needed** | No |

### 7.13 Search and Retrieval

Distinguish between:

- **Case Search:** Locating a specific case by its attributes.
- **Finalized Document Retrieval:** Accessing a previously finalized document associated with a case.

Potential search fields (all [PROPOSED] / [TO BE VALIDATED]) may include: Case ID, Case Type, party name, client name, property identifier (kitta number), and date range.

| Field | Description |
|---|---|
| **ID** | FR-032 |
| **Requirement** | The operator shall be able to search for past cases and retrieve associated Finalized Documents. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Operators may need to reference or reproduce past documents. |
| **Source** | Reasonable practice |
| **Validation Needed** | Yes — search criteria [TO BE VALIDATED] with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-033 |
| **Requirement** | [PROPOSED] Search may support criteria including case ID, case type, party name, client name, property identifier (kitta number), and date range. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | These are likely search criteria based on domain research, but actual operator needs are unknown. |
| **Source** | Domain research |
| **Validation Needed** | Yes — search criteria require validation with domain experts |

### 7.14 Auditability and History

The system should maintain an Audit History of significant lifecycle events. Potential events include: case created, source document added, data extracted, data modified, data verified, draft generated, draft modified, document finalized, finalized document accessed, finalized document downloaded.

> The exact set of audit events required for the MVP is [TO BE VALIDATED]. Not every listed event is confirmed as an MVP requirement.

| Field | Description |
|---|---|
| **ID** | FR-034 |
| **Requirement** | The system shall maintain an Audit History of significant lifecycle events. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Audit trail supports accountability and troubleshooting. |
| **Source** | Reasonable practice for systems handling sensitive information |
| **Validation Needed** | Yes — scope of audit events [TO BE VALIDATED] |

### 7.15 Client Management

> A **Client** is the person or organization on whose behalf a case is processed — distinct from the **Application User** (operator). Client records are reusable across cases (Decision 006). Client fields reuse the Field Dictionary party identity fields; no fields are invented without validation.

| Field | Description |
|---|---|
| **ID** | FR-041 |
| **Requirement** | The operator shall be able to create a Client record containing the client's identity information (name, lineage, address, citizenship details; organization details where applicable). |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Clients are reusable domain entities (Decision 006). |
| **Source** | Product decision 006 |
| **Validation Needed** | Yes — exact Client fields [TO BE VALIDATED] |

| Field | Description |
|---|---|
| **ID** | FR-042 |
| **Requirement** | The operator shall be able to view a Client's stored information. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Operators need to review client information (Decision 006). |
| **Source** | Product decision 006 |
| **Validation Needed** | No |

| Field | Description |
|---|---|
| **ID** | FR-043 |
| **Requirement** | [PROPOSED] The operator shall be able to search for Client records (e.g., by name, citizenship number, or other supported criteria). |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Locating existing clients enables reuse and avoids duplicate records (Decision 006). |
| **Source** | Product decision 006 |
| **Validation Needed** | Yes — search criteria [TO BE VALIDATED] |

| Field | Description |
|---|---|
| **ID** | FR-044 |
| **Requirement** | The operator shall be able to associate a Client with a Case. Client information may pre-fill the case's party fields. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | A case is processed on behalf of one or more clients (Decision 006). |
| **Source** | Product decision 006 |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-045 |
| **Requirement** | The operator shall be able to reuse an existing Client record across multiple Cases rather than re-entering client information. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Client records are reusable (Decision 006); reuse reduces re-entry and inconsistency. |
| **Source** | Product decision 006 |
| **Validation Needed** | No |

| Field | Description |
|---|---|
| **ID** | FR-046 |
| **Requirement** | The operator shall be able to view the Cases associated with a given Client. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Operators need to see all cases involving a client (Decision 006). |
| **Source** | Product decision 006 |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | FR-047 |
| **Requirement** | [PROPOSED] The system shall allow Source Documents to be associated with a Client in addition to their Case association. Source document capture/upload remains subject to Section 7.3; this requirement covers the association model. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Source documents are evidence tied to a client and/or a case (Decisions 006, 007). Whether they live at the client level, case level, or both is [OPEN QUESTION]. |
| **Source** | Product decisions 006, 007 |
| **Validation Needed** | Yes — storage level [OPEN QUESTION] |

### 7.16 Document Types (Source / Draft / Finalized)

> The system distinguishes three non-interchangeable document types (Decision 007): **Source Documents** (supplied/captured evidence), **Generated Drafts** (produced, not finalized), and **Finalized Documents** (explicitly finalized by a human).

| Field | Description |
|---|---|
| **ID** | FR-048 |
| **Requirement** | The system shall distinguish Source Documents, Generated Drafts, and Finalized Documents as separate, non-interchangeable document types. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | The three document types are distinct and not interchangeable (Decision 007). |
| **Source** | Product decision 007 |
| **Validation Needed** | No |

| Field | Description |
|---|---|
| **ID** | FR-049 |
| **Requirement** | The system shall not present a Source Document or a Generated Draft as a Finalized Document. Only a document explicitly finalized by an authorized human is a Finalized Document, and the system does not imply legal validity. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Finalization is a human decision (Decisions 007, 008; Human Authority Principle, Section 2.5). |
| **Source** | Product decisions 007, 008 |
| **Validation Needed** | No |

---

## 8. Non-Functional Requirements

### 8.1 Security

| Field | Description |
|---|---|
| **ID** | NFR-001 |
| **Requirement** | The system shall protect stored case, client, and document data from unauthorized access. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | The system handles personal identity information (including Client records) and property records. |
| **Validation Needed** | Yes — specific security mechanisms [TO BE DETERMINED] |

| Field | Description |
|---|---|
| **ID** | NFR-002 |
| **Requirement** | The system shall require operator authentication before access to any case data. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Authentication gates access to sensitive data. |
| **Validation Needed** | Yes |

### 8.2 Privacy

| Field | Description |
|---|---|
| **ID** | NFR-003 |
| **Requirement** | The system shall handle personal information (names, citizenship numbers, property details) in accordance with applicable data protection principles. |
| **Priority** | Must |
| **Status** | [OPEN QUESTION] |
| **Rationale** | Applicable privacy regulations in Nepal have not been researched. Whether the Nepal Privacy Act 2075 or other regulations apply [TO BE DETERMINED]. |
| **Validation Needed** | Yes — legal research required |

### 8.3 Performance

| Field | Description |
|---|---|
| **ID** | NFR-004 |
| **Requirement** | The system should provide responsive interactions suitable for normal document-preparation workflows. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Operators should not be significantly delayed by system response times. |
| **Validation Needed** | Yes — specific performance targets [TO BE DETERMINED] |

### 8.4 Availability

| Field | Description |
|---|---|
| **ID** | NFR-005 |
| **Requirement** | [TO BE DETERMINED] Availability requirements depend on the deployment model (online, offline, or hybrid). |
| **Priority** | TBD |
| **Status** | [OPEN QUESTION] |
| **Rationale** | The deployment model has not been decided. Offline operation may be required in areas with limited connectivity. |
| **Validation Needed** | Yes — deployment model decision required |

[OPEN QUESTION] **Connectivity:** Does the MVP require offline or degraded-connectivity operation? The decision between online-only, offline-capable, and offline-first has not been made. This question affects architecture, storage, data synchronization, and application design but is not resolved here.

### 8.5 Reliability

| Field | Description |
|---|---|
| **ID** | NFR-006 |
| **Requirement** | The system should preserve data integrity during use, particularly during document finalization. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Data loss or corruption during finalization could result in rework or document errors. |
| **Validation Needed** | No |

### 8.6 Usability

| Field | Description |
|---|---|
| **ID** | NFR-007 |
| **Requirement** | The system should be usable by operators with varying levels of technical experience. |
| **Priority** | Should |
| **Status** | [ASSUMPTION] |
| **Rationale** | Notary/document-preparation professionals have unknown technical skill levels. |
| **Validation Needed** | Yes — user research required |

| Field | Description |
|---|---|
| **ID** | NFR-008 |
| **Requirement** | [PROPOSED] The primary interface should be designed for mobile/tablet use (touchscreen). |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | The product vision describes a mobile-first application, but this has not been confirmed with users. |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | NFR-009 |
| **Requirement** | The system interface should support the Nepali language for content within documents. [TO BE VALIDATED] Whether the system UI itself should be in Nepali, English, or bilingual. |
| **Priority** | Should |
| **Status** | [TO BE VALIDATED] |
| **Rationale** | Operators in Nepal may prefer Nepali, English, or a combination. |
| **Validation Needed** | Yes — with domain experts |

### 8.7 Accessibility

[OPEN QUESTION] Specific accessibility requirements have not been identified. These should be considered during design but are not currently specified.

### 8.8 Maintainability

| Field | Description |
|---|---|
| **ID** | NFR-010 |
| **Requirement** | The system should support updates to document templates without requiring application code changes. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Document templates may change due to legal requirements or practice changes. Separating templates from code reduces maintenance burden. |
| **Validation Needed** | Yes — template management approach [TO BE DETERMINED] |

### 8.9 Scalability

[ASSUMPTION] The initial deployment is expected to involve a single operator or a small number of operators. Scalability requirements beyond this scope are [OPEN QUESTION].

### 8.10 Auditability

| Field | Description |
|---|---|
| **ID** | NFR-011 |
| **Requirement** | The system should maintain logs that allow reconstruction of significant events (case creation, document generation, finalization, access). |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Supports accountability and potential evidentiary needs. |
| **Validation Needed** | Yes — audit scope [TO BE VALIDATED] |

### 8.11 Data Integrity

| Field | Description |
|---|---|
| **ID** | NFR-012 |
| **Requirement** | The system should prevent concurrent conflicting modifications to the same case data. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Prevents data loss or confusion in multi-operator scenarios. |
| **Validation Needed** | Yes — depends on whether multi-operator is an MVP requirement |

### 8.12 Backup and Recovery

| Field | Description |
|---|---|
| **ID** | NFR-013 |
| **Requirement** | The system should support regular backup of case data, client data, source documents, and finalized documents. |
| **Priority** | Should |
| **Status** | [PROPOSED] |
| **Rationale** | Data loss could result in significant work being lost. |
| **Validation Needed** | Yes — backup frequency and method [TO BE DETERMINED] |

---

## 9. Data Requirements

This section describes the conceptual information the system may need to manage. It does not define a database schema or select a technology.

### 9.1 User Information

Application Users are the operators and administrators of the system. They are distinct from Clients (see 9.13).

- Operator identity (name, credentials, role)
- Authentication data
- Access permissions

### 9.2 Case Information

- Case identifier
- Case Type (classification; MVP: LAND_RENT)
- Case status
- Creation date and operator
- Last updated (date/time)
- Finalization date and operator (if applicable)
- Associated Client(s)
- Case notes

### 9.3 Property Information

- Property location description
- Plot / kitta number
- Land area and measurement unit
- Use Purpose (agriculture, business, residence, mixed) — [TO BE VALIDATED]

[OPEN QUESTION] Exactly which property fields are required for a land-rent document is unknown without analyzing the actual template.

### 9.4 Party Information

- Lessor (property owner): name, citizenship number, address, contact
- Lessee (tenant): name, citizenship number, address, contact
- Witnesses: name, age, address (at least one witness per party; citizenship optional) — see BR-008

[TO BE VALIDATED] Whether additional party information is required.

### 9.5 Rental Terms Information

- Rent amount
- Payment schedule / frequency
- Lease duration
- Start date
- Deposit amount (if any)
- Utility responsibilities
- Permitted use

[TO BE VALIDATED] The exact set of rental terms required depends on the actual template and clauses.

### 9.6 Source Document Metadata

- Document type label
- Date captured/uploaded
- File format
- Operator-assigned label
- Association to case
- Association to Client (where applicable — [OPEN QUESTION] whether source documents live at client level, case level, or both)

### 9.7 Candidate Data

Candidate Data is information that has been acquired (via automated extraction, manual entry, or import) but has not yet been verified by the authorized operator.

- Raw extracted text (if OCR/automated extraction is used)
- Extraction confidence values (if applicable)
- Extraction/entry timestamp
- Data source indicator (automated extraction / manual entry / import)
- Original value before operator correction (if retention of originals is implemented)

### 9.8 Verified Case Data

Verified Case Data is information that has been reviewed, corrected (if needed), and explicitly confirmed by the authorized operator. It is the authoritative structured data source for document generation.

- Case association
- Field name and value
- Verification timestamp and verifying operator
- Correction history if applicable

[OPEN QUESTION] Whether pre-verification Candidate Data values must be retained permanently for audit or reference purposes has not been determined.

### 9.9 Template Information

- Template identifier
- Template version
- Template content (static text, variable fields, conditional sections)

[TO BE DETERMINED] Template storage format and management approach.

### 9.10 Draft Document Metadata

- Draft generation timestamp
- Draft status (draft, under review, finalized)
- Editing history (if tracked)

### 9.11 Finalized Document Metadata

- Unique finalized document identifier
- Case association
- Finalization timestamp and operator
- Template identity and version used for generation
- Document format
- Storage location/path

### 9.12 Audit Records

- Event timestamp
- Event type
- Operator identity
- Case/document reference
- Details of the event

### 9.13 Client Information

A Client is the person or organization on whose behalf a case is processed, distinct from the Application User. Client fields reuse the Field Dictionary party identity fields (no invented fields):

- Full name (or organization name)
- Lineage (grandfather, father) for individuals
- Address (district, municipality, ward)
- Citizenship details (number, issue date, issue district)
- Organization details (name, registration) where the client is an entity
- Association to one or more Cases (a Client may participate in many Cases)

### 9.14 Case Type

- Case Type identifier (MVP: LAND_RENT)
- Case Type display name / description
- Associated template(s) for the Case Type
- Case Type is distinct from a property's use purpose (9.3) and from document type (9.6, 9.10, 9.11)

### 9.15 Generated Document Metadata

Generated documents are system/operator outputs and are distinct from Source Documents (9.6). Each generated document is typed as a **Generated Draft** or a **Finalized Document**:

- Document kind (Draft / Finalized)
- Draft generation timestamp
- Finalization timestamp and operator (if finalized)
- Template identity and version
- Finalized document identifier and case association (if finalized)
- Output format / storage location

---

## 10. Document Management Requirements

### 10.1 Data Lifecycle and Document Lifecycle

The system manages two distinct but related lifecycles. These should not be conflated.

**Data Lifecycle** (concerns the information content of a case):

```
Captured / Entered Information
    → Candidate Data
    → Human Verification and Correction
    → Verified Case Data
```

**Document Lifecycle** (concerns the generated document):

```
Verified Case Data + Template (specific version)
    → Draft Document
    → Human Review
    → Finalized Document
```

### 10.2 Relationship Between Lifecycles

- Verified Case Data is the output of the Data Lifecycle and the input to the Document Lifecycle.
- Draft generation does not alter Verified Case Data.
- Re-verification of data (e.g., after a correction) may create new Candidate Data and new Verified Case Data.
- Re-generation of a draft may reuse existing Verified Case Data.

[OPEN QUESTION] Whether the system should support re-verification of existing Verified Case Data, or whether new information always flows through the full lifecycle.

### 10.3 Source Document Handling

- Source document images are the initial input to the case.
- [OPEN QUESTION] Should source documents be retained after finalization for audit/reference? Retention policy for source documents is not yet determined.

### 10.4 Draft Handling

- Drafts are generated from Verified Case Data and a specific template version.
- Drafts may be edited by the operator before finalization.
- [OPEN QUESTION] Should the system retain previous draft versions, or only the current draft?

### 10.5 Final Document Storage

Finalized Documents are persistently retained. Finalized cases are intended to be retained indefinitely for operational use; the exact retention, archival, backup, and deletion policy is [TO BE VALIDATED]. The retention policy for other artifacts — source documents, Candidate Data, Verified Case Data, draft documents, and intermediate processing artifacts — is not yet determined and may vary by artifact type.

> The system does not independently determine legal validity. A Finalized Document is the system's record of a completed document — it does not constitute a legally valid document unless the operator and relevant authorities deem it so.

Possible interpretations (none confirmed):

| Interpretation | Description |
|---|---|
| A | Source document images are deleted after finalization; only the finalized document PDF remains. |
| B | Source document images are retained but marked as "not finalized"; the finalized document is separately stored. |
| C | All case data (source images, extracted data, drafts, finalized document) is retained but only the finalized document is considered a record. |
| D | The finalized document is stored in a separate, more protected archive than working case data. |
| E | Some other interpretation not yet considered. |

[OPEN QUESTION] The correct interpretation for this project is not yet determined.

### 10.6 Final Document Identification

Each finalized document should have:

- A unique identifier
- The case identifier it belongs to
- The date and operator of finalization

### 10.7 Versioning

- [OPEN QUESTION] If a finalized document needs to be revised, should the system create a new version, or should the operator create a new case?
- [PROPOSED] If revisions are needed, the system should create a new version while preserving the original finalized document.

### 10.8 Retrieval

- Finalized documents should be retrievable by case ID, party name, client name, case type, property reference, and date range.
- [TO BE VALIDATED] With domain experts.

### 10.9 Access Control

- Only authorized operators should be able to access case data and finalized documents.
- [OPEN QUESTION] Should an operator be able to access cases created by another operator?

### 10.10 Retention

- Finalized cases and finalized documents are intended to be retained indefinitely for operational use (Decision 004). This is a product intent, not a legal retention period.
- [OPEN QUESTION] The exact retention, archival, backup, and deletion policy is [TO BE VALIDATED]. Whether finalized cases can be archived (moved out of the active directory) is also unresolved.

### 10.11 Backup

- Finalized documents and case data should be included in regular backups (see NFR-013).

---

## 11. OCR and Information Extraction Requirements

### 11.1 General Approach

**Conceptual architecture:**

```
Source Document
    → OCR / Text Recognition
    → Raw Text
    → Field Extraction (Structured Information Extraction)
    → Candidate Data
    → Human Verification
    → Verified Case Data
```

**Manual entry path (primary — always available):**

```
Source Document
    → Manual Data Entry
    → Candidate Data
    → Human Verification
    → Verified Case Data
```

**Key principles:**
- OCR is optional. Automated extraction is optional. The application must remain useful without OCR.
- Human verification is mandatory before any automatically extracted data can be used for final document generation.
- No OCR engine, vendor, library, or AI model is selected by this document.
- No accuracy or confidence thresholds are defined — these will be informed by Phase 0.8 Technical Research.
- Handwriting recognition is [OPEN QUESTION] — feasibility is unknown and subject to technical research.

The requirements in this section apply **if and only if** OCR or automated extraction is implemented. Per Decision 009, automated extraction is **not** part of the MVP; it is a future enhancement required before full deployment.

### 11.2 Image Capture

| Field | Description |
|---|---|
| **ID** | OCR-001 |
| **Requirement** | [PROPOSED] The system should guide the operator to capture images of adequate quality for OCR processing (adequate lighting, focus, framing). |
| **Priority** | Could |
| **Status** | [PROPOSED] |
| **Rationale** | Image quality directly affects OCR accuracy. |
| **Validation Needed** | Yes — technical feasibility |

### 11.3 Text Recognition

| Field | Description |
|---|---|
| **ID** | OCR-002 |
| **Requirement** | [PROPOSED] The OCR component should recognize printed Nepali (Devanagari) text. |
| **Priority** | Could |
| **Status** | [PROPOSED] |
| **Rationale** | Land documents in Nepal are primarily in Nepali. |
| **Validation Needed** | Yes — OCR accuracy for Devanagari is the subject of technical research (Phase 0.8) |

| Field | Description |
|---|---|
| **ID** | OCR-003 |
| **Requirement** | [PROPOSED] The OCR component should recognize English text and numerals that may appear within Nepali documents. |
| **Priority** | Could |
| **Status** | [PROPOSED] |
| **Rationale** | Land documents may contain English-language elements (dates, numerals, transliterated names). |
| **Validation Needed** | Yes |

### 11.4 Handwritten Text

[OPEN QUESTION] Whether OCR must handle handwritten text is not determined. Land documents may contain handwritten annotations, signatures, or stamps. The scope for handwritten text recognition is [TO BE DETERMINED] after sample document analysis.

### 11.5 Human Verification

| Field | Description |
|---|---|
| **ID** | OCR-004 |
| **Requirement** | [PROPOSED] All OCR-extracted information must be presented for human verification before being used in document generation. |
| **Priority** | Must (if OCR is implemented) |
| **Status** | [PROPOSED] |
| **Rationale** | Human-in-the-loop principle. OCR may contain errors, especially on complex documents. |
| **Validation Needed** | Yes |

### 11.6 Missing and Conflicting Information

| Field | Description |
|---|---|
| **ID** | OCR-005 |
| **Requirement** | [PROPOSED] The system should allow the operator to indicate when expected information is missing from a source document. |
| **Priority** | Could |
| **Status** | [PROPOSED] |
| **Rationale** | Not all required information may be present in source documents. |
| **Validation Needed** | Yes — with domain experts |

| Field | Description |
|---|---|
| **ID** | OCR-006 |
| **Requirement** | [PROPOSED] The system should support the operator in resolving information that is inconsistent between source documents. |
| **Priority** | Could |
| **Status** | [PROPOSED] |
| **Rationale** | Conflicting information between documents must be resolved by the operator. |
| **Validation Needed** | Yes — with domain experts |

---

## 12. Document Generation Requirements

### 12.1 Conceptual Workflow

```
Verified Case Data
    +
    Template (specific version)
    →
    Draft Document
    →
    Human Review
    →
    Finalized Document
```

Every generated document should be associated with:
- Template identity (which template was used)
- Template version (which version of that template)
- Generation timestamp
- Finalization timestamp (if finalized)
- Finalizing operator (if finalized)

> Template versioning is important: if a template is updated, previously generated documents must remain associated with the template version used at generation time.

### 12.2 Template-Based Generation

| Field | Description |
|---|---|
| **ID** | DG-001 |
| **Requirement** | Document generation shall use a template containing fixed content and variable fields, populated from Verified Case Data. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | Separating template from data enables consistent output and manageable maintenance. |
| **Validation Needed** | Yes — template design requires analysis of actual land-rent document examples |

### 12.3 Template Versioning

- Each template shall have a unique identity and version identifier.
- Generated documents shall record the template identity and version used.
- [TO BE DETERMINED] The exact versioning mechanism is not specified here and depends on the template management approach.

### 12.4 Variable Fields

- Variable fields shall be populated from Verified Case Data.
- [TO BE VALIDATED] The exact set of variable fields depends on the actual template and is unknown at this time.

### 12.5 Static Content

- Static content includes standard clauses and formatting.
- [TO BE VALIDATED] The exact clauses for a land-rent document are unknown without template analysis.

### 12.6 Conditional Sections

- [PROPOSED] The template may support conditional sections that are included based on case data (e.g., "if deposit is specified, include deposit clause").
- [TO BE VALIDATED] Whether conditional sections are needed requires template analysis and domain expert input.

### 12.7 Nepali Language

| Field | Description |
|---|---|
| **ID** | DG-002 |
| **Requirement** | [TO BE VALIDATED] The generated document shall be in the Nepali language using proper Devanagari script. |
| **Priority** | Must |
| **Status** | [TO BE VALIDATED] |
| **Rationale** | Land-rent documents in Nepal are typically in Nepali. |
| **Validation Needed** | Yes — confirm with domain experts |

### 12.8 Output Format

| Field | Description |
|---|---|
| **ID** | DG-003 |
| **Requirement** | [PROPOSED] The generated document should be output as a PDF file suitable for printing. |
| **Priority** | Must |
| **Status** | [PROPOSED] |
| **Rationale** | PDF is the standard format for printed document delivery. |
| **Validation Needed** | Yes — confirm with domain experts whether PDF or other formats are needed |

### 12.9 Draft and Finalization

- Generated documents start as drafts.
- Drafts can be reviewed and edited (see Section 7.10).
- Finalization transitions a draft to a Finalized Document (see Section 7.11).

---

## 13. Security and Privacy Requirements

### 13.1 Authentication

Authentication establishes the identity of the user. See FR-001. The authentication mechanism (PIN, password, biometric, or other) is [TO BE DETERMINED].

### 13.2 Authorization

Authorization determines what an authenticated user is permitted to do. See FR-002 and FR-003.

- Operator role: can create and manage cases, manage Client records, and generate and finalize documents.
- Administrator role: can manage operator accounts and system configuration.
- [PROPOSED] Additional roles may be defined as the system evolves.
- [PROPOSED] Access to Client records and their associated cases is restricted to authorized operators (see FR-041..FR-047, NFR-001).

### 13.3 Data Minimization Principle

[PROPOSED] The system should avoid retaining personal or sensitive information beyond what is necessary for the documented purpose and applicable retention requirements. This principle applies to:

- Source document images
- Candidate Data
- Verified Case Data
- Drafts
- Finalized Documents
- Audit logs

Exact retention periods are [TO BE DETERMINED] and should be informed by legal research, domain expert input, and practical operational needs.

### 13.4 Data Confidentiality

- Case data and finalized documents should be accessible only to authorized operators.
- [OPEN QUESTION] Data encryption requirements (at rest, in transit) are not yet specified and require security research.

### 13.5 Secure Data Transmission

- [OPEN QUESTION] Whether data transmission between system components requires encryption is not yet determined and depends on the deployment model.

### 13.6 Data Protection

- Operators should be trained on handling sensitive personal and property information.
- [OPEN QUESTION] Whether additional data protection measures are required depends on legal research and the deployment model.

### 13.7 Audit Logging

See FR-034 and NFR-011.

### 13.8 Data Retention

See Section 10.10.

### 13.9 Backup Security

Backups containing case data and finalized documents should be protected with access controls consistent with the live data (see NFR-013).

### 13.10 Compliance Requirements

| Requirement | Status |
|---|---|
| Compliance with Nepal Privacy Act 2075 | [OPEN QUESTION] — legal research required |
| Compliance with Electronic Transaction Act 2063 | [OPEN QUESTION] — legal research required |
| Compliance with data localization requirements (if any) | [OPEN QUESTION] — legal research required |

**The product is currently Nepal-focused.** Compliance with international regulations (e.g., GDPR) is not currently a requirement. If the product scope expands to serve users in other jurisdictions, compliance with applicable regulations should be addressed at that time. GDPR and other international frameworks are [FUTURE SCOPE] unless confirmed otherwise.

---

## 14. Business Rules

### 14.1 Known Project Rules

| ID | Rule | Status |
|---|---|---|
| BR-001 | Human review is required before document finalization. | [CONFIRMED] — explicit project principle |
| BR-002 | Finalized documents must be distinguishable from drafts. | [PROPOSED] |
| BR-003 | Only authorized users should access stored case data and finalized documents. | [PROPOSED] |
| BR-004 | The operator retains full control over document content and finalization. | [CONFIRMED] — explicit project principle |

### 14.2 Proposed Business Rules

| ID | Rule | Status |
|---|---|---|
| BR-005 | A case may be created only by an authorized operator. | [PROPOSED] |
| BR-006 | A finalized document may not be modified without creating a new version. | [PROPOSED] |
| BR-007 | Source documents should be associated with a case before processing. | [PROPOSED] |

### 14.3 Candidate Legal / Domain Rules Requiring Authoritative Verification

The following rules are derived from preliminary domain research but are **legally consequential** and must **not** be treated as confirmed or research-backed without authoritative verification. They are listed as candidate rules requiring validation by a qualified legal professional or domain expert.

| ID | Candidate Rule | Why Verification Is Required | Required Validation Source | Current Status |
|---|---|---|---|---|
| BR-008 | A minimum of one witness per party is required for a valid lease agreement. Witnesses are identified by name, age, and address; citizenship is optional. | Domain rule provided by the project owner (2026-08-13). The template shows 1–3 witnesses total recorded with name/address/age. Legal confirmation pending. | Nepali legal professional | [UNVERIFIED — CANDIDATE DOMAIN RULE] |
| BR-009 | Written agreement is mandatory when monthly rent exceeds NPR 20,000. | Preliminary research identifies this threshold, but the interpretation, exceptions, and enforcement in practice require authoritative verification. | Nepali legal professional or authoritative legal source | [UNVERIFIED — CANDIDATE DOMAIN RULE] |
| BR-010 | Registration at Land Revenue Office is required when annual rent exceeds NPR 500,000 or lease exceeds 10 years. | Preliminary research identifies these thresholds, but their applicability to different lease types and their practical relevance require verification. | Nepali legal professional or authoritative legal source | [UNVERIFIED — CANDIDATE DOMAIN RULE] |

> These rules are **not** confirmed and must **not** be implemented as system-enforced business rules until authoritatively verified. They are captured here to inform future legal/domain research.

### 14.4 Legal Rules Requiring Authoritative Verification

| ID | Rule | Status |
|---|---|---|
| BR-011 | Legal validity requirements for the generated document. | [OPEN QUESTION] — requires legal professional input |
| BR-012 | Whether the system-generated document format is acceptable for notarization. | [OPEN QUESTION] |
| BR-013 | Whether the system-generated document format is acceptable for Malpot registration (if applicable). | [OPEN QUESTION] |

### 14.5 Product Decision Business Rules

> These rules derive from agreed product decisions ([[../../00 - Project Control/Decision Log]] #004–008). They are project rules, not legal rules. No legal retention periods are asserted.

| ID | Rule | Status |
|---|---|---|
| BR-014 | Cases are persistent and long-lived: a case and its artifacts remain available after finalization. Finalized cases and finalized documents are intended to be retained indefinitely for operational use; exact retention, archival, backup, and deletion policies remain [TO BE VALIDATED]. | [PROPOSED] |
| BR-015 | Every case is classified by a Case Type. The MVP supports a single Case Type: LAND_RENT. Additional Case Types are future scope. | [PROPOSED] |
| BR-016 | Case Type is distinct from a property's use purpose (agricultural/business/residential) and from document type; these concepts must not be conflated. | [PROPOSED] |
| BR-017 | A Client is distinct from an Application User: the Client is the person/organization on whose behalf a case is processed and is not an operator of the system. | [PROPOSED] |
| BR-018 | A Client may be associated with one or more Cases; Client records are reusable across Cases. | [PROPOSED] |
| BR-019 | Source Documents, Generated Drafts, and Finalized Documents are distinct and non-interchangeable. Finalization is a human decision; the application does not determine legal validity. | [PROPOSED] |

---

## 15. External Interfaces

### 15.1 Mobile Application Interface

[PROPOSED] The primary user interface is expected to be a mobile application (tablet/smartphone) with:
- Camera integration for source document capture
- Touch-friendly data entry screens
- Document preview capabilities

### 15.2 Document Capture Interface

- Camera capture (primary proposed method)
- File upload (secondary proposed method)

### 15.3 OCR Service Interface

[PROPOSED | IF APPLICABLE] If OCR is implemented, an interface to an OCR processing service or library will be required. The specific technology is [TO BE DETERMINED] by Phase 0.8 Technical Research.

### 15.4 Document Generation Interface

The document generation capability will be implemented as a system component. The specific technology (template engine, PDF library) is [TO BE DETERMINED].

### 15.5 Storage Interface

[PROPOSED] Storage for case data, source document images, and finalized documents. The storage approach (local device, cloud, server) is [TO BE DETERMINED].

---

## 16. Constraints

| Constraint | Description |
|---|---|
| Nepal-Specific Domain | The system is designed exclusively for the Nepali land documentation domain. |
| Nepali Language | Generated documents must be in Nepali (Devanagari script). |
| Sensitive Data | The system handles personal identity information (citizenship numbers, names, property details). |
| Human-in-the-Loop | All automated processes produce outputs that require human review before use. |
| Document Accuracy | Errors in generated documents can have real-world consequences for clients and professionals. |
| Source Document Quality | The system depends on the quality of source documents provided by clients, which may vary significantly. |
| Domain Validation Required | Many requirements depend on domain knowledge that has not yet been validated with experts. |
| Legal Uncertainty | The legal requirements for system-generated documents are not fully known. |
| Template Dependence | Requirements for document generation depend on actual template analysis. |

---

## 17. Assumptions

| ID | Assumption | Impact | Validation Method | Status |
|---|---|---|---|---|
| AS-001 | The initial users are expected to be notary/document-preparation professionals. | Shapes all user-facing design | Domain expert interview | [TO BE VALIDATED] |
| AS-002 | Land-rent documents are currently prepared using word-processing software or handwritten. | Affects the value proposition of automated generation | Domain expert interview | [TO BE VALIDATED] |
| AS-003 | The primary device will be a mobile tablet or smartphone. | Affects UI design and platform choice | User research | [ASSUMPTION] |
| AS-004 | The operator has basic familiarity with mobile apps and document workflows. | Affects UI complexity and training needs | Domain expert interview | [ASSUMPTION] |
| AS-005 | Operators will have reliable internet connectivity during use. | Affects architecture decisions (online vs. offline) | User research | [TO BE VALIDATED] — online/offline/hybrid undecided (see the Connectivity open question under Non-Functional Requirements) |
| AS-006 | A single operator will work on one case at a time. | Affects concurrency requirements | Domain expert interview | [ASSUMPTION] |
| AS-007 | The land-rent document template has a stable structure that can be represented in a template engine. | Fundamental assumption for document generation | Template analysis | [TO BE VALIDATED] |
| AS-008 | Source documents are generally readable and of adequate quality for manual extraction by a human professional. | OCR feasibility depends partly on document quality | Sample document analysis | [ASSUMPTION] |
| AS-009 | The manual workflow for land-rent document preparation follows the general pattern described in Section 3.2. | Shapes the proposed system concept | Domain expert interview | [TO BE VALIDATED] |
| AS-010 | Users will trust the system to store sensitive case data. | Affects trust in the system | User research | [ASSUMPTION] |

---

## 18. Risks

| ID | Risk | Impact | Likelihood | Mitigation | Status |
|---|---|---|---|---|---|
| RSK-001 | OCR inaccuracies for Nepali (Devanagari) text make automated extraction unreliable. | Medium — affects an optional future enhancement, not the MVP | Unknown — requires research | Technical research (Phase 0.8); manual data entry remains the primary path (Decision 009) | [OPEN] |
| RSK-002 | Poor-quality source documents (faded, handwritten, stamped) cannot be reliably processed. | High — affects multiple requirements | Unknown — depends on document types | Sample document analysis; clear user guidance | [OPEN] |
| RSK-003 | The land-rent template is more complex or variable than anticipated. | Medium — may delay development | Unknown — requires template analysis | Template analysis (next project activity) | [OPEN] |
| RSK-004 | Operators may not trust system-generated documents, reducing adoption. | Medium — affects project success | Unknown | Human-in-the-loop design; iterative validation | [OPEN] |
| RSK-005 | Data loss due to device failure, accidental deletion, or lack of backups. | High — could lose client documents | Low with proper design | Backup requirements (NFR-013); clear storage design | [OPEN] |
| RSK-006 | Unauthorized access to sensitive case data. | High — privacy and reputational risk | Low with proper design | Authentication (FR-001); access control (FR-002) | [OPEN] |
| RSK-007 | Legal requirements for document format or content are not met by the generated document. | High — could make documents invalid | Unknown — requires legal research | Legal research; involve legal professionals | [OPEN] |
| RSK-008 | The system automates tasks that should require professional judgment. | Medium — ethical/legal risk | Medium | Human-in-the-loop requirement; clear boundaries | [OPEN] |
| RSK-009 | Domain complexity is underestimated, leading to incomplete requirements. | Medium — rework during development | Medium | Domain expert interviews; iterative requirements validation | [OPEN] |
| RSK-010 | The actual user workflow differs significantly from the proposed system concept. | High — system may not meet user needs | Unknown — requires validation | Domain expert interview; validate workflow | [OPEN] |

---

## 19. Open Questions

### 19.1 Domain Expert Questions

| ID | Question |
|---|---|
| OQ-DE-01 | What is the exact current workflow for preparing a land-rent document? |
| OQ-DE-02 | What tool/software do document-preparation professionals currently use? |
| OQ-DE-03 | What information do they extract from source documents, and what do they ask the client directly? |
| OQ-DE-04 | What are the most common errors in land-rent document preparation? |
| OQ-DE-05 | How are finalized documents currently stored and organized? |
| OQ-DE-06 | What are the biggest pain points in the current process? |
| OQ-DE-07 | Would OCR and automated document generation provide value? |

### 19.2 Legal / Regulatory Questions

| ID | Question |
|---|---|
| OQ-LR-01 | What are the legal requirements for a valid land-rent document in Nepal? |
| OQ-LR-02 | Is there a legally prescribed format or mandatory content for land-rent/lease agreements? |
| OQ-LR-03 | What privacy regulations apply to the storage of personal and property data? |
| OQ-LR-04 | Are system-generated documents (printed from a digital system) legally acceptable for notarization? |
| OQ-LR-05 | What are the evidentiary requirements for digital records in Nepal? |

### 19.3 Document Template Questions

| ID | Question |
|---|---|
| OQ-DT-01 | What is the exact structure of a typical land-rent document in Nepal? |
| OQ-DT-02 | What clauses are standard, and which are conditional? |
| OQ-DT-03 | What variable fields are required? |
| OQ-DT-04 | Are there different templates for different types of rental situations (residential, agricultural, commercial)? |
| OQ-DT-05 | What is the expected document length and formatting? |

### 19.4 User Workflow Questions

| ID | Question |
|---|---|
| OQ-UW-01 | Does the operator prefer to work on a mobile device, tablet, or desktop? |
| OQ-UW-02 | What is the typical turnaround time for a land-rent document? |
| OQ-UW-03 | Does the operator work alone or with assistants? |
| OQ-UW-04 | Does the operator need access to cases created by other operators? |
| OQ-UW-05 | How do operators currently handle document corrections and revisions? |

### 19.5 Data Questions

| ID | Question |
|---|---|
| OQ-DA-01 | What is the complete set of data fields required for a land-rent document? |
| OQ-DA-02 | Which fields come from source documents, and which from the client directly? |
| OQ-DA-03 | Should source documents be retained after finalization? |
| OQ-DA-04 | Should draft versions be retained? |

### 19.6 Security / Privacy Questions

| ID | Question |
|---|---|
| OQ-SP-01 | What authentication method is appropriate for the operators (PIN, password, biometric)? |
| OQ-SP-02 | Should the system encrypt data at rest? |
| OQ-SP-03 | Should the system encrypt data in transit? |
| OQ-SP-04 | What data retention period is legally and practically appropriate? |

### 19.7 Technical Research Questions

| ID | Question |
|---|---|
| OQ-TR-01 | What OCR engines/libraries support Nepali (Devanagari) script? |
| OQ-TR-02 | What is the expected OCR accuracy for printed land documents? |
| OQ-TR-03 | Is OCR for handwritten text feasible? |
| OQ-TR-04 | What document-generation libraries support Nepali script output in PDF? |
| OQ-TR-05 | Should the application operate online, offline, or support both? |

### 19.8 Product Scope Questions

| ID | Question |
|---|---|
| OQ-PS-01 | Should OCR be included in the MVP, or should the initial release support manual entry only? | **RESOLVED (Decision 009)** — manual entry only in the MVP; OCR is a future enhancement required before full deployment. |
| OQ-PS-02 | Should the system support multiple operators in the first release? |
| OQ-PS-03 | Should the system serve NRN (Non-Resident Nepali) users? |
| OQ-PS-04 | Is there a market need for a desktop/Web version, or is mobile sufficient? |

### 19.9 Case, Client, and Document Model Questions

> Added in the v0.1.1 synchronization revision. These questions are also tracked in `00 - Project Control/Open Questions.md`.

| ID | Question |
|---|---|
| OQ-CM-01 | What is the exact Case classification taxonomy beyond LAND_RENT? Which future Case Types are planned? |
| OQ-CM-02 | How is "Agriculture" (or any similar term) classified: a Case Type, a property use purpose, or a directory/category? The Land Rent template currently treats it as a property use purpose (PROP_USE_PURPOSE), not a Case Type. |
| OQ-CM-03 | What is the exact retention, archival, backup, and deletion policy for finalized cases and finalized documents? |
| OQ-CM-04 | Should Source Documents be stored/associated at the Client level, the Case level, or both? |
| OQ-CM-05 | What rules govern updating a Client's information after a Case has been finalized? |
| OQ-CM-06 | Can finalized Cases ever be archived (moved out of the active directory)? Under what criteria? |
| OQ-CM-07 | What are the backup requirements for Case, Client, and Source Document data? |
| OQ-CM-08 | What is the deletion policy for Cases, Clients, and Documents? |
| OQ-CM-09 | What is the exact access-control model (roles, permissions) for Case, Client, and Document data? |

---

## 20. Requirements Traceability

### 20.1 Traceability Structure

| Source | Domain Finding | Requirement(s) | Validation Status |
|---|---|---|---|
| Product vision | Case management | FR-004 to FR-008 | [PROPOSED] — not yet validated |
| Product vision | Source document capture | FR-009 to FR-012 | [PROPOSED] — not yet validated |
| Product vision | OCR / extraction | FR-013 to FR-015, OCR-001 to OCR-006 | [PROPOSED] — requires technical research |
| Product vision | Human verification | FR-016 to FR-019 | [PROPOSED] — not yet validated |
| Product vision | Document generation | FR-021 to FR-026, DG-001 to DG-003 | [PROPOSED] — requires template analysis |
| Product vision | Finalization | FR-027 to FR-031 | [PROPOSED] — not yet validated |
| Domain research | Nepali language requirement | FR-022, DG-002 | [RESEARCH-BACKED] — requires confirmation |
| Domain research | Witness requirement (candidate rule) | BR-008 | [UNVERIFIED — CANDIDATE DOMAIN RULE] |
| Domain research | Rent threshold for written agreement (candidate rule) | BR-009 | [UNVERIFIED — CANDIDATE DOMAIN RULE] |
| Domain research | Registration thresholds (candidate rule) | BR-010 | [UNVERIFIED — CANDIDATE DOMAIN RULE] |
| Product decision 004 | Persistent cases; recent cases; open existing case; case metadata | FR-036, FR-037, FR-039, FR-040; BR-014 | [PROPOSED] — product decision |
| Product decision 005 | Case Type classification; case directory | FR-035, FR-038; BR-015, BR-016 | [PROPOSED] — product decision |
| Product decision 006 | Client management; client reuse; client source documents | FR-041 to FR-047; BR-017, BR-018 | [PROPOSED] — product decision |
| Product decision 007, 008 | Distinct document types; human finalization authority | FR-048, FR-049; BR-019 | [PROPOSED] — product decision |

### 20.2 Requirements Without Validated Source

| Requirement | Source |
|---|---|
| Most proposed functional requirements | Product vision only — source not yet validated |
| Authentication mechanism | Reasonable practice — not domain-validated |
| Specific search criteria (FR-033) | Domain inference — not domain-validated |
| UI language preference (NFR-009) | Domain inference — not domain-validated |
| Performance targets | Not specified — [TO BE DETERMINED] |

---

## 21. Requirement Status Summary

| Category | Count |
|---|---|
| Functional Requirements | 50 (FR-001..FR-049 plus FR-012a) |
| Non-Functional Requirements | 13 (SRS §8; the [[../Non-Functional Requirements/Non-Functional Requirements|Non-Functional Requirements]] document separately maintains 25 NFRs under a different ID scheme) |
| OCR-Specific Requirements (conditional) | 6 |
| Document Generation Requirements | 3 |
| Business Rules | 19 (13 original + 6 product-decision rules; 3 candidate domain rules remain [UNVERIFIED — CANDIDATE DOMAIN RULE]) |
| Assumptions | 10 |
| Risks | 10 |
| Open Questions | 46 |
| **Total Requirements (FR + NFR + OCR + DG + BR)** | **91** |

> Counts updated in the v0.1.1 synchronization revision (new FR-035..FR-049, BR-014..BR-019, OQ-CM-01..09). BR-014..BR-019 are product-decision business rules.

### By Status

Status counts below cover FR + NFR as written in this SRS (63 requirements). Business rules are listed separately.

| Status | Count (FR + NFR) |
|---|---|
| [CONFIRMED] | 0 (2 business rules confirmed: BR-001, BR-004) |
| [RESEARCH-BACKED] | 0 (previously BR-008, BR-009, BR-010 — reclassified) |
| [PROPOSED] | 57 |
| [ASSUMPTION] | 1 (NFR-007) |
| [TO BE VALIDATED] | 3 (FR-011, FR-022, NFR-009) |
| [OPEN QUESTION] | 2 (NFR-003, NFR-005) |
| [UNVERIFIED — CANDIDATE DOMAIN RULE] | 3 (BR-008, BR-009, BR-010) — not counted in FR + NFR total |

> Note: These counts are approximate and will change as requirements are validated, refined, or discovered.

---

## 22. Next Steps

Based on the current state of the SRS (v0.1.1 requirements synchronization revision), the following activities are recommended:

### Short Term (Next Actions)

1. **Analyze the actual land-rent document template.**
   - Obtain one or more representative land-rent document templates.
   - Identify all fields, clauses, and conditional sections.
   - Update the SRS with template-specific requirements.

2. **Conduct domain expert interview.**
   - Use the interview instrument in `01 - Domain Research/Domain Expert Interview - Land Rent.md`.
   - Validate the proposed workflow, identify gaps, and refine requirements.

3. **Map fields to source documents.**
   - For each data field in the template, identify which source document provides it.
   - Identify fields that typically require client verbal input.

4. **Begin technical research (Phase 0.8).**
   - Evaluate OCR options for Nepali (Devanagari) text.
   - Determine OCR feasibility for the MVP.

5. **Validate the Case & Client model additions (FR-035..FR-049, BR-014..BR-019).**
   - Resolve OQ-CM-01..09 (see [[Open Questions]]).
   - Validate the classification taxonomy, retention/archival policy, and client data model with domain experts.

6. **Create the traceability artifacts** for the Case, Client, and Document requirements (see `Traceability/`).

### Medium Term

7. **Refine functional requirements** based on interview and template analysis findings.
8. **Conduct targeted legal/domain research** to resolve open questions.
9. **Update the SRS** to version 0.2 or higher.
10. **Begin requirements validation** with domain experts and the project owner.
11. **Baseline SRS v1.0** after sufficient validation.

---

*End of SRS v0.1.1 Working Draft*
