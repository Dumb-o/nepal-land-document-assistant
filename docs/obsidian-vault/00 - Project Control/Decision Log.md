# Decision Log

**Status:** Living Document  
**Last Updated:** 2026-08-08

This log records all significant decisions made during the project. Each entry links to the relevant Architecture Decision Record (ADR) when applicable.

| #   | Date       | Decision                                           | Rationale                                                     | ADR |
| --- | ---------- | -------------------------------------------------- | ------------------------------------------------------------- | --- |
| 001 | 2026-07-27 | Adopt documentation-first approach                 | Ensure thorough understanding before implementation           | TBD |
| 002 | 2026-07-27 | Use Obsidian vault for project knowledge           | Structured Markdown with linking and diagram support          | TBD |
| 003 | 2026-07-27 | Phase 0 focuses exclusively on research and design | Reduce risk of premature technology or implementation choices | TBD |
| 004 | 2026-08-08 | Cases are persistent and long-lived                | A case and its artifacts must remain available after finalization for operational use; the system is a preparation and management tool, not a one-shot generator | TBD |
| 005 | 2026-08-08 | Cases are classified by a Case Type (MVP: LAND_RENT only) | Classification supports organizing and retrieving cases; Land Rent/Lease remains the only MVP workflow | TBD |
| 006 | 2026-08-08 | Client is a distinct concept from Application User | A Client is the person/organization on whose behalf a case is processed and is distinct from the operator; Client records are reusable across cases | TBD |
| 007 | 2026-08-08 | Documents are typed as Source, Generated Draft, or Finalized | Distinguishes evidence/input from in-progress output from authoritative output; only a human finalizes a document | TBD |
| 008 | 2026-08-08 | Finalization is a human decision; the app does not assert legal validity | The operator reviews and finalizes; the application never implies it determines legal validity | TBD |

> Note: Decisions 004–008 reflect the product direction agreed with the user and have been synchronized across the requirements documents in the 2026-08-08 requirements pass. Retention/archival/backup/deletion policies are intentionally left as open questions.

## Proposed Decisions (Under Discussion)

- OCR engine selection (see [[../07 - OCR/OCR Research]])
- Document generation library (see [[../08 - Document Generation/Document Generation Research]])
- Technology stack (deferred to Phase 1)
