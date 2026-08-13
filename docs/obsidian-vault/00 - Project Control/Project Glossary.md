# Project Glossary

**Status:** Living Document  
**Last Updated:** 2026-08-13

Terms will be defined as research progresses. This page serves as a central reference for domain-specific and project-specific terminology.

## Domain Terms

| Term | Definition |
|---|---|
| Application User | A person who operates the system. The Application User is distinct from a **Client**. The primary role is the **Operator**; a secondary role is the **Administrator**. |
| Operator | The primary Application User role — the document-preparation professional (e.g., notary, deed writer, or office professional) who creates cases, enters and verifies data, and generates and finalizes documents. "Operator" is the canonical term for the human actor in the requirement bodies; "Application User" is the class name. |
| Administrator | A secondary Application User role that additionally manages operator accounts and document templates. |
| Client | The person or organization on whose behalf a case is processed (e.g., a landowner or tenant in a land-rent case). A Client is not an Application User and does not necessarily log in to the system. A Client's information may be reused across one or more cases. |
| Case | A long-lived, self-contained matter (e.g., "Land Rent for client X on property Y") that is created, worked on, and finalized within the system. A Case persists after finalization. |
| Case Type | The classification of a Case that determines its workflow and document requirements (e.g., LAND_RENT). The MVP supports a single Case Type: LAND_RENT. Future Case Types are possible but out of scope for the MVP. A Case Type is distinct from a property's **use purpose** (agriculture / business / residence / mixed) and from any directory or category concept. |
| Party | A role a person or organization plays within a specific Case — **First Party** (landlord/lessor) or **Second Party** (tenant/lessee). Roles are per-case: the same person may be a First Party in one Case and a Second Party in another. A Party may reference a reusable **Client**, or hold its identity fields directly. |
| First Party | The landlord/lessor (प्रथम पक्ष) role within a Case. May be a single individual, multiple co-owners, or, as Second Party only in the current scope, an organization. |
| Second Party | The tenant/lessee (द्वितीय/द्रितिय पक्ष) role within a Case. May be an individual or a company/organization. |
| Use Purpose | The intended use of the Property, distinct from Case Type: **agriculture** (कृषि), **business** (व्यापार व्यवसाय), **residence** (बसोबास), or **mixed**. Determines which clauses are included in the generated document. The initial prototype covers **agriculture only** (Decision 010). |
| Property | The land parcel that a Case concerns. A Property carries details such as location, area, and use purpose. |
| Source Document | A document supplied to or captured by the system as input or evidence (e.g., citizenship/Nagarikta, Lalpurja). A Source Document may be associated with a Client and/or a Case. Source documents are evidence, not a prerequisite for creating a case or representing a party. |
| Candidate Data | Data that has been acquired (via manual entry, automated extraction, or import) but has not yet been verified by the operator. Candidate Data is never used directly for document generation. |
| Verified Case Data | Data that an operator has reviewed and confirmed, and which is the authoritative source for document generation. |
| Generated Draft | A document produced by the system (or an operator) from Case and Client information that has not yet been finalized. |
| Finalized Document | A document that has been explicitly reviewed and finalized by a human operator, becoming the authoritative output of a Case. Finalization is a human decision; the application does not determine legal validity. This is the canonical term (the legacy "Finalized System Record" is deprecated). |
| Manual Data Entry | The required, first-class data-acquisition path: the Operator enters information provided verbally or in writing, including Nepali Unicode (Devanagari) text. No source document or OCR is ever required (Decision 009). |
| OCR | Optical Character Recognition — a proposed, optional mechanism for extracting text from source document images. Never a prerequisite; researched in Phase 0.8 and required before full deployment (Decision 009). |
| Land Rent | The first (and MVP) document workflow: a lease agreement under which a landowner (First Party) rents land to a tenant (Second Party). The initial prototype covers agricultural land rent only (Decision 010). |

## Project Terms

| Term | Definition |
|---|---|
| ADR | Architecture Decision Record — a document capturing a design decision and its rationale |
| Obsidian Vault | The structured collection of Markdown files under `docs/obsidian-vault/` |
| Phase 0 | The initial documentation and research phase of the project |
| UML | Unified Modeling Language — used for system design diagrams |
| SRS | Software Requirements Specification |
