# Project Overview

**Status:** Phase 0 — Requirements Engineering (working drafts, not baselined)  
**Last Updated:** 2026-08-13

## Purpose

The Nepal Land Document Assistant project aims to research, design, and build a system that assists with preparing and managing land-related documents in Nepal. The product is centered on persistent, classified **Cases** (MVP: Land Rent/Lease) that reference reusable **Clients** and distinguish between **Source Documents**, **Generated Drafts**, and **Finalized Documents**. This includes understanding domain-specific workflows, document formats, and document generation needs.

The current proposed architecture is **manual-first** ([[Decision Log]] #009): manual data entry by the Operator is the required acquisition path. OCR/source-document capture are proposed future enhancements, researched in Phase 0.8 and required before full deployment — they are not prerequisites.

## Scope

- Research the domain of Nepali land documentation and related legal/administrative processes (long-term product scope includes land rent/lease, land sale/trade, and land transfer)
- Analyze sample land documents to understand structure, content, and variability
- **Initial prototype scope:** LAND_RENT Case Type with **agricultural use purpose only** ([[Decision Log]] #010); sale/transfer and business/residential rent are future scope
- Explore document-generation technologies suitable for Nepali-language content (OCR research is Phase 0.8, pre-deployment)
- Define functional and non-functional requirements
- Produce UML models and system designs
- Document all architectural decisions
- Model persistent Cases (with Case Type classification), reusable Clients, and typed documents (Source / Generated Draft / Finalized) as first-class concepts (see [[Decision Log]] #004–008)

## Out of Scope (Phase 0)

- Implementation of any application code
- Final technology stack selection
- Mobile or backend source code
- Legal interpretation of documents

## Key Stakeholders

- Project team
- Domain experts (to be engaged during research)

## Repository

All documentation lives in this Obsidian vault under `docs/obsidian-vault/`. Supporting files are stored in `99 - Attachments/`.

## Related Documents

- [[Project Roadmap]]
- [[Open Questions]]
- [[Decision Log]]
- [[Project Glossary]]
