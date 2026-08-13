# Project Glossary

**Status:** Living Document  
**Last Updated:** 2026-08-08

Terms will be defined as research progresses. This page serves as a central reference for domain-specific and project-specific terminology.

## Domain Terms

| Term | Definition |
|---|---|
| Application User | A person who operates the system (e.g., a paralegal, notary, office assistant, or land consultant). The Application User is distinct from a **Client**. |
| Client | The person or organization on whose behalf a case is processed (e.g., a landowner or tenant in a land-rent case). A Client is not an Application User and does not necessarily log in to the system. A Client's information may be reused across one or more cases. |
| Case | A long-lived, self-contained matter (e.g., "Land Rent for client X on property Y") that is created, worked on, and finalized within the system. A Case persists after finalization. |
| Case Type | The classification of a Case that determines its workflow and document requirements (e.g., LAND_RENT). The MVP supports a single Case Type: LAND_RENT. Future Case Types are possible but out of scope for the MVP. A Case Type is distinct from a property's **use purpose** (agricultural, business, residential) and from any directory or category concept. |
| Property | The land parcel that a Case concerns. A Property carries details such as location, area, and use purpose. |
| Source Document | A document supplied to or captured by the system as input or evidence (e.g., citizenship/Nagarikta, Lalpurja). A Source Document may be associated with a Client and/or a Case. |
| Generated Draft | A document produced by the system (or an operator) from Case and Client information that has not yet been finalized. |
| Finalized Document | A document that has been explicitly reviewed and finalized by a human operator, becoming the authoritative output of a Case. Finalization is a human decision; the application does not determine legal validity. |
| Land Rent | The first (and MVP) document workflow: a lease agreement under which a landowner (First Party) rents land to a tenant (Second Party). |

## Project Terms

| Term | Definition |
|---|---|
| ADR | Architecture Decision Record — a document capturing a design decision and its rationale |
| Obsidian Vault | The structured collection of Markdown files under `docs/obsidian-vault/` |
| Phase 0 | The initial documentation and research phase of the project |
| UML | Unified Modeling Language — used for system design diagrams |
| SRS | Software Requirements Specification |
