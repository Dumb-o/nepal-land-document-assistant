# Open Questions

**Status:** Living Document  
**Last Updated:** 2026-08-13

This document tracks unresolved questions that arise during research and design. As answers are found, entries are moved to the [[Decision Log]].

## Domain

- What are the exact types of land documents used in Nepal?
- What government bodies are involved in land document processing?
- What is the typical workflow for land transactions in Nepal?
- What languages are land documents written in (Nepali, English, both)?
- What are the common data fields across different document types?

## Case & Client Model (added 2026-08-08)

- What is the exact Case classification taxonomy beyond LAND_RENT? Which future Case Types are planned, and what criteria define them?
- How is "Agriculture" (or any similar term) to be classified: as a Case Type, as a property use purpose, or as a directory/category? The Land Rent template currently treats it as a property **use purpose** (Field Dictionary PROP_USE_PURPOSE), not a Case Type — this needs confirmation. (Decision 010 narrows the initial prototype to agricultural use purpose; it does not change the classification.)
- What is the exact retention, archival, backup, and deletion policy for finalized cases and finalized documents? Finalized cases are intended to be retained indefinitely for operational use, but the concrete policy is not yet defined.
- Should Source Documents be stored/associated at the Client level, the Case level, or both?
- What rules govern updating a Client's information after a Case has been finalized?
- Can finalized Cases ever be archived (moved out of the active directory)? If so, under what criteria?
- What are the backup requirements for Case, Client, and Source Document data?
- What is the deletion policy for Cases, Clients, and Documents (who can delete, under what conditions)?
- What is the exact access-control model (roles, permissions) for Case, Client, and Document data?
- **How is a person with no reusable Client record and no source document represented?** Options: (a) a Client record created with manually entered data and zero source documents; (b) a case-scoped Party with no Client record and no document; (c) another concept. This must never mean "the person cannot be represented in the case" (Data Needs §2.7, BR-049). Recorded as OQ-DN-17 / OQ-UC-10. [OPEN QUESTION — not auto-resolved]

## OCR & Source-Document Capture (Future Enhancement — Decision 009)

OCR/automated extraction and source-document capture are **proposed mechanisms, not requirements** (Decision 009): the system functions on manual entry alone. They are researched in Phase 0.8 and required before full deployment. Open feasibility questions:

- Is OCR/automated extraction of Nepali (Devanagari) text feasible with acceptable accuracy for the target documents?
- Is handwritten text recognition required, or are documents primarily printed?
- What is the expected source-document image quality (scanned photos, phone camera, etc.)?
- Which OCR engines/libraries support Nepali (Devanagari) script? (Technology selection deferred to Phase 0.8/0.9.)
- What capture mechanism (camera, file upload, or both) is required for full deployment?

## Document Generation

- What output formats are required (PDF, Word, etc.)?
- Are there government-mandated templates for documents?
- Should the system generate fillable forms or complete documents?

## Technical

- Should the system work offline or be cloud-connected?
- What are the target platforms (mobile, web, desktop)?
- What is the expected volume of document processing?

## Legal & Compliance

- Are there data privacy regulations that apply to land records?
- Should the system maintain an audit trail?
- What authentication/authorization mechanisms are needed?
