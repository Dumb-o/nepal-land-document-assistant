# Non-Functional Requirements

> **Status:** Working Draft
>
> This document defines the non-functional requirements (NFRs) for the **Nepal Land Document Assistant — Land-Rent Document Preparation Module** MVP.
>
> These requirements are derived from:
> - **Existing SRS** (`03 - Requirements/SRS/SRS.md`) — legacy NFR-001..NFR-013
> - **Use Cases** (`03 - Requirements/Use Cases.md`) — operator characteristics and workflow
> - **Data Needs** (`03 - Requirements/Business Rules/Data Needs.md`) — data sensitivity and lifecycle
> - **Business Rules** (`03 - Requirements/Business Rules/Business Rules.md`) — access and integrity rules
> - **Functional Requirements** (`03 - Requirements/Functional Requirements.md`) — FR-LR-* behaviors they qualify
>
> **Relationship to the SRS:** The SRS (v0.1) is **not modified** by this task. Legacy SRS NFR IDs are preserved and mapped to the new IDs below (see §2).
>
> **Measurability note:** Only qualitative NFRs are defined. No numerical targets (response times, availability percentages, user counts) are specified because the project documentation does not yet support them. Where a target is needed, the requirement is marked **[TO BE VALIDATED]**.

---

## 1. ID Scheme and Conventions

- **Non-functional requirement IDs:** `NFR-<CAT>-###`, where `<CAT>` is a category code (SEC, PRI, DAT, USE, REL, PER, ACC, MNT, BAC, AUD).
- **Priority levels:** MUST / SHOULD / COULD.
- **Status levels:** CONFIRMED / PROPOSED / TO BE VALIDATED / OPEN QUESTION.
- **Verification methods:** Inspection / Test / Demonstration / Analysis.
- **MVP context:** A small number of authorized operators prepare land-rent documents on a mobile tablet/smartphone (proposed). The system is human-in-the-loop; it does not independently determine legal validity.

---

## 2. Mapping from Existing SRS NFR IDs

| Legacy SRS ID | New ID(s) | Notes |
|---|---|---|
| NFR-001 (Security) | NFR-SEC-001 | Protect stored case/document data |
| NFR-002 (Security) | NFR-SEC-002 | Authentication before access |
| NFR-003 (Privacy) | NFR-PRI-001, NFR-PRI-002 | Personal data handling principles |
| NFR-004 (Performance) | NFR-PER-001 | Responsive interactions |
| NFR-005 (Availability) | NFR-REL-001 | Deployment-dependent availability |
| NFR-006 (Reliability) | NFR-REL-002 | Data integrity during use |
| NFR-007 (Usability) | NFR-USE-001, NFR-USE-002 | Varying technical experience |
| NFR-008 (Usability) | NFR-USE-003 | Mobile/tablet touchscreen |
| NFR-009 (Usability) | NFR-USE-004 | Nepali language interface |
| NFR-010 (Maintainability) | NFR-MNT-001 | Template updates without code changes |
| NFR-011 (Auditability) | NFR-AUD-001 | Logs for event reconstruction |
| NFR-012 (Data Integrity) | NFR-DAT-002 | Concurrent modification prevention |
| NFR-013 (Backup and Recovery) | NFR-BAC-001 | Regular backup support |

---

## 3. Detailed Non-Functional Requirements

### NFR-SEC — Security

### NFR-SEC-001 — Protect Stored Case and Document Data

**Requirement:**
The system shall protect stored case data and documents from unauthorized access.

**Priority:** MUST

**Status:** PROPOSED

**Rationale:**
The system handles personal identity information (names, citizenship numbers) and property records.

**Verification Method:** Inspection / Test

**Acceptance Criteria:**
- Unauthorized users cannot access stored case data or documents.
- Access to stored data is mediated by the authorization controls in FR-LR-002.
- [TO BE DETERMINED] Specific protection mechanisms (encryption at rest, etc.) require security research.

---

### NFR-SEC-002 — Require Authentication Before Access

**Requirement:**
The system shall require operator authentication before access to any case data.

**Priority:** MUST

**Status:** PROPOSED

**Rationale:**
Authentication gates access to sensitive data (FR-LR-001).

**Verification Method:** Test

**Acceptance Criteria:**
- No case data is reachable without successful authentication.
- Authentication is enforced consistently across all data access paths.

---

### NFR-SEC-003 — Secure Handling of Credentials

**Requirement:**
The system shall store and handle authentication credentials securely.

**Priority:** MUST

**Status:** PROPOSED

**Rationale:**
Compromised credentials would grant unauthorized access to sensitive case data.

**Verification Method:** Inspection

**Acceptance Criteria:**
- Credentials are not stored in plain text.
- Credentials are never displayed or logged in full.
- The authentication mechanism (PIN / password / biometric) is [TO BE DETERMINED].

---

### NFR-SEC-004 — Protect Information During Transfer

**Requirement:**
Where data is transmitted between system components or devices, the system shall protect that data from interception.

**Priority:** SHOULD

**Status:** OPEN QUESTION

**Rationale:**
Transmission protection depends on the deployment model (online / offline / hybrid), which is not yet decided.

**Verification Method:** Analysis

**Acceptance Criteria:**
- If any remote transmission occurs, it is protected against interception.
- This requirement is subject to the deployment-model decision.

---

### NFR-PRI — Privacy

### NFR-PRI-001 — Limit Access to Personal Information

**Requirement:**
The system shall limit access to personal and property information to authorized operators.

**Priority:** MUST

**Status:** PROPOSED

**Rationale:**
The system processes citizenship numbers, names, addresses, and property records.

**Verification Method:** Test

**Acceptance Criteria:**
- Personal information is accessible only to authenticated, authorized operators.
- Information is not exposed to indirect stakeholders (e.g., clients) through the system.

---

### NFR-PRI-002 — Avoid Unnecessary Retention

**Requirement:**
The system shall not retain personal or sensitive information beyond what is necessary for the documented purpose and applicable requirements.

**Priority:** SHOULD

**Status:** PROPOSED

**Rationale:**
Minimizing retained data reduces privacy risk (data minimization principle, SRS §13.3).

**Verification Method:** Inspection

**Acceptance Criteria:**
- Retention of each artifact type (source documents, Candidate Data, drafts, finalized documents, audit logs) is defined or explicitly left open.
- Exact retention periods are [TO BE DETERMINED]; no retention periods are invented here.
- Where retention is unresolved, the corresponding OPEN QUESTION is referenced (SRS §10.10; Data Needs OQ-DN-06).

---

### NFR-PRI-003 — Protect Information During Transfer (Privacy)

**Requirement:**
The system shall protect personal information during transfer wherever transfer occurs.

**Priority:** SHOULD

**Status:** OPEN QUESTION

**Rationale:**
Duplicates NFR-SEC-004 from a privacy perspective; both depend on the unresolved deployment model.

**Verification Method:** Analysis

**Acceptance Criteria:**
- If transfer occurs, personal information is protected.
- Resolved by the deployment-model decision.

---

### NFR-PRI-004 — Appropriate Handling of Finalized Documents

**Requirement:**
The system shall treat Finalized System Records as completed documents requiring controlled handling.

**Priority:** SHOULD

**Status:** PROPOSED

**Rationale:**
Finalized documents contain personal and property information and are the primary deliverables.

**Verification Method:** Inspection

**Acceptance Criteria:**
- Finalized documents are accessible only to authorized operators (per FR-LR-048, NFR-SEC-001).
- Finalized documents are not silently modified (per FR-LR-037).

---

### NFR-DAT — Data Integrity

### NFR-DAT-001 — Maintain Accuracy of Verified Data

**Requirement:**
The system shall maintain the accuracy of Verified Case Data as confirmed by the operator.

**Priority:** MUST

**Status:** PROPOSED

**Rationale:**
Verified Case Data is the authoritative source for document generation; errors propagate into legally consequential documents.

**Verification Method:** Test

**Acceptance Criteria:**
- Verified Case Data is not altered by generation or retrieval operations.
- Draft edits do not alter Verified Case Data (BR-018).
- Any correction requires operator action (FR-LR-020).

---

### NFR-DAT-002 — Prevent Concurrent Conflicting Modifications

**Requirement:**
The system shall prevent concurrent conflicting modifications to the same case data.

**Priority:** SHOULD

**Status:** PROPOSED

**Rationale:**
Prevents data loss or confusion where more than one operator could work on the same case.

**Verification Method:** Test

**Acceptance Criteria:**
- Concurrent conflicting writes to the same case are prevented or resolved deterministically.
- Depends on whether multi-operator access is an MVP requirement [TO BE VALIDATED].

---

### NFR-DAT-003 — Ensure Consistency Between Case Data and Generated Documents

**Requirement:**
The system shall ensure consistency between Verified Case Data and the documents generated from it.

**Priority:** MUST

**Status:** PROPOSED

**Rationale:**
Generated documents must reflect the verified data the operator approved.

**Verification Method:** Test

**Acceptance Criteria:**
- A draft reflects the Verified Case Data at generation time.
- Regeneration after data changes reflects the updated verified data.
- The template version used is recorded (FR-LR-029).

---

### NFR-DAT-004 — Preserve Integrity of Finalized Documents

**Requirement:**
The system shall not silently alter Finalized System Records.

**Priority:** MUST

**Status:** PROPOSED

**Rationale:**
Finalized documents must be trustworthy and distinguishable from drafts (BR-002, BR-006).

**Verification Method:** Test

**Acceptance Criteria:**
- A finalized record's content is not modified without an explicit, recorded action.
- Finalized records are protected from ordinary accidental modification (FR-LR-037).

---

### NFR-USE — Usability

### NFR-USE-001 — Usable by Operators with Varying Technical Experience

**Requirement:**
The system shall be usable by operators with varying levels of technical experience.

**Priority:** MUST

**Status:** PROPOSED

**Rationale:**
Document-preparation professionals (the project owner's parents are the initial operators) have unknown technical skill levels.

**Verification Method:** Demonstration / Test (user testing)

**Acceptance Criteria:**
- A non-programmer can complete the core workflow with minimal training.
- Core tasks do not require technical terminology or system administration knowledge.

---

### NFR-USE-002 — Provide a Clear and Understandable Workflow

**Requirement:**
The system shall present a clear, understandable workflow to the operator.

**Priority:** MUST

**Status:** PROPOSED

**Rationale:**
The MVP workflow (create case → enter → review → generate → review → finalize → store → retrieve) must be evident to the operator.

**Verification Method:** Demonstration

**Acceptance Criteria:**
- The operator can determine the current step and next step.
- Required vs optional fields are clearly indicated (FR-LR-017).
- Validation and error messages are clear and actionable (FR-LR-044, FR-LR-018).
- The operator can correct mistakes at each stage (FR-LR-020, FR-LR-033).
- Draft and Finalized documents are clearly distinguished (FR-LR-035).

---

### NFR-USE-003 — Support Mobile/Tablet Use

**Requirement:**
[PROPOSED] The primary interface shall be usable on a mobile tablet or smartphone with touch input.

**Priority:** SHOULD

**Status:** PROPOSED

**Rationale:**
The product vision describes a mobile-first application, but this has not been confirmed with users.

**Verification Method:** Demonstration / Test

**Acceptance Criteria:**
- Core workflow tasks are completable with touch input.
- Forms are usable on tablet-sized and phone-sized screens.

---

### NFR-USE-004 — Support Nepali Language in the Interface

**Requirement:**
The system interface should support the Nepali language. Whether the UI itself is Nepali, English, or bilingual is [TO BE VALIDATED].

**Priority:** SHOULD

**Status:** TO BE VALIDATED

**Rationale:**
Operators in Nepal may prefer Nepali, English, or a combination. Generated documents are Nepali regardless (FR-LR-028).

**Verification Method:** Inspection / Test

**Acceptance Criteria:**
- The UI language preference is confirmed with domain experts.
- Any Nepali text in the UI renders correctly in Devanagari.

---

### NFR-REL — Reliability

### NFR-REL-001 — Provide Availability Appropriate to the Deployment Model

**Requirement:**
[TO BE DETERMINED] Availability requirements depend on the deployment model (online, offline, or hybrid).

**Priority:** TBD

**Status:** OPEN QUESTION

**Rationale:**
Offline operation may be required in areas with limited connectivity.

**Verification Method:** Analysis

**Acceptance Criteria:**
- Availability requirements are defined once the deployment model is decided.
- Whether the MVP requires offline or degraded-connectivity operation is [OPEN QUESTION].

---

### NFR-REL-002 — Preserve Data Integrity During Use

**Requirement:**
The system shall preserve data integrity during use, particularly during document finalization.

**Priority:** SHOULD

**Status:** PROPOSED

**Rationale:**
Data loss or corruption during finalization could result in rework or document errors.

**Verification Method:** Test

**Acceptance Criteria:**
- Failed operations do not corrupt existing case data or finalized documents (FR-LR-046, FR-LR-047).
- A failed finalization does not produce a partial finalized record.

---

### NFR-PER — Performance

### NFR-PER-001 — Provide Responsive Interactions

**Requirement:**
The system should provide responsive interactions suitable for normal document-preparation workflows.

**Priority:** SHOULD

**Status:** TO BE VALIDATED

**Rationale:**
Operators should not be significantly delayed by system response times.

**Verification Method:** Test

**Acceptance Criteria:**
- Specific performance targets are [TO BE DETERMINED]; no targets are invented here.
- Common interactions (form entry, navigation, draft viewing) are perceived as responsive by the operator.

---

### NFR-ACC — Accessibility

### NFR-ACC-001 — Support Basic Accessibility

**Requirement:**
[OPEN QUESTION] Specific accessibility requirements have not been identified.

**Priority:** COULD

**Status:** OPEN QUESTION

**Rationale:**
The project documentation (SRS §8.7) has not identified accessibility requirements. These should be considered during design.

**Verification Method:** Analysis

**Acceptance Criteria:**
- Accessibility requirements are identified and documented before design completion.
- No specific accessibility targets are asserted without evidence.

---

### NFR-MNT — Maintainability

### NFR-MNT-001 — Support Template Updates Without Code Changes

**Requirement:**
The system shall support updates to document templates without requiring application code changes.

**Priority:** SHOULD

**Status:** PROPOSED

**Rationale:**
Document templates may change due to legal requirements or practice changes; separating templates from code reduces maintenance burden (FR-LR-043).

**Verification Method:** Demonstration

**Acceptance Criteria:**
- A template change can be applied without modifying application code.
- Template changes are versioned and do not affect documents generated from earlier versions.

---

### NFR-MNT-002 — Support Configuration Without Code Changes

**Requirement:**
The system should allow configuration (e.g., field labels, use-purpose options) to be changed without code changes where practical.

**Priority:** COULD

**Status:** PROPOSED

**Rationale:**
Domain terminology and options may evolve; reducing code coupling improves maintainability.

**Verification Method:** Demonstration

**Acceptance Criteria:**
- Configuration changes are feasible without code changes where identified.
- This requirement is deliberately modest; no complex configuration framework is assumed.

---

### NFR-BAC — Backup and Recovery

### NFR-BAC-001 — Support Backup of Case Data and Documents

**Requirement:**
The system shall support regular backup of case data and finalized documents.

**Priority:** SHOULD

**Status:** PROPOSED

**Rationale:**
Data loss could result in significant work being lost.

**Verification Method:** Test

**Acceptance Criteria:**
- Case data and finalized documents are included in backups.
- Backup frequency and method are [TO BE DETERMINED]; no backup schedule is invented here.
- Backups containing case data are protected with access controls consistent with live data (SRS §13.9).

---

### NFR-BAC-002 — Support Recovery of Finalized Documents

**Requirement:**
The system shall support recovery of finalized documents from backup after data loss.

**Priority:** SHOULD

**Status:** PROPOSED

**Rationale:**
Finalized documents are the primary deliverables and must survive data loss events.

**Verification Method:** Test

**Acceptance Criteria:**
- Finalized documents can be restored from backup.
- Restoration is verified through a documented recovery procedure.

---

### NFR-AUD — Auditability

### NFR-AUD-001 — Maintain Logs for Event Reconstruction

**Requirement:**
The system shall maintain logs that allow reconstruction of significant events (case creation, document generation, finalization, access to finalized documents).

**Priority:** SHOULD

**Status:** PROPOSED

**Rationale:**
Supports accountability and potential evidentiary needs (FR-LR-042).

**Verification Method:** Test

**Acceptance Criteria:**
- Significant events are logged with timestamp, operator identity, and case/document reference.
- The exact set of audited events is [TO BE VALIDATED] and is not expanded beyond the MVP's needs.

---

## 4. NFR Summary by Category

| Category | NFR IDs | Count |
|---|---|---|
| NFR-SEC — Security | NFR-SEC-001..NFR-SEC-004 | 4 |
| NFR-PRI — Privacy | NFR-PRI-001..NFR-PRI-004 | 4 |
| NFR-DAT — Data Integrity | NFR-DAT-001..NFR-DAT-004 | 4 |
| NFR-USE — Usability | NFR-USE-001..NFR-USE-004 | 4 |
| NFR-REL — Reliability | NFR-REL-001, NFR-REL-002 | 2 |
| NFR-PER — Performance | NFR-PER-001 | 1 |
| NFR-ACC — Accessibility | NFR-ACC-001 | 1 |
| NFR-MNT — Maintainability | NFR-MNT-001, NFR-MNT-002 | 2 |
| NFR-BAC — Backup and Recovery | NFR-BAC-001, NFR-BAC-002 | 2 |
| NFR-AUD — Auditability | NFR-AUD-001 | 1 |
| **Total** | | **25** |

---

## 5. Traceability

| NFR ID | Related FR | Related BR | Related DN | Legacy SRS |
|---|---|---|---|---|
| NFR-SEC-001 | FR-LR-002, FR-LR-048 | BR-003, BR-015 | DN-CASE-01 | NFR-001 |
| NFR-SEC-002 | FR-LR-001 | BR-003 | — | NFR-002 |
| NFR-SEC-003 | FR-LR-001 | — | — | NFR-001, NFR-002 |
| NFR-SEC-004 | FR-LR-001 | — | — | §13.5 |
| NFR-PRI-001 | FR-LR-002, FR-LR-048 | BR-003 | DN-P1-08, DN-P2-08 | NFR-003 |
| NFR-PRI-002 | — | — | DN-SRC-05, DN-LIFE-01 | §13.3 |
| NFR-PRI-003 | — | — | — | §13.5 |
| NFR-PRI-004 | FR-LR-037, FR-LR-048 | BR-006 | DN-LIFE-04 | — |
| NFR-DAT-001 | FR-LR-021 | BR-018 | DN-LIFE-02 | NFR-006 |
| NFR-DAT-002 | — | — | DN-LIFE-02 | NFR-012 |
| NFR-DAT-003 | FR-LR-023, FR-LR-024 | — | DN-LIFE-02 | — |
| NFR-DAT-004 | FR-LR-037 | BR-002, BR-006 | DN-LIFE-04 | NFR-006 |
| NFR-USE-001 | FR-LR-010..FR-LR-016 | — | — | NFR-007 |
| NFR-USE-002 | FR-LR-017, FR-LR-019, FR-LR-035 | — | — | NFR-007 |
| NFR-USE-003 | — | — | — | NFR-008 |
| NFR-USE-004 | FR-LR-028 | — | — | NFR-009 |
| NFR-REL-001 | — | — | — | NFR-005 |
| NFR-REL-002 | FR-LR-046, FR-LR-047 | — | DN-LIFE-04 | NFR-006 |
| NFR-PER-001 | — | — | — | NFR-004 |
| NFR-ACC-001 | — | — | — | §8.7 |
| NFR-MNT-001 | FR-LR-043 | — | DN-DOC-05 | NFR-010 |
| NFR-MNT-002 | FR-LR-043 | — | — | — |
| NFR-BAC-001 | FR-LR-038 | — | DN-LIFE-04 | NFR-013 |
| NFR-BAC-002 | FR-LR-038 | — | DN-LIFE-04 | NFR-013 |
| NFR-AUD-001 | FR-LR-042 | — | DN-LIFE-05 | NFR-011 |

---

## 6. Requirement Quality Issues

### Ambiguous Requirements
| ID | Issue |
|---|---|
| NFR-USE-001 | "Minimal training" is not quantified; acceptable as a qualitative requirement for the MVP but flagged for user testing. |
| NFR-PER-001 | No numerical target; intentionally qualitative pending [TO BE DETERMINED] targets. |

### Duplicate / Overlapping Requirements
| ID | Issue |
|---|---|
| NFR-SEC-004 vs NFR-PRI-003 | Both address transfer protection. Kept as two views (security vs privacy) of the same underlying concern; recommend merging during SRS consolidation. |
| NFR-SEC-001 vs NFR-PRI-001 | Overlapping (both limit access). Distinct focus (data protection vs privacy principle); consider consolidation in SRS pass. |

### Conflicting Requirements
| ID | Issue |
|---|---|
| NFR-REL-001 (availability) | Status is OPEN QUESTION because the deployment model is undecided; conflicts with any implicit online-only assumption. Recorded, not resolved. |

### Unsourced Requirements
| ID | Issue |
|---|---|
| NFR-MNT-002 | Not directly sourced from the SRS or existing artifacts; derived from maintainability good practice. Flagged as [PROPOSED] and weakly sourced. |

### Requirements Requiring Validation
| ID | Issue |
|---|---|
| NFR-USE-004 (Nepali UI), NFR-PER-001 (targets), NFR-ACC-001 (accessibility), NFR-REL-001 (availability) | Require domain/user research and the deployment-model decision before targets or scope can be finalized. |

### Requirements That May Belong Elsewhere
| ID | Issue |
|---|---|
| NFR-AUD-001 | Overlaps FR-LR-042 (functional audit events). The logging capability is non-functional; the event catalog is functional. To be reconciled during SRS consolidation. |
| NFR-USE-002 | Contains some functional-sounding criteria (field indication, draft/finalized distinction) that are defined functionally in FR-LR-017, FR-LR-035; kept here as usability qualities. |

---

*End of Non-Functional Requirements — Working Draft.*
