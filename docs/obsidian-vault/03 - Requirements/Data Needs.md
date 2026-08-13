# Data Needs — Land-Rent Document Preparation

> **Working Analysis Document** — This document is the domain-level data inventory for the Land-Rent (LAND_RENT) Case Type. Data needs are derived from the Field Dictionary (`Land Rent Template Analysis.md` §4.1), Field Origin Classification (§11), Template Variable Model (§13), the actual reference template (`private/Reference Documents/Land Rent - WIP.pdf`), the SRS data requirements (`SRS/SRS.md` §9), and agreed product decisions (Decision Log 004–008). It is a **requirements artifact, not a database schema**: it does not define storage, tables, keys, APIs, or technology, and it does not presume any implementation.
>
> This document is the authoritative data inventory that the Functional Requirements, Use Cases, clause library, document generation, extraction (OCR), future database design, traceability, and tests reference.
>
> **2026-08-08 (finalization pass):** Restructured and expanded into a complete, internally consistent inventory for **all LAND RENT / LAND LEASE variations supported by the currently available project evidence**. Added the Client/Party distinction model, missing/absent-party scenarios, multi-party (repeatable) records, extracted vs verified data layers, provenance, the clause and clause-variable model, coverage matrices (template fields, 16 scenarios, land-rent variations), and traceability. All 98 previously defined data needs (DN-P1, DN-P2, DN-PROP, DN-RENT, DN-WIT, DN-WRI, DN-DOC, DN-CASE, DN-SRC, DN-CLI, DN-CTYPE, DN-GEN, DN-LIFE) are preserved unchanged in meaning; new needs were added under new groups. No new fields are invented beyond those justified by the template or the SRS.

| Field | Value |
|---|---|
| **Document Status** | Draft — Finalization Pass Complete (not baselined) |
| **Date** | 2026-08-08 |
| **Derived From** | Field Dictionary (Template Analysis §4.1), Field Origin Classification (§11), Template Variable Model (§13), Conditional Content (§9), `Land Rent - WIP.pdf` (8 examples), SRS §9, Decisions 004–008 |
| **Related SRS** | `SRS/SRS.md` (v0.1.1) §9, §10 |
| **Related Analysis** | `Land Rent Template Analysis.md` |
| **Related Artifacts** | `Use Cases.md`, `Business Rules.md`, `Functional Requirements.md`, `Traceability/Case Client Document Traceability.md` |

---

## 1. Purpose and Scope

1. **What this document is.** A conceptual, domain-level inventory of every piece of information a LAND_RENT case and its documents can hold, where each value comes from, whether it must be verified, what it is used for, and how it relates to clauses and the generated document.
2. **What it feeds.** Functional Requirements (FR-LR), Use Cases, the clause library, document generation, extraction/verification workflows, future database design, traceability, and tests. Nothing here prescribes an implementation.
3. **Scope boundary.** This document covers the LAND_RENT Case Type only (MVP). Future Case Types (land sale, transfer, etc.) are out of scope; their data needs are not modeled.
4. **Variation policy.** Every LAND RENT / LAND LEASE variation supported by the currently available project evidence (the 8 examples in `Land Rent - WIP.pdf` and the Field Dictionary) is modeled. Variations that are only implied or unverified are explicitly marked **PROPOSED** or **TO BE VALIDATED**; unresolved mappings are marked **[UNRESOLVED]**. No variation is silently omitted.
5. **No invention.** Where evidence is insufficient (e.g., a reusable Client's exact field set), the need is marked **TO BE VALIDATED / OPEN QUESTION** rather than invented.

---

## 2. Conceptual Domain Model

### 2.1 Entities and Relationships

```
Application User ──authenticates/operates──▶ Case (via Cases)
Client ──────────────on whose behalf──────▶ Case         [0..* Cases per Client]
Case ────────────────is classified by─────▶ Case Type    [MVP: LAND_RENT]
Case ────────────────has──────────────────▶ Parties      [role: First Party / Second Party]
Party ───────────────refers to────────────▶ Client       [0..1 Client per Party]
Case ────────────────concerns─────────────▶ Property     [1..* kitta records]
Case ────────────────carries──────────────▶ Rent, Term, Payment values
Case ────────────────records──────────────▶ Witnesses    [0..3], Writer/Preparer [0..1]
Case ────────────────holds───────────────▶ Source Documents [evidence/input]
Source Documents ───extract to───────────▶ Extracted Data (Candidate)
Extracted Data ─────verify to────────────▶ Verified Case Data (authoritative)
Verified Case Data ─+ Clauses/Variables──▶ Generated Draft ──human finalize──▶ Finalized Document
Any value ──────────may carry────────────▶ Provenance record ("where did this come from?")
Case activity ──────records──────────────▶ Audit / Event records
```

### 2.2 Client vs Party (Decision 006)

- A **Client** is a reusable domain person/organization on whose behalf a case is processed (e.g., the landowner or the tenant). A Client is **not** an Application User and does not log in.
- A **Party** is a **role within a Case** — First Party (landlord/lessor) or Second Party (tenant/lessee). Roles are per-case: the same person can be a First Party in one case and a Second Party in another, and one Client may appear as a party in many cases.
- A Party **refers to** zero or one Client record. If no Client record exists (or is not created), a Party may still hold its identity fields directly — the party is not required to be backed by a Client record. When a Client is associated, its identity fields may pre-fill the party fields (FR-LR-058).
- **Not conflated:** Application User ≠ Client ≠ Party. A Party is always a role inside a Case; a Client is reusable and Case-independent.

### 2.3 Missing / Absent Parties and Data

The system must tolerate parties that are absent or not yet identified, and values that are missing. Four **party-presence modes** are recognized (all observed or implied by the template; the Ram Maharjan WIP example contains an entirely blank Second Party):

| Mode | First Party (Landlord) | Second Party (Tenant) | Evidence / Implication |
|---|---|---|---|
| **A** | Present & identified | Present & identified | The normal executed agreement (6 of the filled examples). |
| **B** | Present & identified | Absent / not yet identified | Case can be created and worked on; the tenant's identity is a required set of needs that is currently NOT_PROVIDED. |
| **C** | Absent / not yet identified | Present & identified | Same as B with the roles swapped; the agreement cannot be fully drafted until the landlord is identified. |
| **D** | Not identified | Not identified | Early case creation, or a blank WIP template; only case-level and (optionally) property/rent data may exist. |

For every data value, the system distinguishes these **data states** (used in §5):

| State | Meaning |
|---|---|
| **NOT_PROVIDED** | Value not yet entered and not yet requested. |
| **PENDING** | Value has been entered/provided but not yet processed. |
| **UNKNOWN** | Explicitly marked as unknown/unstated by the operator (e.g., age left blank as `वर्ष __` in the template). |
| **N/A** | Not applicable (e.g., company fields for an individual Second Party). |
| **PROVIDED** | Value entered (manual or import) as Candidate Data. |
| **EXTRACTED** | Value produced by automated extraction as Candidate Data (with confidence where available). |
| **REQUIRES_VERIFICATION** | Candidate value (PROVIDED or EXTRACTED) awaiting human confirmation. |
| **VERIFIED** | Value reviewed/corrected and confirmed by the operator; part of Verified Case Data. |

Missing values are **not** silently treated as "no data": NOT_PROVIDED, UNKNOWN, and N/A behave differently for generation, review, and finalization (see §5 and §7.2).

### 2.4 Multiple Parties (Repeatable Records)

- **Multiple First Party individuals (co-owners):** observed with up to 3 co-owners (गंगालाल, शुक्रराज, चन्द्र गोविन्द महर्जन). Each co-owner repeats the full First Party identity field set (DN-P1-01..10). The signature area repeats per co-owner.
- **Multiple Second Party individuals:** not observed in the evidence; the same repeatable structure applies by symmetry, but this is marked **TO BE VALIDATED**.
- **Witnesses:** repeatable entity, 1–3 observed (DN-WIT-01..09 model the three observed slots; the underlying Witness record is repeatable).
- **Multiple kitta numbers:** a single property clause may reference more than one kitta/area pair (कित्ता न. ५५१ र ६२६ with two areas) — repeatable within DN-PROP.

### 2.5 Two Lifecycles, One Model

The system manages two distinct lifecycles (SRS §10.1) that must not be conflated:

- **Data lifecycle:** Captured/Entered → Candidate Data (PROVIDED or EXTRACTED) → Human verification → Verified Case Data.
- **Document lifecycle:** Verified Case Data + Template (Clause + Variable model) → Generated Draft → Human review → Finalized Document.

### 2.6 Conditional Data Pattern

Conditional content follows the chain **Condition → Required Data → Clause → Document Output**:

```
Condition (e.g., property.usePurpose == "agriculture")
  → requires data (e.g., DN-PROP-06 = agriculture; clause-specific obligations)
  → selects Clause (C04 prohibited crops, C11 agriculture restoration)
  → rendered into the Generated Document
```

Conditions are driven by **data**, not by free text. A Case Type (DN-CTYPE, e.g., LAND_RENT) is distinct from a property's **use purpose** (DN-PROP-06: agriculture / business / residence / mixed) and from **document type** (Source / Generated Draft / Finalized). These three concepts are never conflated (Decision 005, BR-042).

### 2.7 Information Acquisition Paths

**Principle:** A required value may be obtained from a source document, extracted through OCR, entered manually by the operator, or reused from existing Client information — subject to verification and any applicable restrictions. OCR/extraction is never a mandatory prerequisite for case creation or document generation. The system must **not** assume that every person involved in a Land Rent case provides a source document; **"Client has no source document" must not mean "Client cannot be represented in the case."**

Five acquisition paths are recognized for any data value:

| Path | Origin | Data State produced | Applicability |
|---|---|---|---|
| **1. Source document provided** | Value read from a supplied document (citizenship, Lalpurja, company registration) | EXTRACTED (if automated) or PROVIDED (if operator-copied) → REQUIRES_VERIFICATION → VERIFIED | Any field present in the document |
| **2. OCR / extraction** | Value produced by automated extraction from a source document | EXTRACTED → REQUIRES_VERIFICATION → VERIFIED | Fields present in the document; OCR is optional and never a prerequisite |
| **3. Manual entry** | Operator enters information provided by the person (verbal or written) | PROVIDED → REQUIRES_VERIFICATION → VERIFIED | Any field; first-class acquisition path, not a fallback only |
| **4. Combination** | Mixed acquisition: some fields from documents/OCR, others entered manually (e.g., name OCR'd, address manually corrected/entered) | Per-value states → VERIFIED | The normal case; fields acquire values independently |
| **5. Existing Client information** | Value reused/pre-filled from a reusable Client record (DN-CLI, Decision 006) | PROVIDED (from verified Client data) → VERIFIED | Fields matching Client identity; pre-fill via FR-LR-058/059 |

Acquisition-path rules:

- **Manual entry is first-class.** The operator (notary-office user) must be able to enter required information directly, including Nepali Unicode text. This is a data-acquisition requirement; the keyboard/IME implementation is not prescribed.
- **No source document is required.** "No source document supplied" is a valid state for information that can be obtained manually. Source documents are evidence (Decision 007), not a precondition for representing a party or creating a case.
- **OCR is not authoritative.** Extraction output is Candidate Data and requires operator review/edit/confirmation before it becomes Verified Case Data (BR-014, OCR-004, FR-LR-019/020).
- **Per-field acquisition rules vary.** For each Data Need in §7.4, manual entry may be permitted, a source document may be required, the requirement may be conditional, or it may remain unknown. Where evidence is insufficient, the field is marked **[TO BE VALIDATED]**.
- **Provenance is internal.** The acquisition source of a value (e.g., "manually entered", "OCR from citizenship.jpg") is provenance/audit metadata (DN-PROV), primarily for system operation, review, and traceability. It is **not** automatically rendered into the final legal document; it appears in document content only if the Land Rent template actually requires it.
- **Generation is source-agnostic.** Document generation consumes **Verified Case Data** regardless of whether each value came from OCR, manual entry, a document, or a Client record (DN-VER; §5.2; UC-011).

---

## 3. Data Need Groups

The conceptual domains below map to Data Need groups. Each group's evidence and requirement status are shown. Where a conceptual domain has only partial or indirect evidence, it is explicitly marked.

| Conceptual Domain  | DN Group  | Purpose                                                                          | Primary Sources                                   | Status                                         |
| ------------------ | --------- | -------------------------------------------------------------------------------- | ------------------------------------------------- | ---------------------------------------------- |
| Application User   | DN-APP    | Operator/administrator identity, credentials, role (minimal — SRS §9.1)          | SRS §9.1                                          | PROPOSED                                       |
| Client             | DN-CLI    | Reusable person/organization on whose behalf a case is processed (Decision 006)  | Citizenship, Company Registration, verbal         | CONFIRMED (fields), TO BE VALIDATED (full set) |
| Party              | DN-PTY    | Party as a role (First/Second) within a Case; link to Client                     | SRS §9.2, §9.4                                    | PROPOSED                                       |
| Case               | DN-CASE   | Case-level metadata and lifecycle                                                | SRS §9.2, Decisions 004, 005                      | CONFIRMED                                      |
| Case Type          | DN-CTYPE  | Case classification (MVP: LAND_RENT)                                             | SRS §9.14, Decision 005                           | CONFIRMED                                      |
| Property           | DN-PROP   | Land description, kitta, area, use purpose                                       | Lalpurja / land record                            | CONFIRMED                                      |
| Ownership / Rights | DN-OWN    | Registered-owner reference and land registration category (Guthi etc.)           | Lalpurja (template: जोत जनी ज.ध. महल, भवानी गुठि) | PROPOSED (thin evidence)                       |
| Rent / Lease       | DN-RENT   | Rent amount, period, escalation, payment timing, term, notice                    | Client verbal / operator                          | CONFIRMED (except escalation method)           |
| Payment            | DN-PAY    | Advance payment arrangement; expense/obligation assignment (mostly clause-level) | Template Clause 2 + obligation clauses            | PROPOSED (partial evidence)                    |
| Duration / Dates   | DN-DOC    | BS agreement date and output metadata                                            | System-generated; template S08                    | CONFIRMED                                      |
| Witnesses          | DN-WIT    | Witness identity (repeatable 0..3)                                               | Client verbal                                     | PROPOSED                                       |
| Writer / Preparer  | DN-WRI    | Document drafter identity; optional professional license                         | Operator                                          | PROPOSED                                       |
| Source Documents   | DN-SRC    | Capture/upload provenance and typing                                             | System-generated                                  | CONFIRMED                                      |
| Extracted Data     | DN-EXT    | Candidate values from extraction/manual entry (pre-verification layer)           | SRS §9.7                                          | PROPOSED                                       |
| Verified Case Data | DN-VER    | Verified values, verification metadata, correction history (authoritative layer) | SRS §9.8                                          | PROPOSED                                       |
| Clauses            | DN-CLAUSE | Clause identity, text, conditions, required data                                 | Template §9, §3.2                                 | PROPOSED                                       |
| Clause Variables   | DN-VAR    | Variable binding between data needs and clause placeholders                      | Template §13                                      | PROPOSED                                       |
| Generated Draft    | DN-GEN    | Generated Draft metadata                                                         | SRS §9.10, §9.15                                  | CONFIRMED                                      |
| Finalized Document | DN-GEN    | Finalized Document metadata (immutable, human-finalized)                         | SRS §9.11, §9.15, Decision 007/008                | CONFIRMED                                      |
| Case Lifecycle     | DN-LIFE   | Data/doc lifecycle and post-finalization persistence                             | SRS §10, Decision 004                             | CONFIRMED                                      |
| Audit / Event      | DN-AUDIT  | Event history of significant actions                                             | SRS §9.12                                         | PROPOSED                                       |
| Provenance         | DN-PROV   | Per-value "where did this come from?" record                                     | SRS §9.7/9.8                                      | PROPOSED                                       |

> **Conceptual relationships recap:** An **Application User** is an operator of the system. A **Client** is a domain person/organization (e.g., a party in a land-rent case) and is NOT an Application User. A **Case** is classified by a **Case Type**, involves **Parties** (which may reference **Clients**), concerns a **Property**, carries **Rent/Term/Payment** values, records **Witnesses** and a **Writer**, holds **Source Documents**, and produces a **Generated Draft** and a **Finalized Document**. Candidate values pass through **Extracted Data** to **Verified Case Data**; every value may carry a **Provenance** record, and significant events are recorded in **Audit** records.

---

## 4. Data Need Inventory

### 4.0 Legend

**Source (origin of the value):**
- `SOURCE_DERIVED` — value comes from a source document
- `USER_PROVIDED` — value provided verbally by client / entered by operator (manual entry is a first-class acquisition path, §2.7)
- `CALCULATED` — computed by the system
- `SYSTEM_GENERATED` — created by the system
- `STATIC_TEMPLATE` — fixed template text (not a data need)

> **Acquisition note (§2.7):** `SOURCE_DERIVED` does **not** imply a source document is required. Every value may, where permitted and subject to verification, be entered manually (`USER_PROVIDED`), extracted by OCR into Candidate Data, or reused from existing Client information. Where a value can only come from a source document (or only manually), that restriction is stated explicitly; otherwise manual entry is permitted. Per-value acquisition rules are consolidated in the §7.4 acquisition matrix.

**Requirement Status:** `CONFIRMED` (supported by evidence) · `PROPOSED` (reasonable, not yet validated) · `TO BE VALIDATED` (needs domain confirmation) · `OPEN QUESTION` (unresolved).

**Cardinality:** per the entity indicated (e.g., "1 per First Party individual").

**Verification:** whether the operator must verify the value before it may be used in generation (Required / Not required / Conditional).

**Used By:** template sections (`S01` Title, `S02` Preamble, `S03` Clauses, `S04` First Party signature, `S05` Second Party signature, `S06` Witnesses, `S07` Writer, `S08` Date) and clauses (`C01`–`C13`, defined in §6.1), plus FR-LR / UC references where helpful.

### 4.1 DN-APP — Application User Information

> Minimal group. Application User data is operationally required (authentication/authorization) but is not document content. Detailed operator fields are [TO BE VALIDATED].

#### DN-APP-01 — Application User identity

- **Domain:** Application User
- **Description:** Operator/administrator identity record (name, credentials reference, role).
- **Purpose:** Authentication, authorization, and attribution of case/document actions.
- **Source:** USER_PROVIDED / SYSTEM_GENERATED
- **Applies To:** Each Application User account.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per Application User.
- **Source of Value:** Operator (self-registration or administrator-created, FR-LR-003).
- **Verification:** Not required (trusted account data).
- **Used By:** FR-LR-001..003; UC-001, UC-015; audit attribution (DN-AUDIT-03).

#### DN-APP-02 — Authentication data

- **Domain:** Application User
- **Description:** Credentials and authentication method (PIN/password/biometric — method [TO BE DETERMINED]).
- **Purpose:** Secure access (SRS §9.1).
- **Source:** SYSTEM_GENERATED / USER_PROVIDED
- **Applies To:** Each Application User account.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per account.
- **Source of Value:** Operator, per access-control policy.
- **Verification:** Not required (managed by system).
- **Used By:** FR-LR-001, FR-LR-002; NFR-SEC; UC-001.

#### DN-APP-03 — Access permissions / role

- **Domain:** Application User
- **Description:** Role and permissions governing which cases, clients, and documents the user may access.
- **Purpose:** Role-based access control (SRS §9.1, §10.9).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each Application User account.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1..* roles per account (as defined by access-control model).
- **Source of Value:** Administrator.
- **Verification:** Not required.
- **Used By:** FR-LR-002, FR-LR-048; BR-003, BR-037; UC-001, UC-015.

### 4.2 DN-CLI — Client Information

> A **Client** is the person or organization on whose behalf a case is processed, distinct from the Application User (Decision 006). Client fields reuse the Field Dictionary party identity fields; no new fields are invented beyond them ([OPEN QUESTION] OQ-DN-07). One Client may appear in many Cases (1..N).
>
> **No source document is required to create a Client.** A Client record may be created from information entered manually (verbal/written) even when no citizenship certificate, Lalpurja, or company registration has been supplied (§2.7 path 3). Where a source document is available, it may be captured and used for extraction (§2.7 paths 1–2). The absence of a source document must not prevent a Client from being represented in a case (BR-049; see OQ-DN-17 for the Client-record vs case-specific-Party representation question).

#### DN-CLI-01 — Client full name (or organization name)

- **Domain:** Client
- **Description:** Full name of the client person, or the organization name if the client is an entity.
- **Purpose:** Identity; reuse across cases; pre-fills party fields; search key (FR-LR-057).
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Each Client record.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Client.
- **Source of Value:** Citizenship Certificate (name), Company Registration Certificate (organization name), or verbal.
- **Verification:** Required (high sensitivity).
- **Used By:** UC-017, UC-018, UC-019; DN-P1-01 / DN-P2-01 pre-fill; search (FR-LR-057).

#### DN-CLI-02 — Client grandfather

- **Domain:** Client
- **Description:** Grandfather's name (individual clients) — lineage pattern `[grandfather]को नाती/नातिनी`.
- **Purpose:** Identity lineage; pre-fills party lineage.
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Individual Client records.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per Client.
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required.
- **Used By:** UC-017; DN-P1-02 / DN-P2-02 pre-fill.

#### DN-CLI-03 — Client father

- **Domain:** Client
- **Description:** Father's name (individual clients) — lineage pattern `[Father]को छोरा/छोरी`.
- **Purpose:** Identity lineage; pre-fills party lineage.
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Individual Client records.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 0..1 per Client (usually present).
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required.
- **Used By:** UC-017; DN-P1-03 / DN-P2-03 pre-fill.

#### DN-CLI-04 — Client address — district

- **Domain:** Client
- **Description:** Client's home district.
- **Purpose:** Identity/address; pre-fills party address.
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Each Client record.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Client.
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required.
- **Used By:** UC-017; DN-P1-04 / DN-P2-04 pre-fill.

#### DN-CLI-05 — Client address — municipality

- **Domain:** Client
- **Description:** Municipality / rural municipality (including "हाल परिवर्तित" — currently changed).
- **Purpose:** Identity/address; pre-fills party address.
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Each Client record.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Client.
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required.
- **Used By:** UC-017; DN-P1-05 / DN-P2-05 pre-fill.

#### DN-CLI-06 — Client address — ward

- **Domain:** Client
- **Description:** Ward number.
- **Purpose:** Identity/address; pre-fills party address.
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Each Client record.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Client.
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required.
- **Used By:** UC-017; DN-P1-06 / DN-P2-06 pre-fill.

#### DN-CLI-07 — Client citizenship number

- **Domain:** Client
- **Description:** Citizenship (ना.प्र.न.) number of an individual client.
- **Purpose:** Identity; uniqueness/search aid (FR-LR-057).
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Individual Client records.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per Client (present when available).
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required (high sensitivity).
- **Used By:** UC-017, UC-018; DN-P1-08 / DN-P2-08 pre-fill.

#### DN-CLI-08 — Client citizenship issue date

- **Domain:** Client
- **Description:** Citizenship issue date (BS).
- **Purpose:** Identity; pre-fills party citizenship.
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Individual Client records.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per Client.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** UC-017; DN-P1-09 / DN-P2-09 pre-fill.

#### DN-CLI-09 — Client citizenship issue district

- **Domain:** Client
- **Description:** District where citizenship was issued.
- **Purpose:** Identity; pre-fills party citizenship.
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Individual Client records.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per Client.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** UC-017; DN-P1-10 / DN-P2-10 pre-fill.

#### DN-CLI-10 — Client organization name (if the client is an entity)

- **Domain:** Client
- **Description:** Organization name and registration reference where the client is an entity (company).
- **Purpose:** Identity for entity clients; pre-fills the company Second Party variant.
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Entity Client records (CONDITIONAL).
- **Requirement Status:** CONDITIONAL
- **Cardinality:** 0..1 per Client (entities only).
- **Source of Value:** Company Registration Certificate.
- **Verification:** Required.
- **Used By:** UC-017; DN-P2-12..16 pre-fill.

> **Relationship notes:** A Client may be associated with many Cases (DN-CASE-08). Source Documents may be associated with a Client (DN-SRC-06) in addition to a Case — storage level is [OPEN QUESTION] OQ-DN-08. Rules for updating a Client after a finalized Case references it are [OPEN QUESTION] OQ-DN-09.

### 4.3 DN-PTY — Party (Role within a Case)

> A **Party** is the role a person/organization plays in a specific Case (First Party = landlord/lessor; Second Party = tenant/lessee). Roles are per-case and are not fixed identities. This group models the role and its linkage; the identity field sets themselves are DN-P1 / DN-P2.
>
> **A Party does not require a source document, a Client record, or a successful OCR pass to be represented in a Case.** Each Party's identity values (DN-P1 / DN-P2) may be entered manually and verified (§2.7 path 3), and the Party-to-Client reference (DN-PTY-02) is optional (0..1). This keeps a person with no source document fully representable. How such a person is stored long-term — as a Client record with no source documents vs. as a case-scoped Party without a Client — is recorded as an open design question (OQ-DN-17) and is **not** auto-resolved here.

#### DN-PTY-01 — Party role

- **Domain:** Party
- **Description:** The role of a party in a Case: First Party (प्रथम पक्ष, landlord/lessor) or Second Party (द्वितीय/द्रितिय पक्ष, tenant/lessee).
- **Purpose:** Structural: determines which field set (DN-P1 / DN-P2) and which signature section (S04 / S05) apply.
- **Source:** USER_PROVIDED (operator) / SYSTEM_GENERATED
- **Applies To:** Each Party record in a Case.
- **Requirement Status:** PROPOSED
- **Cardinality:** At least 1 Party per Case; typically 2 roles (1..* First Party, 1..* Second Party — multiplicity observed 1..3 for First Party).
- **Source of Value:** Operator during case setup (UC-002, UC-005).
- **Verification:** Required (identity-affecting).
- **Used By:** Preamble S02; Signature areas S04/S05; FR-LR-010..012; UC-005.

#### DN-PTY-02 — Party-to-Client reference

- **Domain:** Party
- **Description:** Reference from a Party to a reusable Client record (0..1). May be absent when no Client record exists.
- **Purpose:** Enables Client reuse (Decision 006, FR-LR-058/059) and pre-fill of party identity fields.
- **Source:** SYSTEM_GENERATED (association)
- **Applies To:** Each Party record in a Case.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per Party.
- **Source of Value:** Operator selecting/creating a Client (UC-017, UC-019).
- **Verification:** Not required (administrative association).
- **Used By:** DN-CASE-08; FR-LR-058..060; UC-019, UC-020.

#### DN-PTY-03 — Party type (individual / organization)

- **Domain:** Party
- **Description:** Whether the party is an individual or an organization (company). Determines which identity variant applies (individual DN-P2-01..11 vs company DN-P2-12..16 for the Second Party; the First Party type is not specified in the evidence).
- **Purpose:** Conditional field selection and preamble rendering.
- **Source:** USER_PROVIDED
- **Applies To:** Each Party record.
- **Requirement Status:** PROPOSED (company variant CONFIRMED for Second Party; First-Party entity type [TO BE VALIDATED])
- **Cardinality:** 1 per Party.
- **Source of Value:** Operator (from source documents).
- **Verification:** Required.
- **Used By:** Preamble S02; DN-P2 company condition; BR-030; UC-005.

> **Presence/absence handling:** Party presence modes A–D (§2.3) are case-level states, not separate data needs; they are tracked via the data states in §5 and the scenario matrix in §7.2.

### 4.4 DN-CASE — Case Information

> Case-level metadata and lifecycle (SRS §9.2; Decisions 004, 005). Cases persist after finalization.

#### DN-CASE-01 — Case identifier

- **Domain:** Case
- **Description:** Unique case identifier assigned at creation.
- **Purpose:** Reference, retrieval, and audit (FR-LR-005, FR-LR-052).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each Case.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Case.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-005; UC-002, UC-003, UC-014; DN-SRC-04, DN-GEN-05.

#### DN-CASE-02 — Case status

- **Domain:** Case
- **Description:** Current lifecycle state. Canonical set (aligned across artifacts 2026-08-13): `Created`, `In Progress`, `Draft Generated`, `Under Review`, `Finalized`, `Persistent`. "In Progress" is the umbrella for data collection/verification activity; the earlier SRS states `Data Collection`, `Verification`, `Archived/Closed` were removed from SRS FR-007.
- **Purpose:** Track progress; control allowed transitions (e.g., generation, finalization).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each Case.
- **Requirement Status:** CONFIRMED (state values [TO BE VALIDATED])
- **Cardinality:** 1 per Case.
- **Source of Value:** System (status transitions per BR/workflow rules).
- **Verification:** Not required.
- **Used By:** FR-LR-008, FR-LR-050; UC-003; BR-016, BR-017; §5.

#### DN-CASE-03 — Case creation metadata

- **Domain:** Case
- **Description:** Creation date/time and creating operator.
- **Purpose:** Audit (FR-LR-006).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each Case.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Case.
- **Source of Value:** System + authenticated operator.
- **Verification:** Not required.
- **Used By:** FR-LR-006; UC-002.

#### DN-CASE-04 — Case finalization metadata

- **Domain:** Case
- **Description:** Finalization date/time and operator (if applicable).
- **Purpose:** Record completion (FR-LR-036); distinguishes finalized cases.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each finalized Case.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 0..1 per Case (present once finalized).
- **Source of Value:** System + finalizing operator.
- **Verification:** Not required.
- **Used By:** FR-LR-036; UC-013.

#### DN-CASE-05 — Case notes

- **Domain:** Case
- **Description:** Free-text operator notes attached to the case.
- **Purpose:** Operational convenience; not document content.
- **Source:** USER_PROVIDED
- **Applies To:** Each Case.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per Case.
- **Source of Value:** Operator.
- **Verification:** Not required.
- **Used By:** FR-LR-009; UC-003.

#### DN-CASE-06 — Case Type (classification)

- **Domain:** Case
- **Description:** Classification of the Case; MVP supports a single Case Type: LAND_RENT (Decision 005).
- **Purpose:** Determines workflow and document requirements; distinct from property use purpose and document type (BR-042).
- **Source:** SYSTEM_GENERATED / USER_PROVIDED
- **Applies To:** Each Case (assigned at creation).
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Case.
- **Source of Value:** Operator at creation (UC-002) from the Case Type catalog (DN-CTYPE).
- **Verification:** Not required.
- **Used By:** FR-LR-049; UC-002, UC-003; BR-041, BR-042.

#### DN-CASE-07 — Last updated (date/time)

- **Domain:** Case
- **Description:** Timestamp of the last modification to the case.
- **Purpose:** Recency display and retrieval (FR-LR-054).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each Case.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Case (maintained automatically).
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-054; UC-003.

#### DN-CASE-08 — Associated Client(s)

- **Domain:** Case
- **Description:** The Client(s) on whose behalf the case is processed (1..N), each via a Party-to-Client link (DN-PTY-02).
- **Purpose:** Client reuse across cases; "view a client's cases" (FR-LR-060).
- **Source:** SYSTEM_GENERATED (association)
- **Applies To:** Each Case.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 0..N Clients per Case.
- **Source of Value:** Operator association (UC-019).
- **Verification:** Not required (administrative association).
- **Used By:** FR-LR-058..060; UC-019, UC-020; DN-PTY-02.

#### DN-CASE-09 — Case persistence after finalization

- **Domain:** Case
- **Description:** Finalized cases remain available and retrievable for operational use; retained indefinitely by product intent (Decision 004), exact retention/archival/backup/deletion policy [TO BE VALIDATED].
- **Purpose:** Persistent, long-lived cases (not a one-shot generator).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each finalized Case.
- **Requirement Status:** CONFIRMED (policy [TO BE VALIDATED])
- **Cardinality:** 1 per Case.
- **Source of Value:** System (Decision 004).
- **Verification:** Not required.
- **Used By:** FR-LR-050; UC-003, UC-014; BR-039, BR-040; DN-LIFE-06.

### 4.5 DN-CTYPE — Case Type

> Case Type classifies a Case and determines its workflow and document requirements (SRS §9.14; Decision 005). MVP: LAND_RENT only. Distinct from property use purpose (DN-PROP-06) and document type.

#### DN-CTYPE-01 — Case Type identifier

- **Domain:** Case Type
- **Description:** Case Type code (MVP: LAND_RENT). Additional Case Types are future scope.
- **Purpose:** Case classification, workflow selection, directory organization.
- **Source:** SYSTEM_GENERATED / USER_PROVIDED
- **Applies To:** Case Type catalog.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1..* in catalog (MVP: 1).
- **Source of Value:** System catalog (MVP: LAND_RENT).
- **Verification:** Not required.
- **Used By:** FR-LR-049, FR-LR-053; UC-002, UC-003; BR-041.

#### DN-CTYPE-02 — Case Type display name / description

- **Domain:** Case Type
- **Description:** Human-readable label/description for operator selection and the case directory.
- **Purpose:** Usability in case creation and browsing.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Case Type catalog.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Case Type.
- **Source of Value:** System catalog.
- **Verification:** Not required.
- **Used By:** UC-002, UC-003; FR-LR-053.

#### DN-CTYPE-03 — Template(s) associated with the Case Type

- **Domain:** Case Type
- **Description:** Which document template(s) apply to a Case Type (LAND_RENT ↔ land-rent template).
- **Purpose:** Template selection at generation time (UC-011).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Case Type catalog.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1..* templates per Case Type.
- **Source of Value:** Administrator (template management).
- **Verification:** Not required.
- **Used By:** UC-011, UC-016; DN-GEN-04.

### 4.6 DN-PROP — Property Information

> Land description from the Lalpurja / land record. Area uses the Ropani-Anna-Paisa-Dam (R-A-P-D) format (०-०-०-०). [OPEN QUESTION] OQ-DN-01: structured R-A-P-D vs single string.

#### DN-PROP-01 — Property district (ल.पु.जि.)

- **Domain:** Property
- **Description:** District where the land is registered (land revenue district).
- **Purpose:** Property identity in Clause C01.
- **Source:** SOURCE_DERIVED
- **Applies To:** Each property record in a Case.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per property record.
- **Source of Value:** Lalpurja / land record.
- **Verification:** Required.
- **Used By:** C01 (S03); FR-LR-013; UC-006.

#### DN-PROP-02 — Property ward

- **Domain:** Property
- **Description:** Ward number of the property (e.g., ३ ख, ८ क, ५-क, ७-क).
- **Purpose:** Property identity in Clause C01.
- **Source:** SOURCE_DERIVED
- **Applies To:** Each property record.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per property record.
- **Source of Value:** Lalpurja / land record.
- **Verification:** Required.
- **Used By:** C01 (S03); FR-LR-013; UC-006.

#### DN-PROP-03 — Kitta number(s)

- **Domain:** Property
- **Description:** Plot/kitta number(s); a single clause may reference more than one kitta (कित्ता न. ५५१ र ६२६ observed).
- **Purpose:** Unique land identifier in Clause C01.
- **Source:** SOURCE_DERIVED
- **Applies To:** Each property record (repeatable kitta entries).
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1..* kitta per property record.
- **Source of Value:** Lalpurja / land record.
- **Verification:** Required (high sensitivity).
- **Used By:** C01 (S03); BR-032; FR-LR-013; UC-006.

#### DN-PROP-04 — Land area (Ropani-Anna-Paisa-Dam)

- **Domain:** Property
- **Description:** Land area in Ropani-Anna-Paisa-Dam format (०-०-०-०); each kitta may carry its own area (e.g., ०-०-३-१ and ०-४-३-१ for two kitta).
- **Purpose:** Legal land description in Clause C01; area format [TO BE VALIDATED] (BR-020).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each property record (per kitta).
- **Requirement Status:** CONFIRMED (format [TO BE VALIDATED]; storage structure [OPEN QUESTION] OQ-DN-01)
- **Cardinality:** 1 per kitta entry.
- **Source of Value:** Lalpurja / land record.
- **Verification:** Required (high sensitivity).
- **Used By:** C01 (S03); BR-020; FR-LR-013, FR-LR-018; UC-006.

#### DN-PROP-05 — Land category / registration type

- **Domain:** Property
- **Description:** Land category / registration reference (जोत जनी ज.ध. महल, भवानी गुठि — Guthi registration appears in some instances; see DN-OWN).
- **Purpose:** Property description in Clause C01; conditionally includes Guthi reference (BR-033).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each property record.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per property record.
- **Source of Value:** Lalpurja / land record.
- **Verification:** Required.
- **Used By:** C01 (S03); BR-033; UC-006; DN-OWN-02.

#### DN-PROP-06 — Use purpose (प्रयोजन)

- **Domain:** Property
- **Description:** Intended use: कृषि (agriculture), व्यापार व्यवसाय (business/commercial), बसोबास (residence), or mixed (व्यापार व्यवसाय तथा बसोबास). Determines which clauses are included (conditional content).
- **Purpose:** Conditional clause selection (C03, C04, C11, C12); distinct from Case Type and document type.
- **Source:** USER_PROVIDED
- **Applies To:** Each property record.
- **Requirement Status:** CONFIRMED (full list of purposes [TO BE VALIDATED] OQ-DN-05)
- **Cardinality:** 1 per property record.
- **Source of Value:** Client / operator (judgment call).
- **Verification:** Not required (operator judgment).
- **Used By:** C01, C03, C04, C11, C12; BR-027, BR-028, BR-029; §14.2 (Template Analysis); UC-006.

### 4.7 DN-OWN — Ownership / Rights

> Thin evidence: the template states the land is registered in the First Party's name (प्रथम पक्षको नाउँ मा दर्ता प्रमाणित) and references registration categories (जोत जनी ज.ध. महल, भवानी गुठि). This group is kept minimal and is largely covered by DN-PROP-05 and the Party identity.

#### DN-OWN-01 — Registered owner reference

- **Domain:** Ownership / Rights
- **Description:** The party in whose name the property is registered (per Clause C01: "प्रथम पक्षको नाउँ मा दर्ता प्रमाणित"). The template does not model ownership separately from the First Party identity.
- **Purpose:** Establishes that the First Party offers land registered in its name.
- **Source:** SOURCE_DERIVED
- **Applies To:** Property record within a Case.
- **Requirement Status:** PROPOSED — TO BE VALIDATED (whether ownership is a distinct record or always the First Party)
- **Cardinality:** 0..1 per property record.
- **Source of Value:** Lalpurja.
- **Verification:** Required.
- **Used By:** C01; [TRACEABILITY REQUIRED] (no dedicated SRS §9 entry; relates to §9.3/§9.4).

#### DN-OWN-02 — Land registration / tenure category

- **Domain:** Ownership / Rights
- **Description:** Registration/tenure category reference (ज.ध. महल, भवानी गुठि, private). Shared with DN-PROP-05 (PROP_TYPE_LAND).
- **Purpose:** Conditional Guthi reference in the property description (BR-033).
- **Source:** SOURCE_DERIVED
- **Applies To:** Property record.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per property record (same value as DN-PROP-05).
- **Source of Value:** Lalpurja / land record.
- **Verification:** Required.
- **Used By:** C01; BR-033; DN-PROP-05.

### 4.8 DN-RENT — Rental and Term Information

> Financial and term conditions (Clause C02 and related clauses). Escalation patterns [TO BE VALIDATED] (Template Analysis §7.2).

#### DN-RENT-01 — Rent amount (figures, NPR)

- **Domain:** Rent / Lease
- **Description:** Rent amount in Nepali rupees (e.g., रु ६५,०००/-, रु २०,०००/-, रु ५,५००/-).
- **Purpose:** Clause C02 rent clause; input to the Nepali-words calculation (DN-RENT-02).
- **Source:** USER_PROVIDED
- **Applies To:** Each Case's rent arrangement.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per rent arrangement.
- **Source of Value:** Client / operator.
- **Verification:** Required (high sensitivity; words override figures — BR-023 [TO BE VALIDATED]).
- **Used By:** C02; BR-021, BR-022, BR-024; FR-LR-014, FR-LR-015; UC-007.

#### DN-RENT-02 — Rent amount (Nepali words, अक्षेरुपिय)

- **Domain:** Rent / Lease
- **Description:** The rent amount written in Nepali words, always following the figure (अक्षेरुपिय पैसाठी हजार रुपैया).
- **Purpose:** Legal wording in Clause C02; generated automatically and presented for verification.
- **Source:** CALCULATED
- **Applies To:** Each rent arrangement.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per rent arrangement.
- **Source of Value:** System (from DN-RENT-01); operator-correctable (FR-LR-015).
- **Verification:** Required (high sensitivity; words override figures).
- **Used By:** C02; BR-021, BR-022, BR-023; FR-LR-015; UC-007, UC-011.

#### DN-RENT-03 — Rent period (मासिक / वार्षिक)

- **Domain:** Rent / Lease
- **Description:** Whether rent is monthly (मासिक) or annual (वार्षिक). Determines which rent wording is generated.
- **Purpose:** Clause C02 conditional generation (BR-029).
- **Source:** USER_PROVIDED
- **Applies To:** Each rent arrangement.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per rent arrangement.
- **Source of Value:** Client / operator.
- **Verification:** Required.
- **Used By:** C02; BR-029; FR-LR-014; UC-007.

#### DN-RENT-04 — Escalation rate

- **Domain:** Rent / Lease
- **Description:** Percentage (or fixed amount) increase (5%, 10% observed).
- **Purpose:** Clause C02 escalation wording and calculation.
- **Source:** USER_PROVIDED
- **Applies To:** Each rent arrangement.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 0..1 per rent arrangement.
- **Source of Value:** Client / operator.
- **Verification:** Required.
- **Used By:** C02; BR-025; FR-LR-014; UC-007.

#### DN-RENT-05 — Escalation period

- **Domain:** Rent / Lease
- **Description:** How often rent increases: प्रत्येक वर्ष (every year), प्रत्येक २/२ वर्षमा (every 2 years), २ वर्ष पछि (after 2 years).
- **Purpose:** Clause C02 escalation wording and calculation schedule.
- **Source:** USER_PROVIDED
- **Applies To:** Each rent arrangement.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 0..1 per rent arrangement.
- **Source of Value:** Client / operator.
- **Verification:** Required.
- **Used By:** C02; BR-025; FR-LR-014; UC-007.

#### DN-RENT-06 — Payment timing (अग्रिम etc.)

- **Domain:** Rent / Lease (also Payment)
- **Description:** When rent is paid — observed: अग्रिम (advance). Advance-rent arrangements appear in the template.
- **Purpose:** Clause C02 payment wording.
- **Source:** USER_PROVIDED
- **Applies To:** Each rent arrangement.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 0..1 per rent arrangement.
- **Source of Value:** Client / operator.
- **Verification:** Required.
- **Used By:** C02; FR-LR-014; UC-007; DN-PAY-01.

#### DN-RENT-07 — Escalation method (compound / simple)

- **Domain:** Rent / Lease
- **Description:** Compound (चक्रवृद्धि) or simple escalation. The template states compound explicitly; other methods [TO BE VALIDATED].
- **Purpose:** Clause C02 escalation wording and calculation method (BR-026 [TO BE VALIDATED]).
- **Source:** USER_PROVIDED
- **Applies To:** Each rent arrangement.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per rent arrangement.
- **Source of Value:** Client / operator.
- **Verification:** Required.
- **Used By:** C02; BR-026; FR-LR-014; UC-007.

#### DN-RENT-08 — Term duration (years)

- **Domain:** Duration / Dates
- **Description:** Lease term in years — 3, 5, or 10 years observed.
- **Purpose:** Clause C01 term wording ("आजको मितिले N वर्ष सम्मको लागि").
- **Source:** USER_PROVIDED
- **Applies To:** Each Case.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Case.
- **Source of Value:** Client / operator.
- **Verification:** Required (high sensitivity).
- **Used By:** C01; FR-LR-014; UC-007.

#### DN-RENT-09 — Notice period

- **Domain:** Duration / Dates
- **Description:** Notice period for termination — 30 days, 60 days, 3 months, 6 months observed; one instance uses asymmetric periods per party (First Party 3 months / Second Party 6 months).
- **Purpose:** Clause C08 notice/termination wording.
- **Source:** USER_PROVIDED
- **Applies To:** Each Case (per-party notice possible).
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1..2 per Case (per-party asymmetric supported).
- **Source of Value:** Client / operator.
- **Verification:** Required.
- **Used By:** C08; FR-LR-014; UC-007.

### 4.9 DN-PAY — Payment

> Thin evidence: the template assigns rent payment to the Second Party (advance) and assigns specified expenses as obligations in clauses. Payment as a distinct conceptual domain is mostly clause-level content rather than additional data fields.

#### DN-PAY-01 — Advance payment arrangement

- **Domain:** Payment
- **Description:** Whether rent is paid in advance (अग्रिम) and any advance schedule. Same value as DN-RENT-06; listed here for the Payment domain mapping.
- **Purpose:** Clause C02 payment wording.
- **Source:** USER_PROVIDED
- **Applies To:** Each rent arrangement.
- **Requirement Status:** CONFIRMED (via DN-RENT-06)
- **Cardinality:** 0..1 per rent arrangement.
- **Source of Value:** Client / operator.
- **Verification:** Required.
- **Used By:** C02; DN-RENT-06.

#### DN-PAY-02 — Expense / obligation assignment

- **Domain:** Payment
- **Description:** Obligations assigned to the Second Party (बहालकर — rent tax; विद्युत महसुल — electricity; पानीको महसुल — water; भौतिक संरचना निर्माण कर — construction taxes; फोहोर व्यवस्थापन — waste management). Modeled as clause content (C06), not variable fields.
- **Purpose:** Clause C06 rendering (conditions/obligations vary in scope).
- **Source:** STATIC_TEMPLATE (clause text) / USER_PROVIDED (which apply)
- **Applies To:** Each Case (rendered via clause selection).
- **Requirement Status:** PROPOSED — TO BE VALIDATED (exact obligation scope)
- **Cardinality:** 0..1 set per Case.
- **Source of Value:** Template clauses; scope confirmed by operator.
- **Verification:** Required (review of clause scope).
- **Used By:** C06; BR-036 [TO BE VALIDATED]; [TRACEABILITY REQUIRED] (§9.5 partial).

### 4.10 DN-DOC — Document and Date Information

> Bikram Sambat (BS) dates and generated-document metadata. All template dates are BS (इतिसम्बत YYYY महिना MMMM GG गते रोज N) — BR-019.

#### DN-DOC-01 — Agreement date — BS year

- **Domain:** Duration / Dates
- **Description:** Bikram Sambat year of the agreement (e.g., २०८३).
- **Purpose:** Date section S08.
- **Source:** SYSTEM_GENERATED (or operator-entered)
- **Applies To:** Each Case's document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per document.
- **Source of Value:** System (current BS date); operator-adjustable.
- **Verification:** Not required (system-generated).
- **Used By:** S08; BR-019; FR-LR-018, FR-LR-028.

#### DN-DOC-02 — Agreement date — Nepali month name

- **Domain:** Duration / Dates
- **Description:** Nepali month name (साउन, वैशाख, जेठ, ... चैत्र).
- **Purpose:** Date section S08.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each Case's document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per document.
- **Source of Value:** System (BS calendar).
- **Verification:** Not required.
- **Used By:** S08; BR-019.

#### DN-DOC-03 — Agreement date — BS day

- **Domain:** Duration / Dates
- **Description:** Day of the BS month (१–३२ depending on month).
- **Purpose:** Date section S08.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each Case's document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per document.
- **Source of Value:** System (BS calendar).
- **Verification:** Not required.
- **Used By:** S08; BR-019.

#### DN-DOC-04 — Agreement date — BS weekday (रोज १–७)

- **Domain:** Duration / Dates
- **Description:** Weekday in रोज N form (रोज १ = Sunday … रोज ७).
- **Purpose:** Date section S08.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each Case's document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per document.
- **Source of Value:** System (BS calendar).
- **Verification:** Not required.
- **Used By:** S08; BR-019.

#### DN-DOC-05 — Template identity and version

- **Domain:** Generated Draft / Finalized Document
- **Description:** Which template and version was used to generate the document.
- **Purpose:** Historical accuracy; version association (FR-LR-029, FR-LR-043).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each generated document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per generated document.
- **Source of Value:** System (template registry).
- **Verification:** Not required.
- **Used By:** FR-LR-029, FR-LR-043; UC-011, UC-016; DN-GEN-04.

#### DN-DOC-06 — Generation / finalization metadata

- **Domain:** Generated Draft / Finalized Document
- **Description:** Generation timestamp and (if finalized) finalization timestamp and operator.
- **Purpose:** Draft/finalized record metadata (SRS §9.10/9.11).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each generated document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per generated document (finalization part conditional).
- **Source of Value:** System + operator.
- **Verification:** Not required.
- **Used By:** FR-LR-036, FR-LR-039; UC-013; DN-GEN-02, DN-GEN-03.

### 4.11 DN-WIT — Witnesses

> Witness is a **repeatable entity**: 1–3 witnesses observed (name, address, age). DN-WIT-01..09 preserve the three observed slots (WITNESS_1..3). Rule (BR-008, updated 2026-08-13): minimum **one witness per party**, identified by name, age, and address; citizenship optional. BR-008 remains [UNVERIFIED — CANDIDATE DOMAIN RULE] pending legal confirmation.

#### DN-WIT-01 — Witness 1 name

- **Domain:** Witnesses
- **Description:** Full name of the first witness (may include relationship, e.g., "प्रथम पक्षको श्रीमती सम्जना महर्जन").
- **Purpose:** Witness section S06.
- **Source:** USER_PROVIDED
- **Applies To:** Witness slot 1 (repeatable entity).
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per case (slot 1); witness record repeatable 0..3.
- **Source of Value:** Client verbal / operator.
- **Verification:** Required.
- **Used By:** S06; BR-034; FR-LR-016; UC-008.

#### DN-WIT-02 — Witness 1 address

- **Domain:** Witnesses
- **Description:** Address of the first witness (e.g., "ल.पु.म.न.पा. वडा न २९ बस्ने").
- **Purpose:** Witness section S06.
- **Source:** USER_PROVIDED
- **Applies To:** Witness slot 1.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per case (slot 1).
- **Source of Value:** Client verbal / operator.
- **Verification:** Required.
- **Used By:** S06; BR-034; FR-LR-016; UC-008.

#### DN-WIT-03 — Witness 1 age

- **Domain:** Witnesses
- **Description:** Age of the first witness ("वर्ष N को").
- **Purpose:** Witness section S06.
- **Source:** USER_PROVIDED
- **Applies To:** Witness slot 1.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per case (slot 1).
- **Source of Value:** Client verbal / operator.
- **Verification:** Required.
- **Used By:** S06; BR-034; FR-LR-016; UC-008.

#### DN-WIT-04 — Witness 2 name

- **Domain:** Witnesses
- **Description:** Full name of the second witness.
- **Purpose:** Witness section S06.
- **Source:** USER_PROVIDED
- **Applies To:** Witness slot 2.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per case (slot 2).
- **Source of Value:** Client verbal / operator.
- **Verification:** Required.
- **Used By:** S06; BR-034; FR-LR-016; UC-008.

#### DN-WIT-05 — Witness 2 address

- **Domain:** Witnesses
- **Description:** Address of the second witness.
- **Purpose:** Witness section S06.
- **Source:** USER_PROVIDED
- **Applies To:** Witness slot 2.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per case (slot 2).
- **Source of Value:** Client verbal / operator.
- **Verification:** Required.
- **Used By:** S06; BR-034; FR-LR-016; UC-008.

#### DN-WIT-06 — Witness 2 age

- **Domain:** Witnesses
- **Description:** Age of the second witness.
- **Purpose:** Witness section S06.
- **Source:** USER_PROVIDED
- **Applies To:** Witness slot 2.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per case (slot 2).
- **Source of Value:** Client verbal / operator.
- **Verification:** Required.
- **Used By:** S06; BR-034; FR-LR-016; UC-008.

#### DN-WIT-07 — Witness 3 name

- **Domain:** Witnesses
- **Description:** Full name of the third witness (appears in one instance only).
- **Purpose:** Witness section S06.
- **Source:** USER_PROVIDED
- **Applies To:** Witness slot 3.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per case (slot 3).
- **Source of Value:** Client verbal / operator.
- **Verification:** Required.
- **Used By:** S06; BR-034; FR-LR-016; UC-008.

#### DN-WIT-08 — Witness 3 address

- **Domain:** Witnesses
- **Description:** Address of the third witness.
- **Purpose:** Witness section S06.
- **Source:** USER_PROVIDED
- **Applies To:** Witness slot 3.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per case (slot 3).
- **Source of Value:** Client verbal / operator.
- **Verification:** Required.
- **Used By:** S06; BR-034; FR-LR-016; UC-008.

#### DN-WIT-09 — Witness 3 age

- **Domain:** Witnesses
- **Description:** Age of the third witness.
- **Purpose:** Witness section S06.
- **Source:** USER_PROVIDED
- **Applies To:** Witness slot 3.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per case (slot 3).
- **Source of Value:** Client verbal / operator.
- **Verification:** Required.
- **Used By:** S06; BR-034; FR-LR-016; UC-008.

> **Repeatability:** the underlying model is a repeatable **Witness record** with fields name/address/age; slots 1–3 are the observed maximum. DN-WIT-01..09 map to `witness[N].name|address|age`.

### 4.12 DN-WRI — Writer / Preparer

> The person who drafted the document (लेखक / मसौदाकार). May be a party themselves ("लेखक प्रथम पक्ष सुनिल महर्जन आफै") or a third party; one instance includes a professional license number (प्र.प.नं. ३४६). The Writer is an identity in its own right (not necessarily a Client or Party).

#### DN-WRI-01 — Writer name

- **Domain:** Writer / Preparer
- **Description:** Name of the writer/scribe (लेखक / मसौदाकार).
- **Purpose:** Writer section S07.
- **Source:** USER_PROVIDED
- **Applies To:** Each Case's document.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per document.
- **Source of Value:** Operator.
- **Verification:** Not required (operator knows).
- **Used By:** S07; FR-LR-016; UC-008.

#### DN-WRI-02 — Writer professional license number

- **Domain:** Writer / Preparer
- **Description:** Professional license/registration number where the writer is a licensed scribe (प्र.प.नं. ३४६ observed).
- **Purpose:** Writer section S07 (conditional).
- **Source:** USER_PROVIDED
- **Applies To:** Licensed writers only.
- **Requirement Status:** PROPOSED — [OPEN QUESTION] whether this is a distinct data need (OQ-DN-03)
- **Cardinality:** 0..1 per document.
- **Source of Value:** Operator.
- **Verification:** Not required.
- **Used By:** S07; [TRACEABILITY REQUIRED] (no dedicated template/Field Dictionary field).

### 4.13 DN-SRC — Source Document Metadata

> Source Documents are inputs/evidence (Decision 007). They are distinct from Generated Drafts and Finalized Documents.

#### DN-SRC-01 — Document type label

- **Domain:** Source Documents
- **Description:** Operator-assigned type label (e.g., Citizenship Certificate / Nagarikta, Lalpurja, Company Registration Certificate).
- **Purpose:** Organization and extraction routing (FR-011).
- **Source:** USER_PROVIDED
- **Applies To:** Each source document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per source document.
- **Source of Value:** Operator (labels [TO BE VALIDATED]).
- **Verification:** Not required (label).
- **Used By:** UC-004; FR-009..012 (legacy), FR-LR-101..104.

#### DN-SRC-02 — Capture/upload timestamp

- **Domain:** Source Documents
- **Description:** When the document was captured/uploaded.
- **Purpose:** Provenance and audit.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each source document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per source document.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** UC-004.

#### DN-SRC-03 — File format

- **Domain:** Source Documents
- **Description:** Format of the captured/uploaded file (image, PDF).
- **Purpose:** Storage and retrieval.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each source document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per source document.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** UC-004.

#### DN-SRC-04 — Association to case

- **Domain:** Source Documents
- **Description:** The Case the source document is associated with.
- **Purpose:** Case-level evidence organization.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each source document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per source document (case association).
- **Source of Value:** System (operator captures within a case).
- **Verification:** Not required.
- **Used By:** UC-004; BR-046; FR-009..012.

#### DN-SRC-05 — Stored image/file

- **Domain:** Source Documents
- **Description:** The stored digital file/image of the source document.
- **Purpose:** Evidence; input to extraction and verification.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each source document.
- **Requirement Status:** CONFIRMED (retention [OPEN QUESTION] — see §10.5 interpretations)
- **Cardinality:** 1 per source document.
- **Source of Value:** Operator capture/upload.
- **Verification:** Not required.
- **Used By:** UC-004, UC-010 (side-by-side verification).

#### DN-SRC-06 — Association to client

- **Domain:** Source Documents
- **Description:** Association of a source document to a Client (in addition to its case association). Whether source documents are stored at the Client level, the Case level, or both is **[OPEN QUESTION] OQ-DN-08** — not resolved here.
- **Purpose:** Client-level evidence reuse.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each source document (where client-level storage is supported).
- **Requirement Status:** PROPOSED — [OPEN QUESTION]
- **Cardinality:** 0..1 per source document.
- **Source of Value:** Operator (UC-021).
- **Verification:** Not required.
- **Used By:** UC-021; BR-046; FR-LR-061.

### 4.14 DN-EXT — Extracted Data (Candidate Layer)

> The pre-verification layer (SRS §9.7). Values produced by manual entry or automated extraction are Candidate Data until verified. OCR/automated extraction is optional and not MVP-mandatory (FR-LR-019..022, OCR-001..006).

#### DN-EXT-01 — Extracted field identifier

- **Domain:** Extracted Data
- **Description:** The target data need / field the extracted value maps to (e.g., P1_FULL_NAME).
- **Purpose:** Binds candidate values to needs for verification and generation.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each extracted value.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per extracted value.
- **Source of Value:** System (field mapping, Template Analysis §10.1).
- **Verification:** Not required (system mapping).
- **Used By:** UC-009, UC-010; FR-LR-019..022.

#### DN-EXT-02 — Extracted candidate value

- **Domain:** Extracted Data
- **Description:** The value as extracted or entered (raw), before verification.
- **Purpose:** Retains the pre-verification value; becomes Verified Case Data upon confirmation.
- **Source:** EXTRACTED (automated) or PROVIDED (manual)
- **Applies To:** Each extracted value.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per extracted value.
- **Source of Value:** OCR/extraction output or operator entry.
- **Verification:** Required before use in generation (BR-014, OCR-004).
- **Used By:** UC-009, UC-010; FR-LR-019, FR-LR-020.

#### DN-EXT-03 — Source document reference

- **Domain:** Extracted Data / Provenance
- **Description:** Which source document the candidate value came from (if any).
- **Purpose:** Side-by-side verification; provenance.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each extracted value.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per extracted value (present when from a source document).
- **Source of Value:** System (link to DN-SRC).
- **Verification:** Not required.
- **Used By:** UC-010; DN-PROV.

#### DN-EXT-04 — Extraction method

- **Domain:** Extracted Data
- **Description:** How the value was obtained: manual entry or automated extraction (OCR). Supports the SRS data-source indicator (§9.7).
- **Purpose:** Provenance and trust assessment.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each extracted value.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per extracted value.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** UC-009, UC-010; FR-LR-022; DN-PROV.

#### DN-EXT-05 — Extraction confidence

- **Domain:** Extracted Data
- **Description:** Confidence indicator for automated extraction, where feasible. No threshold is defined (SRS §11.1 — thresholds deferred to Phase 0.8 research).
- **Purpose:** Operator guidance during verification.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Automated-extraction values only.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per extracted value.
- **Source of Value:** Extraction engine (where available).
- **Verification:** Not required.
- **Used By:** UC-009, UC-010; OCR-001..006.

#### DN-EXT-06 — Extraction / entry status

- **Domain:** Extracted Data
- **Description:** State of the candidate value: EXTRACTED / PROVIDED → REQUIRES_VERIFICATION → VERIFIED (or corrected). Reuses the data states of §2.3.
- **Purpose:** Track the data lifecycle.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each extracted value.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per extracted value.
- **Source of Value:** System (state machine).
- **Verification:** Not required (state).
- **Used By:** UC-010; §5.

### 4.15 DN-VER — Verified Case Data (Authoritative Layer)

> The authoritative structured data source for document generation (SRS §9.8). Only verified values are used in generation (BR-016, BR-017).

#### DN-VER-01 — Verified field and value

- **Domain:** Verified Case Data
- **Description:** The confirmed value for a data need, after operator review/correction.
- **Purpose:** Authoritative input to generation.
- **Source:** VERIFIED (result of verification)
- **Applies To:** Each data need with a verified value.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per verified value.
- **Source of Value:** Confirmed candidate value (DN-EXT-02) or operator-entered.
- **Verification:** N/A (this IS the verified layer).
- **Used By:** UC-011; BR-016, BR-017; FR-LR-021.

#### DN-VER-02 — Verification timestamp and operator

- **Domain:** Verified Case Data
- **Description:** Who verified and when.
- **Purpose:** Audit of the authoritative data layer.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each verified value.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per verified value.
- **Source of Value:** System + verifying operator.
- **Verification:** Not required.
- **Used By:** UC-010; FR-LR-021; DN-AUDIT.

#### DN-VER-03 — Correction history

- **Domain:** Verified Case Data
- **Description:** Record of corrections: original candidate value, corrected value, operator, timestamp.
- **Purpose:** Transparency and audit of corrections.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Corrected values only.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..* per verified value.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** UC-010; FR-LR-020; §9.8.

#### DN-VER-04 — Case association

- **Domain:** Verified Case Data
- **Description:** The Case the verified value belongs to.
- **Purpose:** Scoping verified data to a case.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each verified value.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per verified value.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** §9.8; UC-010.

#### DN-VER-05 — Verification state

- **Domain:** Verified Case Data
- **Description:** Marker that a value is VERIFIED (vs REQUIRES_VERIFICATION). Part of the data-state model (§2.3).
- **Purpose:** Gate for generation.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each verified value.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per value.
- **Source of Value:** System (state machine).
- **Verification:** Not required.
- **Used By:** UC-011; BR-016; FR-LR-021, FR-LR-030.

#### DN-VER-06 — Per-value data status marker

- **Domain:** Verified Case Data
- **Description:** The full data-state marker for any value: NOT_PROVIDED / PENDING / UNKNOWN / N/A / PROVIDED / EXTRACTED / REQUIRES_VERIFICATION / VERIFIED (§2.3).
- **Purpose:** Uniform handling of missing/unknown/pending/verified values across all needs.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Every data need value.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per value.
- **Source of Value:** System (state machine).
- **Verification:** Not required.
- **Used By:** §5; §7.2 scenario matrix; FR-LR-017, FR-LR-030.

### 4.16 DN-CLAUSE — Clauses

> Clause model derived from the template (§3.2, §9 of Template Analysis). A clause is identified, versioned content with text, a condition, and required data. See §6 for the full inventory and variable bindings.

#### DN-CLAUSE-01 — Clause identifier and version

- **Domain:** Clauses
- **Description:** Unique identifier (C01..C13) and version for each clause in the template.
- **Purpose:** Traceability of document content to template version.
- **Source:** SYSTEM_GENERATED (template registry)
- **Applies To:** Each clause definition.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per clause definition.
- **Source of Value:** Template (Administrator-managed, FR-LR-043).
- **Verification:** Not required.
- **Used By:** §6; FR-LR-025, FR-LR-029.

#### DN-CLAUSE-02 — Clause text

- **Domain:** Clauses
- **Description:** The clause text: static wording plus variable placeholders (e.g., property, rent).
- **Purpose:** Content of the generated document (S03).
- **Source:** STATIC_TEMPLATE (with placeholders)
- **Applies To:** Each clause definition.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per clause definition.
- **Source of Value:** Template.
- **Verification:** Not required (template-controlled).
- **Used By:** FR-LR-023, FR-LR-024; UC-011.

#### DN-CLAUSE-03 — Clause condition

- **Domain:** Clauses
- **Description:** When the clause is included, driven by data (e.g., usePurpose == agriculture selects C04/C11; construction present selects C03/C12).
- **Purpose:** Conditional generation.
- **Source:** STATIC_TEMPLATE (condition definition)
- **Applies To:** Conditional clauses only.
- **Requirement Status:** PROPOSED — conditions [TO BE VALIDATED] (OQ-DN-05, OQ-TA-01)
- **Cardinality:** 0..1 condition per clause.
- **Source of Value:** Template; validated with domain experts.
- **Verification:** Not required.
- **Used By:** §6.1; FR-LR-025; BR-027..033.

#### DN-CLAUSE-04 — Clause required data / variables

- **Domain:** Clauses
- **Description:** The data needs and variables a clause depends on (e.g., C02 depends on DN-RENT-01..07).
- **Purpose:** Missing-variable detection; generation completeness (FR-LR-030).
- **Source:** SYSTEM_GENERATED (template registry)
- **Applies To:** Each clause definition.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1..* per clause definition.
- **Source of Value:** Template variable model (§13).
- **Verification:** Not required.
- **Used By:** §6.2, §6.3; FR-LR-030; BR-017.

### 4.17 DN-VAR — Clause Variables

> The binding between data needs and clause placeholders (Template Analysis §13).

#### DN-VAR-01 — Variable name and binding

- **Domain:** Clause Variables
- **Description:** A named placeholder (e.g., `party.first.name`, `rent.amount`, `property.area.ropani`) bound to a data need (DN-P1-01, DN-RENT-01, DN-PROP-04).
- **Purpose:** Populates clause text from Verified Case Data.
- **Source:** SYSTEM_GENERATED (template registry)
- **Applies To:** Each variable in each clause.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1..* per clause.
- **Source of Value:** Template variable model (§13).
- **Verification:** Not required.
- **Used By:** FR-LR-024; UC-011.

#### DN-VAR-02 — Render behavior (required / optional-blank)

- **Domain:** Clause Variables
- **Description:** Whether a missing variable blocks generation (required) or renders as a blank placeholder (optional, e.g., age `वर्ष __`, blank Second Party in the WIP template).
- **Purpose:** Deterministic generation; aligns with FR-LR-030 and missing-data handling.
- **Source:** SYSTEM_GENERATED (template registry)
- **Applies To:** Each variable.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per variable.
- **Source of Value:** Template; per-field rules [TO BE VALIDATED].
- **Verification:** Not required.
- **Used By:** §6.3; FR-LR-030; UC-011.

### 4.18 DN-GEN — Generated Document Metadata (Draft and Finalized)

> Generated documents are outputs (Decision 007) and are distinct from Source Documents. Two states: **Generated Draft** and **Finalized Document**. Only human finalization creates a Finalized Document (Decision 008).

#### DN-GEN-01 — Document kind (Draft / Finalized)

- **Domain:** Generated Draft / Finalized Document
- **Description:** The type of generated document: Generated Draft or Finalized Document. Distinct and non-interchangeable (BR-045); only human-finalized documents are Finalized (BR-038, BR-047).
- **Purpose:** Document typing (FR-LR-062, FR-LR-063).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each generated document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per generated document.
- **Source of Value:** System (kind set by lifecycle, human finalization).
- **Verification:** Not required (kind transition is a workflow event).
- **Used By:** FR-LR-035, FR-LR-062, FR-LR-063; UC-013, UC-021; BR-038, BR-045, BR-047.

#### DN-GEN-02 — Draft generation timestamp

- **Domain:** Generated Draft
- **Description:** When the draft was generated.
- **Purpose:** Draft metadata (SRS §9.10).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each generated draft.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per generated draft.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** UC-011; FR-LR-023.

#### DN-GEN-03 — Finalization timestamp and operator

- **Domain:** Finalized Document
- **Description:** When and by whom the document was finalized.
- **Purpose:** Finalized record metadata (SRS §9.11).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each finalized document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per finalized document.
- **Source of Value:** System + finalizing operator.
- **Verification:** Not required.
- **Used By:** UC-013; FR-LR-036; BR-038.

#### DN-GEN-04 — Template identity and version

- **Domain:** Generated Draft / Finalized Document
- **Description:** Template and version used (shared with DN-DOC-05).
- **Purpose:** Historical association (FR-LR-029).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each generated document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per generated document.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** UC-011, UC-016; FR-LR-029, FR-LR-043.

#### DN-GEN-05 — Finalized document identifier and case association

- **Domain:** Finalized Document
- **Description:** Unique finalized-document identifier and the case it belongs to.
- **Purpose:** Identification and retrieval (SRS §10.6).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each finalized document.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per finalized document.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-039, FR-LR-040; UC-013, UC-014.

#### DN-GEN-06 — Output format / storage location

- **Domain:** Finalized Document
- **Description:** Output format and storage reference (PDF proposed, not prescribed; storage location per §9.11).
- **Purpose:** Printing/delivery and retrieval (FR-LR-031, FR-LR-038).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each finalized document.
- **Requirement Status:** CONFIRMED (format proposal [TO BE VALIDATED])
- **Cardinality:** 1 per finalized document.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-031, FR-LR-038; UC-013.

### 4.19 DN-AUDIT — Audit / Event Records

> Event history of significant actions (SRS §9.12).

#### DN-AUDIT-01 — Event type

- **Domain:** Audit / Event
- **Description:** The type of event (case created, data verified, draft generated, document finalized, document accessed, etc.).
- **Purpose:** Auditability (FR-LR-042).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Significant events.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per event record.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-042; UC-013, UC-014.

#### DN-AUDIT-02 — Event timestamp

- **Domain:** Audit / Event
- **Description:** When the event occurred.
- **Purpose:** Audit chronology.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each event record.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per event record.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-042.

#### DN-AUDIT-03 — Operator identity

- **Domain:** Audit / Event
- **Description:** Which operator performed the event.
- **Purpose:** Accountability.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each event record.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per event record (system events may record no operator).
- **Source of Value:** System (from DN-APP-01).
- **Verification:** Not required.
- **Used By:** FR-LR-042; DN-APP-01.

#### DN-AUDIT-04 — Case/document reference and details

- **Domain:** Audit / Event
- **Description:** The case/document the event refers to, plus details.
- **Purpose:** Audit trail linkage.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Each event record.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 reference per event record.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-042.

### 4.20 DN-PROV — Provenance

> A per-value provenance record answering "where did this value come from?" (§9.7, §9.8). This is a conceptual requirement; the exact storage is implementation detail.

#### DN-PROV-01 — Value provenance record

- **Domain:** Provenance
- **Description:** For any value: origin indicator (SOURCE_DERIVED / USER_PROVIDED / CALCULATED / SYSTEM_GENERATED), the source document or verbal source (via DN-EXT-03), extraction method (DN-EXT-04), and confidence (DN-EXT-05, where available).
- **Purpose:** Trust and audit of every document value.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Every value used in a document.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per value (may share record structure).
- **Source of Value:** System (composed from DN-EXT/DN-VER metadata).
- **Verification:** Not required.
- **Used By:** FR-LR-022; §9.7/9.8; [TRACEABILITY REQUIRED] (no dedicated SRS entry beyond §9.7/9.8).

#### DN-PROV-02 — Provenance query capability

- **Domain:** Provenance
- **Description:** The system can answer, per value, "where did this value come from?" (source document, method, confidence, verification).
- **Purpose:** Operator review and audit support.
- **Source:** SYSTEM_GENERATED (derived)
- **Applies To:** Case data and documents.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1 per Case (capability).
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** UC-010, UC-013; [TRACEABILITY REQUIRED].

### 4.21 DN-LIFE — Data and Document Lifecycle Needs

> Cross-cutting lifecycle needs (SRS §10). Retains the existing lifecycle needs and extends them to the Client/Party and extracted/verified layers.

#### DN-LIFE-01 — Retain Candidate Data (pre-verification values)

- **Domain:** Case Lifecycle
- **Description:** Candidate values (DN-EXT) are retained with origin, confidence, and original value. Permanent retention of originals is [OPEN QUESTION].
- **Purpose:** Traceability of the data lifecycle.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Candidate values.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..* per Case.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-019..022; UC-010; BR-014; §9.7.

#### DN-LIFE-02 — Retain Verified Case Data

- **Domain:** Case Lifecycle
- **Description:** Verified values (DN-VER) with verification timestamp, operator, and correction history are retained as the authoritative layer.
- **Purpose:** Authoritative input to generation; audit.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Verified values.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1..* per Case.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-021; UC-010; BR-016; §9.8.

#### DN-LIFE-03 — Retain draft generation/edit metadata

- **Domain:** Case Lifecycle
- **Description:** Draft generation timestamp and edit history. Whether previous draft versions are retained is [OPEN QUESTION].
- **Purpose:** Draft history (SRS §9.10, §10.4).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Generated drafts.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..* per Case.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-033; UC-012.

#### DN-LIFE-04 — Persist Finalized Documents

- **Domain:** Finalized Document / Case Lifecycle
- **Description:** Finalized documents are immutable and non-editable; revisions create new versions/cases (SRS §10.7).
- **Purpose:** Integrity of the authoritative output.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Finalized documents.
- **Requirement Status:** PROPOSED
- **Cardinality:** 1..* per Case.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-037; UC-013; BR-006.

#### DN-LIFE-05 — Audit records

- **Domain:** Audit / Event (cross-cutting)
- **Description:** Significant events recorded (DN-AUDIT): event, timestamp, operator, reference.
- **Purpose:** Auditability (SRS §9.12).
- **Source:** SYSTEM_GENERATED
- **Applies To:** Case and document activity.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..* per Case.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-042; UC-013, UC-014.

#### DN-LIFE-06 — Persist finalized Cases

- **Domain:** Case Lifecycle
- **Description:** Cases remain available after finalization for operational use; intended to be retained indefinitely (Decision 004). Exact retention, archival, backup, and deletion policies [TO BE VALIDATED]; no legal retention period is asserted.
- **Purpose:** Persistent, long-lived cases.
- **Source:** SYSTEM_GENERATED
- **Applies To:** Finalized cases.
- **Requirement Status:** CONFIRMED (policy [TO BE VALIDATED])
- **Cardinality:** 1..* retained cases.
- **Source of Value:** System.
- **Verification:** Not required.
- **Used By:** FR-LR-050; UC-003, UC-014; BR-039, BR-040; DN-CASE-09.

### 4.22 DN-P1 — First Party Information (Landlord / Lessor)

> Identity field set for a First Party individual. **Repeatable:** the First Party may consist of multiple co-owners (up to 3 observed); each co-owner repeats DN-P1-01..DN-P1-10. Field Dictionary: `P1_*` (Template Analysis §4.1).
>
> **Acquisition (§2.7):** First Party identity values may be entered manually (e.g., the landlord supplies information verbally; the notary-office operator types it), read from a source document (Citizenship Certificate, Lalpurja), or extracted by OCR then verified by the operator. No source document is required and OCR is never a precondition. Where a field is marked `Source: SOURCE_DERIVED`, the documented origin is the source document, but manual entry is permitted unless a field explicitly states otherwise.

#### DN-P1-01 — First Party full name

- **Domain:** Party — First Party
- **Description:** Landowner/lessor's full name.
- **Purpose:** Identity in preamble (S02) and signature area (S04).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each First Party individual (co-owner).
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per First Party individual; 1..3 First Party individuals per Case.
- **Source of Value:** Citizenship Certificate; Lalpurja.
- **Verification:** Required (high sensitivity).
- **Used By:** S02, S04, C01; FR-LR-010, FR-LR-011; UC-005.

#### DN-P1-02 — First Party grandfather

- **Domain:** Party — First Party
- **Description:** Grandfather's name (`[Grandfather]को नाती/नातिनी`).
- **Purpose:** Preamble lineage (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each First Party individual.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per individual (usually present).
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P1-03 — First Party father

- **Domain:** Party — First Party
- **Description:** Father's name (`[Father]को छोरा/छोरी`).
- **Purpose:** Preamble lineage (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each First Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per individual.
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P1-04 — First Party district

- **Domain:** Party — First Party
- **Description:** Home district.
- **Purpose:** Preamble address (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each First Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P1-05 — First Party municipality

- **Domain:** Party — First Party
- **Description:** Municipality / rural municipality (incl. "हाल परिवर्तित" changed address).
- **Purpose:** Preamble address (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each First Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P1-06 — First Party ward

- **Domain:** Party — First Party
- **Description:** Ward number.
- **Purpose:** Preamble address (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each First Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P1-07 — First Party age

- **Domain:** Party — First Party
- **Description:** Age in years. Often left blank in the template (`वर्ष __`).
- **Purpose:** Preamble identity (S02).
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Each First Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 0..1 per individual (blank placeholder acceptable per template [TO BE VALIDATED]).
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required when present.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P1-08 — First Party citizenship number

- **Domain:** Party — First Party
- **Description:** Citizenship number (ना.प्र.न.), when present.
- **Purpose:** Preamble identity (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each First Party individual.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per individual (not present in all instances).
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required (high sensitivity).
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P1-09 — First Party citizenship issue date

- **Domain:** Party — First Party
- **Description:** Citizenship issue date (BS), when citizenship number present.
- **Purpose:** Preamble identity (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each First Party individual.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P1-10 — First Party citizenship issue district

- **Domain:** Party — First Party
- **Description:** District where citizenship was issued.
- **Purpose:** Preamble identity (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Each First Party individual.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P1-11 — First Party signature name

- **Domain:** Party — First Party
- **Description:** Name as written in the signature area (S04). Same as DN-P1-01 in practice.
- **Purpose:** Signature block.
- **Source:** SYSTEM_GENERATED / USER_PROVIDED
- **Applies To:** Each First Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per First Party individual.
- **Source of Value:** Derived from DN-P1-01; operator-adjustable.
- **Verification:** Not required (rendering).
- **Used By:** S04.

### 4.23 DN-P2 — Second Party Information (Tenant / Lessee)

> Identity field set for a Second Party. Individual variant uses DN-P2-01..11; **company variant (CONDITIONAL)** uses DN-P2-12..16. Field Dictionary: `P2_*`.
>
> **Acquisition (§2.7):** Second Party identity values may be entered manually, read from a source document, or extracted by OCR then verified. The tenant frequently supplies only verbal/written information and no document; manual entry must fully support this (§2.7 path 3). Where a field is marked `Source: SOURCE_DERIVED`, the documented origin is the source document, but manual entry is permitted unless a field explicitly states otherwise.

#### DN-P2-01 — Second Party full name

- **Domain:** Party — Second Party
- **Description:** Tenant/lessee's full name (individual). Blank in the Ram Maharjan WIP template.
- **Purpose:** Identity in preamble (S02) and signature area (S05).
- **Source:** SOURCE_DERIVED
- **Applies To:** Second Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Second Party individual (0 in blank-template mode).
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required (high sensitivity).
- **Used By:** S02, S05, C01; FR-LR-010; UC-005.

#### DN-P2-02 — Second Party grandfather

- **Domain:** Party — Second Party
- **Description:** Grandfather's name.
- **Purpose:** Preamble lineage (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Second Party individual.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per individual.
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P2-03 — Second Party father

- **Domain:** Party — Second Party
- **Description:** Father's name.
- **Purpose:** Preamble lineage (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Second Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per individual.
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P2-04 — Second Party district

- **Domain:** Party — Second Party
- **Description:** Home district.
- **Purpose:** Preamble address (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Second Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P2-05 — Second Party municipality

- **Domain:** Party — Second Party
- **Description:** Municipality / rural municipality.
- **Purpose:** Preamble address (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Second Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P2-06 — Second Party ward

- **Domain:** Party — Second Party
- **Description:** Ward number.
- **Purpose:** Preamble address (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Second Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P2-07 — Second Party age

- **Domain:** Party — Second Party
- **Description:** Age in years (often blank `वर्ष __`).
- **Purpose:** Preamble identity (S02).
- **Source:** SOURCE_DERIVED / USER_PROVIDED
- **Applies To:** Second Party individual.
- **Requirement Status:** CONFIRMED
- **Cardinality:** 0..1 per individual (blank placeholder acceptable per template [TO BE VALIDATED]).
- **Source of Value:** Citizenship Certificate / verbal.
- **Verification:** Required when present.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P2-08 — Second Party citizenship number

- **Domain:** Party — Second Party
- **Description:** Citizenship number (ना.प्र.न.).
- **Purpose:** Preamble identity (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Second Party individual.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required (high sensitivity).
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P2-09 — Second Party citizenship issue date

- **Domain:** Party — Second Party
- **Description:** Citizenship issue date (BS).
- **Purpose:** Preamble identity (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Second Party individual.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P2-10 — Second Party citizenship issue district

- **Domain:** Party — Second Party
- **Description:** District where citizenship was issued.
- **Purpose:** Preamble identity (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Second Party individual.
- **Requirement Status:** PROPOSED
- **Cardinality:** 0..1 per individual.
- **Source of Value:** Citizenship Certificate.
- **Verification:** Required.
- **Used By:** S02; FR-LR-010; UC-005.

#### DN-P2-11 — Second Party signature name

- **Domain:** Party — Second Party
- **Description:** Name as written in the signature area (S05). For the company variant, the signature name is the proprietor's name (DN-P2-16).
- **Purpose:** Signature block.
- **Source:** SYSTEM_GENERATED / USER_PROVIDED
- **Applies To:** Second Party (individual or company).
- **Requirement Status:** CONFIRMED
- **Cardinality:** 1 per Second Party.
- **Source of Value:** Derived from DN-P2-01 (individual) or DN-P2-16 (company).
- **Verification:** Not required (rendering).
- **Used By:** S05.

#### DN-P2-12 — Company name

- **Domain:** Party — Second Party (company variant)
- **Description:** Company/organization name (e.g., स्यबा मल्टिपर्पोज एग्रो हब्स एण्ड रिसर्च सेन्टर).
- **Purpose:** Preamble for entity tenants (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Company Second Parties (CONDITIONAL).
- **Requirement Status:** CONDITIONAL
- **Cardinality:** 1 per company Second Party.
- **Source of Value:** Company Registration Certificate.
- **Verification:** Required.
- **Used By:** S02; BR-030; FR-LR-012; UC-005.

#### DN-P2-13 — Company registration number

- **Domain:** Party — Second Party (company variant)
- **Description:** Company registration number (द.नं.).
- **Purpose:** Preamble for entity tenants (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Company Second Parties (CONDITIONAL).
- **Requirement Status:** CONDITIONAL
- **Cardinality:** 1 per company Second Party.
- **Source of Value:** Company Registration Certificate.
- **Verification:** Required.
- **Used By:** S02; BR-030; FR-LR-012; UC-005.

#### DN-P2-14 — Company registration date

- **Domain:** Party — Second Party (company variant)
- **Description:** Company registration date (BS/AD format varies).
- **Purpose:** Preamble for entity tenants (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Company Second Parties (CONDITIONAL).
- **Requirement Status:** CONDITIONAL
- **Cardinality:** 1 per company Second Party.
- **Source of Value:** Company Registration Certificate.
- **Verification:** Required.
- **Used By:** S02; BR-030; FR-LR-012; UC-005.

#### DN-P2-15 — Company registrar office

- **Domain:** Party — Second Party (company variant)
- **Description:** Company Registrar's Office (कम्पनी रजिष्ट्रारको कार्यालय).
- **Purpose:** Preamble for entity tenants (S02).
- **Source:** SOURCE_DERIVED
- **Applies To:** Company Second Parties (CONDITIONAL).
- **Requirement Status:** CONDITIONAL
- **Cardinality:** 1 per company Second Party.
- **Source of Value:** Company Registration Certificate.
- **Verification:** Required.
- **Used By:** S02; BR-030; FR-LR-012; UC-005.

#### DN-P2-16 — Company proprietor

- **Domain:** Party — Second Party (company variant)
- **Description:** Proprietor name (प्रप्राइतर) representing the company; also used as the signature name (S05).
- **Purpose:** Preamble identity and signature block for entity tenants.
- **Source:** SOURCE_DERIVED
- **Applies To:** Company Second Parties (CONDITIONAL).
- **Requirement Status:** CONDITIONAL
- **Cardinality:** 1 per company Second Party.
- **Source of Value:** Company Registration Certificate.
- **Verification:** Required.
- **Used By:** S02, S05; BR-030; FR-LR-012; UC-005.

---

## 5. Data States and the Candidate → Verified Lifecycle

### 5.1 Data States

Every value in a Case carries one of the data states defined in §2.3 (NOT_PROVIDED / PENDING / UNKNOWN / N/A / PROVIDED / EXTRACTED / REQUIRES_VERIFICATION / VERIFIED). The transition model:

```
                     ┌─────────────────────────────┐
   NOT_PROVIDED ──▶ PENDING ──▶ PROVIDED ─────────┐
        │                                          │
        │                                        REQUIRES_VERIFICATION ──▶ VERIFIED
        └──────────▶ UNKNOWN (explicitly unstated)             ▲
        └──────────▶ N/A (not applicable)                      └── corrected (operator)
```

- **NOT_PROVIDED → PROVIDED/EXTRACTED:** value entered manually or produced by extraction.
- **PROVIDED/EXTRACTED → REQUIRES_VERIFICATION:** candidate awaiting human confirmation.
- **REQUIRES_VERIFICATION → VERIFIED:** operator confirms (or corrects, then confirms).
- **NOT_PROVIDED → UNKNOWN:** operator explicitly marks a value as unknown/unstated (blank placeholders like `वर्ष __`).
- **N/A:** set when a conditional variant does not apply (e.g., company fields for an individual).

### 5.2 Effects on Generation and Finalization

| State | Generation (draft) | Finalization | Rule |
|---|---|---|---|
| VERIFIED | Value used | Permitted | BR-016, FR-LR-021 |
| REQUIRES_VERIFICATION | Value not used — blocked | Blocked | BR-014, OCR-004, BR-016 |
| PROVIDED / EXTRACTED | Not used until verified | Blocked | FR-LR-019..022 |
| NOT_PROVIDED | Required fields block; optional fields blank | Blocked if mandatory missing | FR-LR-030, BR-017 |
| UNKNOWN | Blank placeholder if template permits (e.g., age) | [TO BE VALIDATED] for mandatory fields | §4.22/4.23 notes |
| N/A | Excluded (conditional not active) | Permitted | §2.6 |

### 5.3 Case Lifecycle States

Retained minimum set (DN-CASE-02): **Created → In Progress → Draft Generated → Under Review → Finalized → Persistent**. SRS FR-007 was aligned to this set on 2026-08-13 (the earlier finer-grained states `Data Collection`, `Verification`, and `Archived/Closed` were removed). "In Progress" covers data collection and verification activity. Finalized cases persist for operational use (Decision 004).

---

## 6. Clause and Variable Model

### 6.1 Clause Inventory (LAND_RENT template)

Clause identifiers (C01–C13) referenced throughout this document. Derived from Template Analysis §3.2, §9, and the reference PDF.

| Clause ID | Topic | Section | Content | Condition | Status |
|---|---|---|---|---|---|
| C01 | Land description, offer & acceptance | S03 (Clause 1) | Property (district, ward, kitta, area), use purpose, term, offer/acceptance formula | — | CONFIRMED |
| C02 | Rent, escalation & payment | S03 (Clause 2) | Rent figures + words, period, escalation rate/period/method, payment timing | — | CONFIRMED (method [TO BE VALIDATED]) |
| C03 | Physical structure construction (permission) | S03 | Permission to build structures | usePurpose agriculture/business | CONFIRMED |
| C04 | Prohibited crops / restricted use | S03 | No government-prohibited agricultural production | usePurpose = agriculture | CONFIRMED |
| C05 | Subletting prohibition | S03 | No re-renting to third parties | — | CONFIRMED |
| C06 | Tax & expense responsibilities | S03 | Rent tax, utilities, construction tax, waste management → Second Party | — | CONFIRMED (scope [TO BE VALIDATED]) |
| C07 | Uninterrupted use (First Party obligation) | S03 | First Party permits undisturbed use during term | — | CONFIRMED |
| C08 | Notice & termination | S03 | Notice period(s); may be asymmetric per party | notice period set | CONFIRMED |
| C09 | Amendment by mutual consent | S03 | Terms changeable by mutual agreement | — | CONFIRMED (4 instances) |
| C10 | Governing law | S03 | Prevailing law applies beyond written terms | — | CONFIRMED |
| C11 | Agriculture restoration | S03 | Land returned in cultivable condition | usePurpose = agriculture | CONFIRMED |
| C12 | Structure handover after term | S03 | Structures demolished/cleared on expiry | business/construction present | CONFIRMED |
| C13 | Renewal / new agreement after term | S03 | New agreement made by mutual consent after expiry | observed in one instance | TO BE VALIDATED |

### 6.2 Variable Chain

```
Data Need (DN-XXX, VERIFIED)
   → Clause Variable (DN-VAR-01, e.g., party.first.name, rent.amount)
   → Clause (DN-CLAUSE, C01..C13)
   → Generated Document (DN-GEN)
```

Examples: `DN-P1-01 → party.first.name → C01/C02 preamble → Generated Draft`; `DN-RENT-01/DN-RENT-02 → rent.amount/rent.amountWords → C02 → Generated Draft`; `DN-PROP-04 → property.area.ropani/anna/paisa/dam → C01 → Generated Draft`.

### 6.3 Missing-Variable Detection

- If a **required** variable for an included clause has no VERIFIED value, generation is blocked and the missing fields are reported (FR-LR-030, BR-017, UC-011 alt flow).
- If a variable is **optional-blank** (DN-VAR-02), generation proceeds with a blank placeholder where the template permits it (observed: age `वर्ष __`, citizenship details when absent, whole Second Party in the blank WIP template).
- The Case can remain **In Progress** while required values are missing; finalization is blocked for incomplete or unreviewed documents (FR-LR-045).

---

## 7. Coverage Matrices

### 7.1 Template Field Coverage Matrix

Legend — **Status:** CONFIRMED / PROPOSED / TO BE VALIDATED / [UNRESOLVED]. `[UNRESOLVED]` marks template or SRS fields with no clean data-need mapping. Conditional flags indicate when the field applies.

| Data Need | Template Field | Entity | Required/Optional | Conditional? | Source | Verification | Clause Usage | Status |
|---|---|---|---|---|---|---|---|---|
| DN-P1-01 | P1_FULL_NAME | First Party | Required | Multi co-owner | SOURCE_DERIVED | Required | S02, S04, C01 | CONFIRMED |
| DN-P1-02 | P1_GRANDFATHER | First Party | Optional | — | SOURCE_DERIVED | Required | S02 | PROPOSED |
| DN-P1-03 | P1_FATHER | First Party | Required | — | SOURCE_DERIVED | Required | S02 | CONFIRMED |
| DN-P1-04 | P1_DISTRICT | First Party | Required | — | SOURCE_DERIVED | Required | S02 | CONFIRMED |
| DN-P1-05 | P1_MUNICIPALITY | First Party | Required | — | SOURCE_DERIVED | Required | S02 | CONFIRMED |
| DN-P1-06 | P1_WARD | First Party | Required | — | SOURCE_DERIVED | Required | S02 | CONFIRMED |
| DN-P1-07 | P1_AGE | First Party | Optional | Blank placeholder | SOURCE_DERIVED / USER_PROVIDED | Required when present | S02 | CONFIRMED |
| DN-P1-08 | P1_CITIZENSHIP_NUM | First Party | Optional | When present | SOURCE_DERIVED | Required | S02 | PROPOSED |
| DN-P1-09 | P1_CITIZENSHIP_DATE | First Party | Optional | When number present | SOURCE_DERIVED | Required | S02 | PROPOSED |
| DN-P1-10 | P1_CITIZENSHIP_DIST | First Party | Optional | When number present | SOURCE_DERIVED | Required | S02 | PROPOSED |
| DN-P1-11 | P1_SIGNATURE_NAME | First Party | Required | — | SYSTEM_GENERATED / USER_PROVIDED | Not required | S04 | CONFIRMED |
| DN-P2-01 | P2_FULL_NAME | Second Party | Required | Blank in WIP template | SOURCE_DERIVED | Required | S02, S05, C01 | CONFIRMED |
| DN-P2-02 | P2_GRANDFATHER | Second Party | Optional | — | SOURCE_DERIVED | Required | S02 | PROPOSED |
| DN-P2-03 | P2_FATHER | Second Party | Required | — | SOURCE_DERIVED | Required | S02 | CONFIRMED |
| DN-P2-04 | P2_DISTRICT | Second Party | Required | — | SOURCE_DERIVED | Required | S02 | CONFIRMED |
| DN-P2-05 | P2_MUNICIPALITY | Second Party | Required | — | SOURCE_DERIVED | Required | S02 | CONFIRMED |
| DN-P2-06 | P2_WARD | Second Party | Required | — | SOURCE_DERIVED | Required | S02 | CONFIRMED |
| DN-P2-07 | P2_AGE | Second Party | Optional | Blank placeholder | SOURCE_DERIVED / USER_PROVIDED | Required when present | S02 | CONFIRMED |
| DN-P2-08 | P2_CITIZENSHIP_NUM | Second Party | Optional | When present | SOURCE_DERIVED | Required | S02 | PROPOSED |
| DN-P2-09 | P2_CITIZENSHIP_DATE | Second Party | Optional | When number present | SOURCE_DERIVED | Required | S02 | PROPOSED |
| DN-P2-10 | P2_CITIZENSHIP_DIST | Second Party | Optional | When number present | SOURCE_DERIVED | Required | S02 | PROPOSED |
| DN-P2-11 | P2_SIGNATURE_NAME | Second Party | Required | — | SYSTEM_GENERATED / USER_PROVIDED | Not required | S05 | CONFIRMED |
| DN-P2-12 | P2_COMPANY_NAME | Second Party (company) | Conditional | Second Party is company | SOURCE_DERIVED | Required | S02 | CONDITIONAL |
| DN-P2-13 | P2_COMPANY_REG | Second Party (company) | Conditional | Second Party is company | SOURCE_DERIVED | Required | S02 | CONDITIONAL |
| DN-P2-14 | P2_COMPANY_REG_DATE | Second Party (company) | Conditional | Second Party is company | SOURCE_DERIVED | Required | S02 | CONDITIONAL |
| DN-P2-15 | P2_COMPANY_REG_OFFICE | Second Party (company) | Conditional | Second Party is company | SOURCE_DERIVED | Required | S02 | CONDITIONAL |
| DN-P2-16 | P2_COMPANY_PROPRIETOR | Second Party (company) | Conditional | Second Party is company | SOURCE_DERIVED | Required | S02, S05 | CONDITIONAL |
| DN-PROP-01 | PROP_DISTRICT | Property | Required | — | SOURCE_DERIVED | Required | C01 | CONFIRMED |
| DN-PROP-02 | PROP_WARD | Property | Required | — | SOURCE_DERIVED | Required | C01 | CONFIRMED |
| DN-PROP-03 | PROP_KITTA_NUM | Property | Required | Multi-kitta | SOURCE_DERIVED | Required | C01 | CONFIRMED |
| DN-PROP-04 | PROP_AREA | Property | Required | Per kitta | SOURCE_DERIVED | Required | C01 | CONFIRMED (storage structure [UNRESOLVED] OQ-DN-01) |
| DN-PROP-05 | PROP_TYPE_LAND | Property | Optional | Guthi etc. | SOURCE_DERIVED | Required | C01 | PROPOSED |
| DN-PROP-06 | PROP_USE_PURPOSE | Property | Required | Clause selection | USER_PROVIDED | Not required | C01, C03, C04, C11, C12 | CONFIRMED (list [TO BE VALIDATED]) |
| DN-RENT-01 | RENT_AMOUNT | Rent | Required | — | USER_PROVIDED | Required | C02 | CONFIRMED |
| DN-RENT-02 | RENT_AMOUNT_WORDS | Rent | Required | — | CALCULATED | Required | C02 | CONFIRMED |
| DN-RENT-03 | RENT_PERIOD | Rent | Required | monthly/annual | USER_PROVIDED | Required | C02 | CONFIRMED |
| DN-RENT-04 | RENT_ESCALATION_RATE | Rent | Optional | When escalation | USER_PROVIDED | Required | C02 | CONFIRMED |
| DN-RENT-05 | RENT_ESCALATION_PERIOD | Rent | Optional | When escalation | USER_PROVIDED | Required | C02 | CONFIRMED |
| DN-RENT-06 | RENT_PAYMENT_TIMING | Rent | Optional | — | USER_PROVIDED | Required | C02 | CONFIRMED |
| DN-RENT-07 | RENT_ESCALATION_METHOD | Rent | Optional | When escalation | USER_PROVIDED | Required | C02 | PROPOSED |
| DN-RENT-08 | TERM_DURATION | Term | Required | — | USER_PROVIDED | Required | C01 | CONFIRMED |
| DN-RENT-09 | NOTICE_PERIOD | Term | Required | Per-party possible | USER_PROVIDED | Required | C08 | CONFIRMED |
| DN-WIT-01..03 | WITNESS_1_NAME/_ADDRESS/_AGE | Witness | Optional | 1–3 witnesses | USER_PROVIDED | Required | S06 | PROPOSED |
| DN-WIT-04..06 | WITNESS_2_NAME/_ADDRESS/_AGE | Witness | Optional | 1–3 witnesses | USER_PROVIDED | Required | S06 | PROPOSED |
| DN-WIT-07..09 | WITNESS_3_NAME/_ADDRESS/_AGE | Witness | Optional | 1–3 witnesses | USER_PROVIDED | Required | S06 | PROPOSED |
| DN-WRI-01 | WRITER_NAME | Writer | Optional | — | USER_PROVIDED | Not required | S07 | PROPOSED |
| DN-DOC-01 | DATE_YEAR | Document | Required | — | SYSTEM_GENERATED | Not required | S08 | CONFIRMED |
| DN-DOC-02 | DATE_MONTH | Document | Required | — | SYSTEM_GENERATED | Not required | S08 | CONFIRMED |
| DN-DOC-03 | DATE_DAY | Document | Required | — | SYSTEM_GENERATED | Not required | S08 | CONFIRMED |
| DN-DOC-04 | DATE_WEEKDAY | Document | Required | — | SYSTEM_GENERATED | Not required | S08 | CONFIRMED |
| — | WRITER_LICENSE_NUM (observed, not in Field Dictionary) | Writer | Optional | Licensed writer | USER_PROVIDED | Not required | S07 | [UNRESOLVED] (see OQ-DN-03) |
| — | Property deposit amount (SRS §9.5) | Rent | — | Not in template | — | — | — | [UNRESOLVED] (no template evidence) |
| — | Lease start date (SRS §9.5) | Term | — | Implied "आजको मितिले" | — | — | C01 | [UNRESOLVED] (implied, not a field) |
| — | Utility responsibilities (SRS §9.5) | Rent | — | Clause-level (C06) | — | — | C06 | [UNRESOLVED] (clause, not field) |
| — | Party contact info (SRS §9.4) | Party | — | Not in template | — | — | — | [UNRESOLVED] (contradicts template — see §8.2) |
| — | Witness citizenship number (SRS §9.4) | Witness | — | Not in template | — | — | — | **RESOLVED 2026-08-13** — optional per updated BR-008 (name/age/address sufficient; citizenship optional); no data need required |

### 7.2 Scenario Coverage (16 scenarios)

Scenarios combine **party presence** (M1–M4) with **data state** (S1–S4). Outcome columns describe whether the case may proceed to generation and finalization under current rules. Mandatory-field blank finalization is [TO BE VALIDATED].

| # | Party presence | Data state | Data Needs affected | Generation | Finalization | Notes / evidence |
|---|---|---|---|---|---|---|
| 1 | M1 — both parties present | S1 — all required data VERIFIED | DN-P1/P2, DN-PROP, DN-RENT | Permitted | Permitted | Normal executed agreement (filled examples) |
| 2 | M1 — both parties present | S2 — data complete but REQUIRES_VERIFICATION | DN-EXT-02, DN-VER-05/06 | Blocked until verified | Blocked | BR-016, OCR-004; verification required |
| 3 | M1 — both parties present | S3 — some required data NOT_PROVIDED | Missing fields (FR-LR-030) | Blocked; gaps reported | Blocked | BR-017; operator supplies or flags unresolved |
| 4 | M1 — both parties present | S4 — some data UNKNOWN | Optional fields (e.g., age) | Permitted with placeholders | Permitted for optional blanks; mandatory blanks [TO BE VALIDATED] | Template uses `वर्ष __` for age |
| 5 | M2 — First Party present, Second Party absent | S1 — P1 data VERIFIED | DN-P2 set NOT_PROVIDED | Blocked (Second Party identity missing) | Blocked | Case may stay In Progress; tenant must be identified |
| 6 | M2 — First Party present, Second Party absent | S2 — P1 data pending verification | DN-P1 REQUIRES_VERIFICATION | Blocked | Blocked | Verify First Party data first |
| 7 | M2 — First Party present, Second Party absent | S3 — P1 required data missing | DN-P1 gaps | Blocked | Blocked | FR-LR-030 |
| 8 | M2 — First Party present, Second Party absent | S4 — some P1 data UNKNOWN | DN-P1 optional | Partial draft possible; Second Party still blocks | Blocked | Blank-tenant draft only for WIP-style placeholders [TO BE VALIDATED] |
| 9 | M3 — Second Party present, First Party absent | S1 — P2 data VERIFIED | DN-P1 set NOT_PROVIDED | Blocked | Blocked | Landlord identity required for valid agreement |
| 10 | M3 — Second Party present, First Party absent | S2 — P2 data pending verification | DN-P2 REQUIRES_VERIFICATION | Blocked | Blocked | — |
| 11 | M3 — Second Party present, First Party absent | S3 — P2 required data missing | DN-P2 gaps | Blocked | Blocked | FR-LR-030 |
| 12 | M3 — Second Party present, First Party absent | S4 — some P2 data UNKNOWN | DN-P2 optional | Partial draft possible; First Party still blocks | Blocked | — |
| 13 | M4 — neither party identified | S1 — (no party data) | DN-PTY, DN-P1/P2 | Blocked | Blocked | Early case / blank WIP template state |
| 14 | M4 — neither party identified | S2 — n/a (no party data) | — | Blocked | Blocked | No parties, no draft |
| 15 | M4 — neither party identified | S3 — case/property/rent data may exist | DN-PROP, DN-RENT, DN-CASE | Blocked | Blocked | Data collection in progress |
| 16 | M4 — neither party identified | S4 — data UNKNOWN/unstated | All identity needs | Blocked | Blocked | Blank WIP template (Ram Maharjan) is a template, not a completed document |

### 7.3 Land-Rent Variation Coverage

Every variation supported by the project evidence is listed with its data needs and affected clauses. Unverified variations are marked.

| # | Variation | Observed values | Data Needs | Clauses | Status |
|---|---|---|---|---|---|
| 1 | Use purpose | agriculture, business, residence, business+residence | DN-PROP-06 | C01, C03, C04, C11, C12 | CONFIRMED (full list [TO BE VALIDATED] OQ-DN-05) |
| 2 | Rent period | monthly (मासिक), annual (वार्षिक) | DN-RENT-03 | C02 | CONFIRMED |
| 3 | Escalation rate | 5%, 10% | DN-RENT-04 | C02 | CONFIRMED |
| 4 | Escalation period | every year, every 2 years, after 2 years | DN-RENT-05 | C02 | CONFIRMED |
| 5 | Escalation method | compound (चक्रवृद्धि) | DN-RENT-07 | C02 | PROPOSED — [TO BE VALIDATED] |
| 6 | Notice period | 30 days, 60 days, 3 months, 6 months (asymmetric per party in one instance) | DN-RENT-09 | C08 | CONFIRMED |
| 7 | Second Party type | individual, company | DN-P2-01..11, DN-P2-12..16 | S02, S05 | CONFIRMED |
| 8 | First Party multiplicity | 1, 3 co-owners | DN-P1 (repeat) | S02, S04 | CONFIRMED |
| 9 | Kitta multiplicity | single, two kitta | DN-PROP-03 | C01 | CONFIRMED |
| 10 | Land registration category | private, Guthi (भवानी गुठि), ज.ध. महल | DN-PROP-05, DN-OWN-02 | C01 | PROPOSED — [TO BE VALIDATED] (BR-033) |
| 11 | Writer | a party themselves, third party, professional with license | DN-WRI-01, DN-WRI-02 | S07 | PROPOSED |
| 12 | Witness count | 1–3 | DN-WIT | S06 | CONFIRMED (template); legal minimum [OPEN QUESTION] |
| 13 | Term duration | 3, 5, 10 years | DN-RENT-08 | C01 | CONFIRMED |
| 14 | Structure construction clause | present / absent | — (clause-level) | C03, C12 | CONFIRMED |
| 15 | Renewal clause | present in one instance | — (clause-level) | C13 | TO BE VALIDATED |
| 16 | Missing/blank party (WIP) | entire Second Party blank | DN-P2 (all) | S02 | CONFIRMED only as blank WIP template; finalization with blank party [TO BE VALIDATED] |

### 7.4 Information Acquisition Matrix (§2.7)

Per-field acquisition rules for every data need group. Columns: **Manual** = manual entry permitted; **Doc** = value obtainable from a source document; **OCR** = value may be extracted by OCR (into Candidate Data); **Client** = value reusable/pre-fillable from an existing Client record; **Condition** = any conditionality / source restriction; **Status** = `CONFIRMED` (evidence supports) or `[TO BE VALIDATED]` (no project evidence yet).

| Group | Manual | Doc | OCR | Client | Condition / Notes | Status |
|---|---|---|---|---|---|---|
| DN-CLI (Client identity) | YES | YES | YES | n/a (origin of reuse) | Client may exist with **no** source documents (OQ-DN-17). Reused via DN-PTY-02 → DN-CASE-08. | CONFIRMED |
| DN-PTY (role, type, link) | YES | n/a | n/a | n/a | Role assigned during case setup; Party-to-Client link optional (0..1). | CONFIRMED |
| DN-P1 (First Party identity) | YES | YES | YES | YES | Preamble/signature (S02/S04); co-owner repeat. Manual entry permitted even with `Source: SOURCE_DERIVED`. | CONFIRMED |
| DN-P2 (Second Party identity) | YES | YES | YES | YES | Tenant frequently has no document; manual entry fully supported. | CONFIRMED |
| DN-PROP (property, kitta, use purpose) | YES | YES | YES | n/a | Property data typically from Lalpurja; manual entry permitted. | CONFIRMED |
| DN-RENT (rent terms) | YES | YES | YES | n/a | Terms usually agreed verbally/written; deposit modeled as clause (OQ-DN-13). | CONFIRMED |
| DN-OWN (ownership) | YES | YES | YES | n/a | From Lalpurja/papers; category values partially unverified (BR-033). | CONFIRMED — [TO BE VALIDATED] |
| DN-CASE (case metadata) | YES | n/a | n/a | n/a | System-generated identifiers; type/user/description operator-set. | CONFIRMED |
| DN-EXT (extraction metadata) | n/a | n/a | YES | n/a | Records extraction results incl. manual (PROVIDED) values; OCR is Candidate Data, never final. | CONFIRMED |
| DN-VER (verification metadata) | n/a | n/a | n/a | n/a | Operator verification required before Verified state (FR-LR-021). | CONFIRMED |
| DN-CLAUSE / DN-VAR | n/a | n/a | n/a | n/a | Derived from verified case data; clause presence conditional (§2.6). | CONFIRMED |
| DN-SRC (source document) | n/a | YES | n/a | n/a | **Optional** — a case/Client may have zero source documents. Storage level Client-vs-Case is OQ-DN-08. | CONFIRMED |
| DN-GEN / DN-DOC (generation, document) | n/a | n/a | n/a | n/a | Generation consumes **Verified Case Data** regardless of acquisition path (§2.7). | CONFIRMED |
| DN-WIT (witness) | YES | YES | YES | n/a | Witness info entered/recorded; count rules OQ-DN-16. | CONFIRMED |
| DN-WRI (writer) | YES | YES | YES | n/a | Professional license number unverified in evidence (OQ-DN-03). | CONFIRMED — [TO BE VALIDATED] |
| DN-PAY (payment/receipt) | YES | YES | YES | n/a | Receipt-based; entered or extracted. | CONFIRMED |
| DN-APP / DN-AUDIT / DN-PROV | n/a | n/a | n/a | n/a | System/operator metadata; provenance is internal audit, **not** automatic document content (§2.7). | CONFIRMED |

> **Reading the matrix:** "YES" means the path is permitted; it is never required that all paths be used. Per-field values default to the group's paths; where a specific field is more restrictive, the field's own entry states so. Fields lacking project evidence are marked `[TO BE VALIDATED]` rather than silently assumed. OCR availability for any path does not create a case-creation or generation dependency (BR-050, FR-LR-004).

---

## 8. Traceability

### 8.1 Group-Level Traceability

| DN Group | Related FR-LR | Related UC | Related BR | SRS §9 Reference | Status |
|---|---|---|---|---|---|
| DN-APP | FR-LR-001..003, FR-LR-048 | UC-001, UC-015 | BR-003, BR-037 | §9.1 | PROPOSED |
| DN-CLI | FR-LR-055..061 | UC-017..021 | BR-037, BR-043, BR-044, BR-046 | §9.13 | CONFIRMED/PROPOSED |
| DN-PTY | FR-LR-010..012, FR-LR-058..060 | UC-005, UC-019, UC-020 | BR-043, BR-044 | §9.2, §9.4 | PROPOSED — [TRACEABILITY REQUIRED] (role model not explicitly in SRS) |
| DN-CASE | FR-LR-004..009, FR-LR-049..054 | UC-002, UC-003, UC-014 | BR-039, BR-040, BR-041 | §9.2 | CONFIRMED |
| DN-CTYPE | FR-LR-049, FR-LR-053 | UC-002, UC-003 | BR-041, BR-042 | §9.14 | CONFIRMED |
| DN-PROP | FR-LR-013, FR-LR-018 | UC-006 | BR-020 | §9.3 | CONFIRMED |
| DN-OWN | (none dedicated) | UC-006 | BR-033 | §9.3 | PROPOSED — [TRACEABILITY REQUIRED] |
| DN-RENT | FR-LR-014, FR-LR-015, FR-LR-018 | UC-007 | BR-021..026, BR-029 | §9.5 | CONFIRMED (escalation [TO BE VALIDATED]) |
| DN-PAY | (none dedicated) | UC-007 | BR-036 | §9.5 | PROPOSED — [TRACEABILITY REQUIRED] (partial) |
| DN-DOC | FR-LR-018, FR-LR-028, FR-LR-029 | UC-011, UC-013 | BR-019 | §9.9, §9.10, §9.11 | CONFIRMED |
| DN-WIT | FR-LR-016 | UC-008 | BR-034 | §9.4 | PROPOSED — SRS §9.4 aligned 2026-08-13 (min 1 witness/party; name, age, address; citizenship optional) |
| DN-WRI | FR-LR-016 | UC-008 | — | §9.4 | PROPOSED — [TRACEABILITY REQUIRED] for DN-WRI-02 |
| DN-SRC | FR-009..012, FR-LR-101..104, FR-LR-061 | UC-004, UC-021 | BR-045, BR-046 | §9.6 | CONFIRMED |
| DN-EXT | FR-LR-019..022 | UC-009, UC-010 | BR-014 | §9.7 | PROPOSED |
| DN-VER | FR-LR-019..022, FR-LR-030 | UC-010, UC-011 | BR-016, BR-017 | §9.8 | PROPOSED |
| DN-CLAUSE | FR-LR-023..030 | UC-011 | BR-017, BR-025..033 | §9.9 | PROPOSED |
| DN-VAR | FR-LR-024 | UC-011 | — | §9.9; Template Analysis §13 | PROPOSED |
| DN-GEN | FR-LR-023..040, FR-LR-062, FR-LR-063 | UC-011, UC-012, UC-013 | BR-038, BR-045, BR-047 | §9.10, §9.11, §9.15 | CONFIRMED |
| DN-AUDIT | FR-LR-042 | UC-013, UC-014 | — | §9.12 | PROPOSED |
| DN-PROV | FR-LR-022 | UC-010 | — | §9.7, §9.8 | PROPOSED — [TRACEABILITY REQUIRED] (no dedicated SRS entry) |
| DN-LIFE | FR-LR-050, FR-LR-054 | UC-002, UC-003, UC-014 | BR-039, BR-040 | §10.1..§10.11 | CONFIRMED (policy [TO BE VALIDATED]) |

> Cross-artifact consistency: this inventory is consistent with `Traceability/Case Client Document Traceability.md` (Decisions 004–008 → FR → UC → DN → BR). New groups (DN-EXT, DN-VER, DN-CLAUSE, DN-VAR, DN-AUDIT, DN-PROV) map to existing SRS §9.7/9.8/9.9/9.12 sections; DN-PTY, DN-OWN, DN-PAY are only partially covered by SRS §9 and are marked [TRACEABILITY REQUIRED].

### 8.2 Detected Contradictions (flagged, not auto-resolved)

| # | Source A | Source B | Issue | Handling |
|---|---|---|---|---|
| 1 | SRS §9.4: Lessor/Lessee include "contact" | Template Field Dictionary (§4.1) | No contact fields exist in the template | Flagged [UNRESOLVED] in §7.1; no SRS edit (out of scope); logged as open question OQ-DN-11 |
| 2 | ~~SRS §9.4: "Witnesses: ... citizenship number (at least two per party)"~~ | Template: witnesses carry name/address/age only; 1–3 total | **RESOLVED 2026-08-13** — SRS §9.4 and BR-008 aligned: minimum one witness per party; name, age, address; citizenship optional (project owner). Template supports 1–3 slots. | SRS §9.4 + BR-008 updated; OQ-DN-12 closed |
| 3 | SRS §9.5: deposit amount, utility responsibilities as rental terms | Template: no deposit field; utilities are clause-level obligations (C06) | Deposit is not template-backed | Flagged [UNRESOLVED] in §7.1; logged as OQ-DN-13 |

---

## 9. Open Questions

| ID | Question | Reference |
|---|---|---|
| OQ-DN-01 | Should area be stored as structured Ropani-Anna-Paisa-Dam fields or as a single text string? | OQ-TA-17 |
| OQ-DN-02 | Should addresses be structured (district/municipality/ward) or free text? | OQ-TA-19 |
| OQ-DN-03 | Should writer professional license number be a distinct data need? | DN-WRI-02; §7.1 |
| OQ-DN-04 | Should the system support both Ropani and Square Meter area systems? | OQ-TA-18 |
| OQ-DN-05 | What is the complete list of use purposes? | OQ-TA-20; §7.3 #1 |
| OQ-DN-06 | Should original Candidate Data values be retained permanently? | SRS §9.8; DN-LIFE-01 |
| OQ-DN-07 | Which fields does a reusable Client record contain beyond the Field Dictionary party fields? No new fields are invented here. | TO BE VALIDATED |
| OQ-DN-08 | Should Source Documents be stored/associated at the Client level, the Case level, or both? (**[OPEN QUESTION]** — not resolved here) | SRS §9.6; DN-SRC-06; BR-046 |
| OQ-DN-09 | What rules govern updating a Client's information after a Case has been finalized? | FR-LR-055..061 |
| OQ-DN-10 | What is the exact retention, archival, backup, and deletion policy for finalized Cases and finalized documents? Finalized cases are intended to be retained indefinitely for operational use. | Decision 004; DN-LIFE-06 |
| OQ-DN-11 | SRS §9.4 lists "contact" for parties; the template has no contact field. Should contact be added, or is the SRS entry to be trimmed? | §8.2 #1 |
| OQ-DN-12 | ~~SRS §9.4 listed witness citizenship numbers and "at least two witnesses per party" vs the template's name/address/age, 1–3 total.~~ **RESOLVED 2026-08-13** — BR-008 updated: minimum one witness per party; name, age, address; citizenship optional. SRS §9.4 aligned. | §8.2 #2; BR-008 |
| OQ-DN-13 | SRS §9.5 lists deposit amount and utility responsibilities as rental terms; the template has no deposit field and treats utilities as clause obligations. Should these be modeled as data needs or clause content? | §8.2 #3 |
| OQ-DN-14 | Should multiple Second Party individuals be supported (repeatable Second Party)? First Party co-owners are observed; Second Party multiplicity is symmetric but unobserved. | §2.4 |
| OQ-DN-15 | Are Bikram Sambat dates legally required, or are AD dates also acceptable? | OQ-TA-16; §8.3 Template Analysis |
| OQ-DN-16 | What determines the number of witnesses? Is there a legal minimum? | **Partial resolution 2026-08-13** — minimum one witness per party per BR-008 (candidate domain rule, pending legal confirmation). Template provides up to 3 witness slots. | OQ-TA-03, OQ-TA-14; BR-008 |
| OQ-DN-17 | How is a person who has **no reusable Client record and no source document** represented? Options: (a) a Client record created with manually entered data and zero source documents; (b) a case-scoped Party with no Client record and no document; (c) another concept. The requirements do not auto-resolve this; the choice affects Client reuse, source-document association (OQ-DN-08), and long-term storage. Must not mean "person cannot be represented." | §2.7; DN-CLI, DN-PTY-02; FR-LR-058..061 |

---

## 10. Quality Review Summary

| Check | Result |
|---|---|
| No duplicate data needs | PASS — 133 data needs; each maps to a distinct field/meaning |
| Every Field Dictionary §4.1 field mapped | PASS — see §7.1 (all 56 Field Dictionary fields covered) |
| Template fields with no mapping | NONE — every Field Dictionary field maps to a data need; observed-but-unlisted fields (writer license) are flagged [UNRESOLVED] with OQ-DN-03 |
| Client vs Application User not conflated | PASS — §2.2; distinct groups DN-CLI vs DN-APP |
| Client vs Party not conflated | PASS — §2.2; DN-CLI (reusable) vs DN-PTY (per-case role) |
| Case Type ≠ use purpose ≠ document type | PASS — DN-CTYPE, DN-PROP-06, DN-GEN/SRC/DOC kept distinct (BR-042) |
| Missing/absent party scenarios modeled | PASS — §2.3, §7.2 (16 scenarios) |
| Multi-party / repeatable records modeled | PASS — DN-P1 co-owners, DN-P2 company variant, DN-WIT repeatable, DN-PROP multi-kitta |
| Extracted vs verified data layers separated | PASS — DN-EXT (candidate) vs DN-VER (authoritative); DN-LIFE-01/02 |
| Provenance modeled | PASS — DN-PROV; per-value "where did this value come from?" |
| Clause system with variables and conditions | PASS — DN-CLAUSE, DN-VAR; §6.1–6.3; conditional pattern §2.6 |
| Missing-variable detection | PASS — §6.3; FR-LR-030 / BR-017 alignment |
| Case lifecycle minimum states present | PASS — Created / In Progress / Draft Generated / Under Review / Finalized (DN-CASE-02, §5.3) |
| Retention consistent with Decision 004, no invented legal retention | PASS — DN-CASE-09, DN-LIFE-06; BR-040 |
| OQ-CM-04 (client vs case-level source docs) preserved as open | PASS — OQ-DN-08, DN-SRC-06, BR-046 |
| SRS/BR/UC contradictions checked | PASS — §8.2 (3 flagged; none auto-resolved; no SRS edits made) |
| Traceability gaps marked | PASS — [TRACEABILITY REQUIRED] markers for DN-PTY, DN-OWN, DN-PAY, DN-PROV, DN-WRI-02 |
| No source document required to represent a party | PASS — §2.7, §7.4, DN-CLI/DN-PTY notes; manual entry first-class (OQ-DN-17) |
| OCR not a prerequisite for case creation or generation | PASS — §2.7, §7.4 note, DN-EXT/DN-VER separation (BR-050, FR-LR-004) |
| Manual entry (incl. Nepali Unicode) modeled as first-class | PASS — §2.7 path 3; DN-P1/DN-P2 acquisition notes (FR-LR-064) |
| Provenance not automatically document content | PASS — §2.7; DN-PROV internal/audit only |
| Cross-document reference updates needed | 1 — `Traceability/Case Client Document Traceability.md` references "Data Needs §9.14"; section numbering changed in this finalization pass (see §11 note) |

### Summary counts (this document)

- **Data needs before finalization:** 98 (DN-P1 11, DN-P2 16, DN-PROP 6, DN-RENT 9, DN-WIT 9, DN-WRI 1, DN-DOC 6, DN-CASE 9, DN-SRC 6, DN-CLI 10, DN-CTYPE 3, DN-GEN 6, DN-LIFE 6)
- **Data needs after finalization:** 133 — all 98 preserved unchanged in meaning; **35 added** (DN-APP 3, DN-PTY 3, DN-OWN 2, DN-PAY 2, DN-EXT 6, DN-VER 6, DN-CLAUSE 4, DN-VAR 2, DN-WRI-02 1, DN-AUDIT 4, DN-PROV 2); 0 merged/removed
- **Data need groups:** 23 (was 13)
- **Conceptual domains covered:** 22 (all listed in §3, with evidence and status)
- **Template fields mapped:** 56/56 Field Dictionary fields; 6 additional observed/SRS fields flagged [UNRESOLVED]
- **Scenarios covered:** 16 (§7.2)
- **Land-rent variations covered:** 16 (§7.3)
- **Open questions:** 17 (OQ-DN-01..17; OQ-DN-08 = OQ-CM-04 preserved as open)
- **Acquisition paths modeled:** 5 (source document, OCR/extraction, manual entry, combination, existing Client info — §2.7) with per-group acquisition matrix §7.4
- **Contradictions flagged:** 3 (§8.2)
- **Docs modified outside this file:** 1 reference fix in `Traceability/Case Client Document Traceability.md` (section number only)

---

## 11. Note on Section Numbering

The section numbering of this document changed during the 2026-08-08 finalization pass (the previous version had Case Type and Generated Document Metadata at §9.14/§9.15). Any external reference to the old numbering should be read against the new structure. One such reference (`Traceability/Case Client Document Traceability.md`) is fixed by a minimal edit.
