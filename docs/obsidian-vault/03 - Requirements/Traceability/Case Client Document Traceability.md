---
title: Case, Client, and Document Type Traceability
status: in-progress
date: 2026-08-08
---

# Case, Client, and Document Type Traceability

> Traceability artifact for the requirements added in the v0.1.1 synchronization revision (product decisions [[../../00 - Project Control/Decision Log|004–008]]). Links decisions → functional requirements → use cases → data needs → business rules across the requirements documentation.

## 1. Scope

This note covers the requirements introduced or refined by product decisions 004–008:

- **004 — Cases persist after finalization**
- **005 — Case Type classification**
- **006 — Client management**
- **007 — Distinct document types**
- **008 — Human-finalized only (no AI/application finalization)**

For the legacy requirements (FR-001..FR-034, OCR, DG), see the traceability matrix in [[../Functional Requirements/Functional Requirements|Functional Requirements §6]] and the SRS traceability table in [[../SRS/SRS|SRS §20]].

## 2. Decision → Requirement → Artifact Map

### 004 — Persistent Cases

| SRS FR | FR-LR | Use Case | Data Need | Business Rule | Status |
|---|---|---|---|---|---|
| FR-036 | FR-LR-050 | UC-003, UC-014 | DN-CASE-09, DN-LIFE-06 | BR-039, BR-040 | PROPOSED |
| FR-037 | FR-LR-051 | UC-003 | — | — | PROPOSED |
| FR-039 | FR-LR-052 | UC-003, UC-014 | DN-CASE-01 | BR-039 | PROPOSED |
| FR-040 | FR-LR-054 | UC-002, UC-003 | DN-CASE-01..09 | — | PROPOSED |

### 005 — Case Type Classification

| SRS FR | FR-LR | Use Case | Data Need | Business Rule | Status |
|---|---|---|---|---|---|
| FR-035 | FR-LR-049 | UC-002 | DN-CTYPE-01, DN-CASE-06 | BR-041, BR-042 | PROPOSED |
| FR-038 | FR-LR-053 | UC-003, UC-014 | DN-CTYPE-01 | BR-041 | PROPOSED |

### 006 — Client Management

| SRS FR | FR-LR | Use Case | Data Need | Business Rule | Status |
|---|---|---|---|---|---|
| FR-041 | FR-LR-055 | UC-017 | DN-CLI-01..10 | BR-043 | PROPOSED |
| FR-042 | FR-LR-056 | UC-018 | DN-CLI | BR-037, BR-043 | PROPOSED |
| FR-043 | FR-LR-057 | UC-018 | DN-CLI-01, DN-CLI-07 | — | PROPOSED |
| FR-044 | FR-LR-058 | UC-019 | DN-CASE-08 | BR-044 | PROPOSED |
| FR-045 | FR-LR-059 | UC-019 | DN-CLI, DN-CASE-08 | BR-044 | PROPOSED |
| FR-046 | FR-LR-060 | UC-020 | DN-CASE-08 | BR-044 | PROPOSED |
| FR-047 | FR-LR-061 | UC-021 | DN-SRC-06 | BR-045, BR-046 | PROPOSED |

### 007 — Distinct Document Types / 008 — Human Finalization

| SRS FR | FR-LR | Use Case | Data Need | Business Rule | Status |
|---|---|---|---|---|---|
| FR-048 | FR-LR-062 | UC-013, UC-021 | DN-GEN-01, DN-SRC | BR-045 | PROPOSED |
| FR-049 | FR-LR-063 | UC-013, UC-021 | DN-GEN-01 | BR-038, BR-047 | CONFIRMED |

## 3. Use Case Index

| Use Case | Title | Added/Refined |
|---|---|---|
| UC-002 | Create Case | Refined — Case Type at creation |
| UC-003 | List/Manage Cases | Refined — persistent cases, directory |
| UC-014 | Finalize Case | Refined — finalized cases persist |
| UC-017 | Create Client | Added |
| UC-018 | View/Search Client | Added |
| UC-019 | Associate/Reuse Client | Added |
| UC-020 | View Client's Cases | Added |
| UC-021 | Manage Client Source Documents | Added |

## 4. Business Rule Index

| Rule | Title | Status |
|---|---|---|
| BR-037 | Client record lifecycle | PROPOSED |
| BR-038 | Finalization is human decision | CONFIRMED |
| BR-039 | Case persistence after finalization | PROPOSED |
| BR-040 | Case/document retention intent | PROPOSED |
| BR-041 | Case Type classification | PROPOSED |
| BR-042 | Case Type vs property use purpose | PROPOSED |
| BR-043 | Client vs Application User | PROPOSED |
| BR-044 | Client reuse across cases | PROPOSED |
| BR-045 | Source vs generated documents | PROPOSED |
| BR-046 | Source document ownership level | PROPOSED |
| BR-047 | No implied legal validity | PROPOSED |

## 5. Data Need Index

| Data Need | Title |
|---|---|
| DN-CASE-06 | Case Type at creation |
| DN-CASE-07 | Last updated |
| DN-CASE-08 | Associated clients |
| DN-CASE-09 | Finalized case persistence |
| DN-SRC-06 | Client association for source documents |
| DN-LIFE-06 | Post-finalization lifecycle |
| DN-CLI-01..10 | Client identity fields |
| DN-CTYPE-01 | Case Type catalog |
| DN-GEN-01 | Generated document kind (draft/finalized) |

## 6. Open Questions

Open questions tracked for this scope (OQ-CM-01..09) live in [[../../00 - Project Control/Open Questions|Open Questions]] and [[../SRS/SRS|SRS §19.9]].

Key gaps:

- Retention/archival/backup/deletion policy for finalized cases and documents (FR-036).
- Source document storage level: client, case, or both (FR-047).
- Case Type taxonomy beyond LAND_RENT (FR-035).
- Post-finalization client information update rules.

## 7. Consistency Checks

- **Case Type ≠ property use purpose ≠ document type** — confirmed consistent across SRS FR-035, BR-041/042, Data Needs §4.5 (DN-CTYPE).
- **Client ≠ Application User** — confirmed consistent across SRS FR-041..047, BR-043, SRS §9.13.
- **Source vs Draft vs Finalized** — confirmed consistent across SRS FR-048/049, BR-045, SRS §9.15.
- **No legal-validity claims** — SRS §10.10, BR-019, BR-047, NFR-SEC-001 state retention and finalization intent without asserting legal validity.
