# Project Roadmap

***
**Status:** Living Document  
**Last Updated:** 2026-08-13
***

## Phases

### Phase 0 — Documentation & Research (Current)

Phase 0 is organized into ten internal workstreams. The dependency chain is:

```
0.1 Project & Repository Setup
        ↓
0.2 Domain Research
        ↓
0.3 Sample Document Analysis
        ↓
0.4 Requirements Engineering
        ↓
0.5 SRS Development
        ↓
0.6 System Design
        ↓
0.7 UML Modeling
        ↓
0.8 Technical Research / 0.9 Architecture Decisions
        ↓
0.10 UI/UX Foundations
        ↓
Phase 1 — Design & Prototyping
```

Some workstreams may begin early once their prerequisites are satisfied. For example, UML modeling can start with preliminary models during requirements analysis, and technical research can begin during requirements engineering when a requirement surfaces a technical question.

---

#### 0.1 — Project & Repository Setup
- **Status:** Complete
- **Objective:** Establish the repository structure, documentation vault, and project conventions so that all subsequent work has a consistent home.
- **Activities:**
  - Initialize Git repository
  - Create Obsidian vault directory skeleton with numbered topical folders
  - Write root `README.md` with project overview, phase status, and roadmap
  - Create core control documents (Project Overview, Roadmap, Open Questions, Decision Log, Glossary)
  - Define Markdown and naming conventions
- **Expected Artifacts:**
  - Repository with `docs/obsidian-vault/` structure
  - Root `README.md`
  - Control documents in `00 - Project Control/`
- **Dependencies:** None
- **Completion Criteria:** All directory folders exist, all control documents are written and reviewed.

---

#### 0.2 — Domain Research
- **Status:** Complete (primary artifact `01 - Domain Research/Domain Overview.md`; not all listed sub-artifacts were produced)
- **Objective:** Build a foundational understanding of Nepali land documentation, the stakeholders involved, the legal and administrative context, and common workflows.
- **Activities:**
  - Research types of land documents used in Nepal (title deeds, land revenue receipts, cadastral maps, etc.)
  - Identify government bodies and their roles (Survey Department, Land Revenue Office, Malpot, etc.)
  - Document typical land transaction workflows
  - Research relevant legal frameworks (without legal interpretation)
  - Identify common data fields, terminology, and document formats
  - Capture sources and references
- **Expected Artifacts:**
  - `01 - Domain Research/Domain Overview.md`
  - `01 - Domain Research/Stakeholder Map.md`
  - `01 - Domain Research/Typical Workflows.md`
  - `01 - Domain Research/Terminology Reference.md`
  - Updates to Project Glossary
  - Updates to Open Questions
- **Dependencies:** 0.1 Project & Repository Setup
- **Completion Criteria:** Domain overview document covers document types, stakeholders, workflows, and terminology. Glossary is updated with domain terms. Open questions are captured.

---

#### 0.3 — Sample Document Analysis
- **Status:** Complete (primary artifact `02 - Document Analysis/Land Rent Template Analysis.md`; not all listed sub-artifacts were produced)
- **Objective:** Analyze real or representative sample land documents to understand structure, content patterns, data fields, and variability.
- **Activities:**
  - Collect sample documents (anonymized if necessary)
  - For each document type, document structure, sections, and key data fields
  - Identify variations across documents of the same type
  - Note language usage patterns (Nepali, English, mixed)
  - Document potential OCR challenges (handwriting, stamps, seals, table structures)
  - Capture findings in structured analysis documents
- **Expected Artifacts:**
  - `02 - Document Analysis/Document Type Catalog.md`
  - `02 - Document Analysis/[Document Type] Analysis.md` (one per type)
  - `02 - Document Analysis/Common Field Inventory.md`
  - `02 - Document Analysis/OCR Challenge Notes.md`
- **Dependencies:** 0.2 Domain Research
- **Completion Criteria:** At least one representative document per identified type has been analyzed. Field inventory is compiled. OCR challenges are noted.

---

#### 0.4 — Requirements Engineering
- **Status:** In Progress (draft artifacts exist; pending review — see note below)
- **Objective:** Elicit, categorize, and document functional requirements, non-functional requirements, and business rules derived from domain research and document analysis.
- **Activities:**
  - Elicit functional requirements from domain workflows and document analysis
  - Identify non-functional requirements (performance, security, usability, reliability)
  - Document business rules inherent to the domain
  - Trace requirements back to source documents and research findings
  - Establish a requirement ID scheme
  - Review and refine requirements for consistency
  - Synchronize requirements with product decisions (persistent Cases, Client concept, typed documents)
- **Expected Artifacts:**
  - `03 - Requirements/Functional Requirements/`
  - `03 - Requirements/Non-Functional Requirements/`
  - `03 - Requirements/Business Rules/`
  - `03 - Requirements/Use Cases.md`
  - `03 - Requirements/Data Needs.md`
  - `03 - Requirements/Traceability/`
  - Updated Open Questions
  - Input to Decision Log
- **Dependencies:** 0.2 Domain Research, 0.3 Sample Document Analysis
- **Completion Criteria:** All requirements are captured, categorized, and reviewed. Each requirement has a unique ID, description, and source reference. A requirements-synchronization pass reflecting agreed product decisions has been performed.
- **Note:** Draft requirements artifacts exist as of 2026-08-08 but are **not** baselined; they remain pending review and acceptance.
- **Note (2026-08-13):** Initial prototype scope agreed as LAND_RENT with **agricultural use purpose only** ([[../00 - Project Control/Decision Log|Decision 010]]); manual-first architecture confirmed ([[../00 - Project Control/Decision Log|Decision 009]]). A vault-wide terminology and scope audit was performed; follow-up corrections are tracked via this roadmap and the [[../00 - Project Control/Open Questions|Open Questions]].

---

#### 0.5 — SRS Development
- **Status:** In Progress (draft SRS exists; updated 2026-08-08 as a requirements-synchronization revision, not baselined)
- **Objective:** Synthesize the requirements into a structured Software Requirements Specification document.
- **Activities:**
  - Create SRS document structure following a standard template
  - Import and organize functional and non-functional requirements
  - Define system scope, context, and interfaces
  - Define user classes and characteristics
  - Document assumptions and dependencies
  - Review SRS for completeness and consistency
- **Expected Artifacts:**
  - `03 - Requirements/SRS/SRS.md`
- **Dependencies:** 0.4 Requirements Engineering
- **Completion Criteria:** SRS document is complete and reviewed. All requirements are included and traceable.

---

#### 0.6 — System Design
- **Status:** Pending
- **Objective:** Produce a high-level system design that defines system boundaries, major components, data flow, and interfaces based on the requirements.
- **Activities:**
  - Define system context and external interfaces
  - Identify major subsystems or modules
  - Describe data flow between components
  - Define API boundaries and integration points
  - Document high-level data model
  - Consider deployment architecture at a conceptual level
- **Expected Artifacts:**
  - `04 - System Design/System Context.md`
  - `04 - System Design/Architecture Overview.md`
  - `04 - System Design/Data Flow.md`
  - `04 - System Design/Module Descriptions.md`
  - Preliminary data model in `06 - Data Design/`
- **Dependencies:** 0.5 SRS Development
- **Completion Criteria:** System context, component architecture, and data flow are documented. Modules are identified and described.

---

#### 0.7 — UML Modeling
- **Status:** Pending
- **Objective:** Model the system from multiple perspectives using UML diagrams, described with Mermaid syntax for embedding in Obsidian.
- **Activities:**
  - Create use case diagrams from functional requirements
  - Model key workflows as activity diagrams
  - Develop sequence diagrams for critical interactions
  - Derive class diagrams from the data model
  - Model state diagrams for entities with significant lifecycle
  - Create component diagrams showing system structure
  - Create deployment diagrams at a conceptual level
- **Expected Artifacts:**
  - `05 - UML/Use Case Diagrams/`
  - `05 - UML/Activity Diagrams/`
  - `05 - UML/Sequence Diagrams/`
  - `05 - UML/Class Diagrams/`
  - `05 - UML/State Diagrams/`
  - `05 - UML/Component Diagrams/`
  - `05 - UML/Deployment Diagrams/`
- **Dependencies:** 0.4 Requirements Engineering (preliminary models), 0.6 System Design (detailed models)
- **Completion Criteria:** At least one diagram exists in each UML category. Diagrams are consistent with the SRS and system design.

---

#### 0.8 — Technical Research
- **Status:** Pending
- **Objective:** Investigate source-document capture and OCR feasibility for Nepali (Devanagari) text (a pre-deployment requirement per Decision 009) and document-generation solutions, producing recommendations. OCR/capture are proposed enhancements, never prerequisites — the system functions on manual entry alone.
- **Activities:**
  - Evaluate OCR engines for Devanagari script support (research candidates only — Tesseract, Google Cloud Vision, Azure OCR, etc.; no selection is made here)
  - Evaluate source-document capture mechanisms (camera, file upload) for full deployment
  - Test OCR accuracy on sample documents if feasible
  - Research document-generation libraries and tools (PDF generation, templating, etc.)
  - Evaluate output format support (PDF, DOCX, etc.)
  - Consider offline vs. online processing requirements
  - Document findings and trade-offs
- **Expected Artifacts:**
  - `07 - OCR/OCR Research.md`
  - `07 - OCR/OCR Candidate Comparison.md`
  - `08 - Document Generation/Document Generation Research.md`
  - `08 - Document Generation/DocGen Candidate Comparison.md`
- **Dependencies:** 0.3 Sample Document Analysis (for OCR test data), may begin during 0.4 Requirements Engineering
- **Completion Criteria:** OCR/capture and document-generation candidates are identified, compared, and findings documented. Recommendations are ready for architecture decisions. OCR/capture feasibility must be established before full deployment (Decision 009).

---

#### 0.9 — Architecture Decisions
- **Status:** Pending
- **Objective:** Capture all significant architectural decisions with rationale, alternatives considered, and consequences.
- **Activities:**
  - Identify decisions that need to be made (technology, patterns, tools)
  - For each decision, document the context, options, decision, and rationale
  - Use Architecture Decision Record (ADR) format
  - Link decisions to requirements and design documents
  - Review and socialize decisions
- **Expected Artifacts:**
  - `11 - Architecture Decisions/ADR-001-[Title].md` and subsequent ADRs
  - Updated Decision Log
- **Dependencies:** 0.6 System Design, 0.8 Technical Research
- **Completion Criteria:** All pending architectural decisions have ADR documents. Decision Log is up to date.

---

#### 0.10 — UI/UX Foundations
- **Status:** Pending
- **Objective:** Establish UI/UX principles, user personas, and high-level screen flows without detailed design.
- **Activities:**
  - Define target user personas based on domain research
  - Identify primary user goals and tasks
  - Document user journey maps for key workflows
  - Define UI principles and design constraints
  - Create low-level screen flow diagrams
  - Research target platform constraints (mobile, web, etc.)
- **Expected Artifacts:**
  - `09 - UI UX/User Personas.md`
  - `09 - UI UX/User Journeys.md`
  - `09 - UI UX/UI Principles.md`
  - `09 - UI UX/Screen Flows.md`
- **Dependencies:** 0.2 Domain Research, 0.4 Requirements Engineering (user needs), 0.6 System Design (system boundaries)
- **Completion Criteria:** Personas, user journeys, UI principles, and screen flows are documented. Detailed wireframing is deferred to Phase 1.

---

### Phase 1 — Design & Prototyping
- [ ] Refine UML models based on feedback
- [ ] Create detailed UI/UX wireframes and prototypes
- [ ] Validate designs with stakeholders
- [ ] Finalize technology stack recommendation
- [ ] Build proof-of-concept prototypes

### Phase 2 — Implementation
- [ ] Set up development environment
- [ ] Implement backend services
- [ ] Implement frontend (mobile/web)
- [ ] Integrate document generation
- [ ] Implement business rules
- [ ] Integrate source-document capture and OCR capabilities (required before full deployment; gated on Phase 0.8 research, Decision 009)

### Phase 3 — Testing & Deployment
- [ ] Unit and integration testing
- [ ] User acceptance testing
- [ ] Staging deployment
- [ ] Production deployment
- [ ] Operational documentation and runbooks

## Milestones

| Milestone | Target |
|---|---|
| Vault structure complete | Done |
| Domain research complete | Done |
| Document analysis complete | Done |
| Prototype scope agreed (LAND_RENT, agricultural use purpose) | Done — 2026-08-13 (Decision 010) |
| Requirements baselined | TBD |
| SRS complete | TBD |
| System design complete | TBD |
| UML modeling complete | TBD |
| Technical research complete | TBD |
| Architecture decisions captured | TBD |
| UI/UX foundations complete | TBD |
| Design review completed | TBD |
| First prototype | TBD |
