# Decision Log

**Status:** Living Document  
**Last Updated:** 2026-08-13

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
| 009 | 2026-08-13 | Manual-first is the current proposed architecture; capture and OCR are future enhancements required before full deployment | Manual data entry is the required, first-class acquisition path for the initial prototype. Source-document capture and OCR/automated extraction are proposed mechanisms — never prerequisites — to be researched in Phase 0.8 and implemented before full production deployment | TBD |
| 010 | 2026-08-13 | Initial prototype scope: LAND_RENT Case Type with agricultural use purpose only | For initial prototyping the product covers land-rent agreements for agricultural land only. Land sale/trade, land transfer, and business/residential rent remain confirmed long-term product directions but are future scope | TBD |

> Note: Decisions 004–008 reflect the product direction agreed with the user and have been synchronized across the requirements documents in the 2026-08-08 requirements pass. Retention/archival/backup/deletion policies are intentionally left as open questions.
>
> Decision 009 refines the treatment of OCR across the requirements set: the SRS's capture/upload (FR-009/FR-010) and OCR items are proposed, pre-deployment enhancements, not MVP requirements. Decision 010 refines Decision 005 for the initial prototype (LAND_RENT × agricultural use purpose).

## Proposed Decisions (Under Discussion)

- OCR / source-document capture technology selection (research in Phase 0.8; required before full deployment, per Decision 009)
- Document generation library / output format (PDF proposed, not prescribed)
- Technology stack (deferred to Phase 1)
