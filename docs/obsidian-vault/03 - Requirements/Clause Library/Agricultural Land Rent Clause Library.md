# Agricultural Land Rent Clause Library

> **Working Analysis Document** — This library catalogues, in verbatim source wording, the clauses found in the project's agricultural land-rent reference documents. It is a source-derived domain-analysis artifact, NOT a legal document, and it does not claim legal authority. Corrupt or ambiguous source text is preserved and marked; nothing is silently corrected; every gap is reported using the vocabulary defined in the [[Clause Library Schema]].

| Field | Value |
|---|---|
| **Document Status** | Draft — Source Extraction Complete |
| **Date** | 2026-08-13 |
| **Domain** | AGR — Agricultural Land Rent |
| **Primary Sources** | `private/Reference Documents/Land Rent - WIP.pdf` (20 pages; 8 instance documents) |
| **Schema** | [[Clause Library Schema]] |
| **Related Analysis** | `Land Rent Template Analysis.md`, `Data Needs.md` §6 |
| **Scope** | Clauses found in the **agricultural-purpose** instances only; business/residential instances are catalogued as context |

---

## 1. Purpose and Scope

This library answers: **"Which clauses appear in the supplied agricultural land-rent reference documents, in which instances, with which variables, and how do they trace to the existing requirements set?"**

- Scope is limited to the **5 agricultural-purpose instances** in the supplied PDF.
- The 3 business/residential instances are listed as context and are **not** the basis of any `CLAUSE-AGR-###` entry (they contain clauses that also appear in agricultural instances; those overlaps are noted as context evidence only).
- No implementation, no redesign, no invented legal rules, no legal conclusions. Where the sources do not support an answer, this library says so.

---

## 2. Source Documents

The single supplied reference file is `private/Reference Documents/Land Rent - WIP.pdf` (PDF 1.4, 20 pages, Skia/PDF m152 Google Docs Renderer). It contains **8 instance documents** extracted with `pdftotext -layout`. (`Land Rent Template Analysis.md` §1.1/§17.1 previously stated "7 instances (6 complete, 1 partially blank)"; corrected to 8 on 2026-08-13 — see CON-01.)

| SD ID | Instance label (file header) | Parties (P1 / P2) | Use purpose | Clauses | Agricultural? |
|---|---|---|---|---|---|
| SD-01 | Land Rent for Agriculture (Satya Raj Maharjan) | Sunil Maharjan / Dawa Tamang | कृषि (agriculture) | 9 | **YES** |
| SD-02 | Land Rent (Satya Ram Maharjan) | Bikhi Maharjan / Budha Bahadur Tamang (company: Syabaa Multipurpose Agro Hubs & Research Centre) | कृषि (agriculture) | 8 | **YES** |
| SD-03 | (no file header) | Gangalal Maharjan (3 co-owners) / Juhi Khan | व्यापार व्यवसाय तथा बसोबास (business + residence) | 7 | No (context) |
| SD-04 | (no file header) — re-typed variant of SD-03, clause 2 duplicated | Gangalal Maharjan (3 co-owners) / Juhi Khan | व्यापार व्यवसाय तथा बसोबास (business + residence) | 7 (clause 2 duplicated: two renderings) | No (context) |
| SD-05 | Tab 5 | Dhan Raj Maharjan / Ramila Thapa Magar | कृषि (agriculture) | 7 | **YES** |
| SD-06 | (header "as") | Shyam Man Maharjan / Bishwor Maharjan | व्यवोसाय (business) | 6 | No (context) |
| SD-07 | Tab 7 | Sunil Maharjan / Dawa Tamang (same parties as SD-01) | कृषि (agriculture) | 9 | **YES** |
| SD-08 | Ram Maharjan | Ram Maharjan / **Second Party blank (WIP)** | कृषि (agriculture) | 9 | **YES** |

**Agricultural source set (primary):** SD-01, SD-02, SD-05, SD-07, SD-08.
**Context set (secondary):** SD-03, SD-04, SD-06.

> **Source limitation:** Only this one physical file was supplied. Statements such as "universal across instances" mean universal across the 5 agricultural instances of this single file; they do not claim frequency in the wider domain. The task guidance to not rely on a single example is recorded here as a domain-validation question (OQ-CL-10).

---

## 3. Status Legend

| Mark | Meaning |
|---|---|
| **Source-Derived** | Clause present verbatim in the cited source instance(s); wording verified against extraction. |
| **Needs Review** | Unresolved ambiguity/contradiction requiring human review. |
| **Draft** | Not yet checked against source. |
| **Validated** | Source-derived AND confirmed externally (not achievable from supplied sources). |
| `⟨sic⟩` | Source renders this string in this (likely erroneous) form; preserved verbatim, reader hypothesis offered, never silently corrected. |
| `Not established from supplied sources.` | Cannot be determined from the supplied references. |
| `Condition requires validation.` | Condition suspected but not proven by the sources. |

---

## 4. Clause Index

| ID | Clause | Category | Applicability | Variables | Sources | Status |
|---|---|---|---|---|---|---|
| CLAUSE-AGR-001 | Party Identification and Designation (Preamble) | Preamble — Party | All land-rent agreements (all 5 agricultural instances) | 20 party-identity variables + 5 company variables (conditional) | SD-01, SD-02, SD-05, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-002 | Legal Basis and Execution (Preamble) | Preamble — Legal Basis & Execution | All land-rent agreements | None (static wording; two source forms) | SD-01, SD-02, SD-05, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-003 | Land Description, Offer and Acceptance | Property & Grant | All land-rent agreements | property.district, property.ward, property.kittaNumber[], property.area.*, property.landCategory, property.usePurpose, term.durationYears | SD-01, SD-02, SD-05, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-004 | Rent, Escalation and Payment | Rent & Payment | All land-rent agreements | rent.amount, rent.amountWords, rent.period, rent.escalation.rate, rent.escalation.period, rent.paymentTiming, rent.escalation.method | SD-01, SD-02, SD-05, SD-07, SD-08 | Needs Review (financial formulas unvalidated) |
| CLAUSE-AGR-005 | Physical Structure Construction (permission) | Party Obligations | Present in 4/5 agricultural instances (SD-01, SD-02, SD-07, SD-08) | property.usePurpose (trigger) | SD-01, SD-02, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-006 | Prohibited Crops / Restricted Use | Land Use & Cultivation | Present in all 5 agricultural instances; two source forms (prohibited-crops form vs prohibited-acts→void form) | None | SD-01, SD-02, SD-05, SD-07, SD-08 | Source-Derived (wording variant) |
| CLAUSE-AGR-007 | Prohibition on Subletting | Subletting & Third Parties | All land-rent agreements (all 5 agricultural instances; clause position varies) | None | SD-01, SD-02, SD-05, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-008 | Tax and Expense Responsibilities | Party Obligations | All land-rent agreements (scope varies: rent tax only vs utilities+rent tax+construction tax+waste) | None (clause-level obligations) | SD-01, SD-02, SD-05, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-009 | Uninterrupted Use (First Party obligation) | Party Obligations | Present in 3/5 agricultural instances (SD-01, SD-07, SD-08) | None | SD-01, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-010 | Notice and Termination | Termination & Notice | All land-rent agreements (uniform 60 days vs asymmetric 3/6 months) | term.noticePeriod | SD-01, SD-02, SD-05, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-011 | Amendment by Mutual Consent | General Provisions | Present in 4/5 agricultural instances (SD-01, SD-02, SD-07, SD-08) | None | SD-01, SD-02, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-012 | Governing Law (residual) | General Provisions | Present in 4/5 agricultural instances (SD-01, SD-02, SD-07, SD-08) | None | SD-01, SD-02, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-013 | Agricultural Restoration on Exit | Land Use & Cultivation | Present in 4/5 agricultural instances (SD-01, SD-02, SD-07, SD-08) | None | SD-01, SD-02, SD-07, SD-08 | Source-Derived |
| CLAUSE-AGR-014 | Structure Handover After Term | Party Obligations | Present in 1/5 agricultural instances (SD-05); common in business context (SD-03/04/06) | None | SD-05 | Source-Derived (rare in agricultural set) |
| CLAUSE-AGR-015 | Compliance and Breach Remedy | General Provisions | Present in 1/5 agricultural instances (SD-05) | None | SD-05 | Source-Derived (rare in agricultural set) |

---

## 5. Clause Entries

### CLAUSE-AGR-001 — Party Identification and Designation (Preamble)

**Status:** Source-Derived · **Legal validation:** Not assessed · **Domain validation:** Source-confirmed (domain validation of lineage-format requirement required — see OQ-CL-02)

**Category:** Preamble — Party

**Applicability:** All land-rent agreements (present in all 5 agricultural instances; also in business/residential context instances).

**Canonical Source Text** (SD-01; lineage + address + citizenship + party-designation formula):

> लिखितम [P1_GRANDFATHER]को नाती [P1_FATHER]को छोरा [P1_DISTRICT] [P1_MUNICIPALITY] वडा न. [P1_WARD] बस्ने वर्ष [P1_AGE] को [P1_FULL_NAME] ना.प्र.न. [P1_CITIZENSHIP_NUM] जारी मिति [P1_CITIZENSHIP_DATE] [P1_CITIZENSHIP_DIST] (जसलाई यस लिखतमा प्रथम पक्ष भनि सम्बोधन गरिएको) र [P2_GRANDFATHER]को नाती [P2_FATHER]को छोरा [P2_DISTRICT] जिल्ला [P2_MUNICIPALITY] वडा न. [P2_WARD] बस्ने वर्ष [P2_AGE] को [P2_FULL_NAME] ना.प्र.न. [P2_CITIZENSHIP_NUM] जारी मिति [P2_CITIZENSHIP_DATE] [P2_CITIZENSHIP_DIST] (जसलाई यस लिखतमा द्रितिय पक्ष भनि सम्बोधन गरिएको) का बीचमा

**Source Rendering Notes:** The extraction renders `द ुवै` with spacing artifacts (PDF rendering artifact, not a correction). "द्रितिय" (SD-01/SD-05/SD-07/SD-08) and "द्वितीय" (SD-02/SD-03/SD-04) both occur for "Second Party"; both preserved.

**Variables:**

| Variable | Description | Source Evidence | Data Need ID | Field ID | Required? | Notes |
|---|---|---|---|---|---|---|
| party.first.grandfather | P1 grandfather name | "गजव महर्जनको नाती" (SD-01) | DN-P1-02 | P1_GRANDFATHER | Optional | Blank in some instances |
| party.first.father | P1 father name | "नन्द बहादुर महर्जनको छोरा" (SD-01) | DN-P1-03 | P1_FATHER | Yes | |
| party.first.name | P1 full name | "सुनिल महर्जन" (SD-01) | DN-P1-01 | P1_FULL_NAME | Yes | |
| party.first.address.district | P1 district | "ल.पु." (SD-01) | DN-P1-04 | P1_DISTRICT | Yes | |
| party.first.address.municipality | P1 municipality | "हरिसिद्धि वडा न. ६ हाल परिवर्तित ल.पु.म.न.पा" (SD-01) | DN-P1-05 | P1_MUNICIPALITY | Yes | "हाल परिवर्तित" (currently-changed) form present |
| party.first.address.ward | P1 ward | "वडा न. २८" (SD-01) | DN-P1-06 | P1_WARD | Yes | |
| party.first.age | P1 age | "बस्ने वर्ष __ को" (SD-01) | DN-P1-07 | P1_AGE | Optional | Blank `__` in most instances |
| party.first.citizenship.number | P1 citizenship number | "ना.प्र.न. ००२०७१" (SD-01) | DN-P1-08 | P1_CITIZENSHIP_NUM | Conditional | Absent in some instances |
| party.first.citizenship.issueDate | P1 citizenship issue date (BS) | "जारी मिति २०५७/१२/०९" (SD-01) | DN-P1-09 | P1_CITIZENSHIP_DATE | Conditional | |
| party.first.citizenship.issueDistrict | P1 citizenship issue district | "ल.पु." (SD-01) | DN-P1-10 | P1_CITIZENSHIP_DIST | Conditional | |
| party.second.grandfather | P2 grandfather | "सितल सिंह तामांगको नाती" (SD-01) | DN-P2-02 | P2_GRANDFATHER | Optional | |
| party.second.father | P2 father | "बधु तामांगको छोरा" (SD-01) | DN-P2-03 | P2_FATHER | Yes | |
| party.second.name | P2 full name | "दावा तामांग" (SD-01) | DN-P2-01 | P2_FULL_NAME | Yes | Blank in SD-08 (WIP) |
| party.second.address.district | P2 district | "दोलखा जिल्ला" (SD-01) | DN-P2-04 | P2_DISTRICT | Yes | |
| party.second.address.municipality | P2 municipality | "सुरी गाविस" (SD-01) | DN-P2-05 | P2_MUNICIPALITY | Yes | |
| party.second.address.ward | P2 ward | "वडा न. ९" (SD-01) | DN-P2-06 | P2_WARD | Yes | |
| party.second.age | P2 age | "बस्ने वर्ष __ को" (SD-01) | DN-P2-07 | P2_AGE | Optional | |
| party.second.citizenship.number | P2 citizenship number | "ना.प्र.न. २२-०१-७९-१९०" (SD-01) | DN-P2-08 | P2_CITIZENSHIP_NUM | Conditional | |
| party.second.citizenship.issueDate | P2 citizenship issue date (BS) | "जारी मिति २०७९/०८/०३" (SD-01) | DN-P2-09 | P2_CITIZENSHIP_DATE | Conditional | |
| party.second.citizenship.issueDistrict | P2 citizenship issue district | "दोलखा" (SD-01) | DN-P2-10 | P2_CITIZENSHIP_DIST | Conditional | |
| party.second.company.name | P2 company name | "स्यबा मल्टिपर्पोज एग्रो हब्स एण्ड रिसर्च सेन्टर" (SD-02) | DN-P2-12 | P2_COMPANY_NAME | Conditional | When P2 is a company |
| party.second.company.registrationNo | P2 company registration no. | "द.नं.:२४९०८३/०७७/०७८" (SD-02) | DN-P2-13 | P2_COMPANY_REG | Conditional | |
| party.second.company.registrationDate | P2 company registration date | "मिति:२०७७-०८-२१" (SD-02) | DN-P2-14 | P2_COMPANY_REG_DATE | Conditional | |
| party.second.company.registrarOffice | P2 company registrar office | "कम्पनी रजिष्ट्रारको कार्यालय- ___________" (SD-02) | DN-P2-15 | P2_COMPANY_REG_OFFICE | Conditional | Blank in source |
| party.second.company.proprietor | P2 company proprietor | "प्रप्राइतर बुद्धिबहादुर तामांग" (SD-02) | DN-P2-16 | P2_COMPANY_PROPRIETOR | Conditional | |

**Conditions:**
- Company variables apply **when the Second Party is a company** (observed in SD-02). `Condition requires validation.` for the general trigger, though company presence in SD-02 is source-confirmed.
- Lineage (grandfather/father) present in all instances but blank-capable for grandfather and age; whether lineage is legally required is `Not established from supplied sources.` (OQ-CL-02).

**Variants:**
- **Wording:** `द्रितिय` (SD-01/05/07/08) vs `द्वितीय` (SD-02/03/04) for "Second Party".
- **Structural:** "हाल परिवर्तित" (currently-changed address) appears in SD-01, SD-07, SD-08; not in SD-02/SD-05.
- **Structural (context):** SD-03/SD-04 have 3 First-Party co-owners (repeatable P1); SD-02 has company P2. Both documented in Template Analysis §5.1/§5.2.

**Related Data Needs:** DN-P1-01..10, DN-P2-01..10, DN-P2-12..16, DN-PTY-01..03
**Related Business Rules:** BR-031 (multi-party), BR-030 (company party)
**Related Use Cases:** UC-005, UC-019
**Related Functional Requirements:** FR-LR-010, FR-LR-011, FR-LR-012, FR-LR-024

**Open Questions:** OQ-CL-02 (lineage format legal requirement), OQ-CL-03 (citizenship presence/absence)

**Validation Notes:**
- **Source-derived fact:** Every agricultural instance opens with the lineage→name→address→citizenship→party-designation formula; Second Party designation uses "द्रितिय/द्वितीय पक्ष".
- **Domain interpretation:** The blank `वर्ष __` (age) and blankable citizenship indicate these are optional-blank render positions (consistent with DN-VAR-02 optional-blank behavior).
- **Project decision:** Party representation need not depend on a source document (BR-048/BR-049, Decisions 006/007).

---

### CLAUSE-AGR-002 — Legal Basis and Execution (Preamble)

**Status:** Source-Derived · **Legal validation:** Not assessed (statutory references preserved verbatim; their validity is `Not established from supplied sources.`) · **Domain validation:** Source-confirmed

**Category:** Preamble — Legal Basis & Execution

**Applicability:** All land-rent agreements (all 5 agricultural instances).

**Canonical Source Text** (SD-01; the "Muluki Civil Code" form):

> जग्गा बहालमा लिने दिने सम्बन्धमा मुलुकी देवानी सहिंता ऐन २०७४, मुलुकी कार्यबिधि ऐन २०७४ को करार ऐन भाग ५ बमोजिम परिपालन गर्ने गरी दुवै पक्षको सहमतिमा प्रथम पक्षको घर बैठकमा बसी । लेखि लेखाई दुवै पक्षले दाया दाया बाया सहिछाप गरी एक/एक प्रति लियौ दियौ । साक्षी तपसिलमा मानिस सदर ।

**Second Source Form** (SD-05; the "Muluki Civil (Code) Act 2074" form — used in SD-05 and the business context instances SD-03/04/06):

> तपसिलमा उल्लेखित जग्गा भाडामा लिने दिने समबन्धमा देहाय बमोजिम लेखेको शर्तहरु पूर्ण रुपमा परिपालन गर्ने गरि मुलुकी देवानी (सहिता) ऐन २०७४ को अधिनमा रहने गरि प्रथम पक्षको घर बैठकमा बसी यो करारनामा कागज तयार पारि सहि छाप समेत गरि एक एक प्रति बुझीलियौँ दियौँ। साक्षि तपसिलका मानिस सदर।

**Variables:** None (static preamble wording).

**Conditions:** `Condition requires validation.` for which legal-basis form is used when (SD-01/02/07/08 vs SD-05). The two forms coexist in the agricultural source set.

**Variants:**
- **Wording:** `सहिंता` (SD-01/07/08) vs `सहिता` (SD-02/05) vs `संहिता` (SD-03); `कार्यबिधि` (SD-01/07/08) vs `कार्यविधि` (SD-02); "करार ऐन भाग ५" (SD-01/07/08) vs "मुलुकी देवानी (सहिता) ऐन २०७४ को अधिनमा रहने" (SD-02/05) vs "मुलुकी देवानी (संहिता) ऐन २०७४ को अधीनमा" (SD-03/04).
- **Structural:** Second legal-basis form folds the statutory reference into a single "acting under Muluki Civil (Code) Act 2074" sentence rather than the two-Act reference.

**Related Data Needs:** (none — static)
**Related Business Rules:** BR-019 (BS format), BR-027/BR-028 (conditional content) — indirect
**Related Use Cases:** UC-011
**Related Functional Requirements:** FR-LR-024, FR-LR-028

**Open Questions:** OQ-CL-04 (which legal-basis form is current/authoritative)

**Validation Notes:**
- **Source-derived fact:** Two distinct legal-basis phrasings occur within the agricultural instances themselves (SD-01 vs SD-05). The statutory citations are quoted verbatim; this library does not verify their current legal status.
- **Domain interpretation:** The first form references two Acts (Muluki Civil Code 2074 + Muluki Procedure Code 2074, Contract Act Part 5); the second references only the Muluki Civil (Code) Act 2074. Difference requires domain/legal review.

---

### CLAUSE-AGR-003 — Land Description, Offer and Acceptance (Clause 1)

**Status:** Source-Derived · **Legal validation:** Not assessed (property identification is legally consequential; see OQ-CL-05) · **Domain validation:** Source-confirmed

**Category:** Property & Grant

**Applicability:** All land-rent agreements (all 5 agricultural instances; present as Clause 1 in each).

**Canonical Source Text** (SD-01; two-kitta form):

> म प्रथम पक्षको नाउँ मा दर्ता प्रमाणित भएका ल.पु.जि [PROP_DISTRICT] वडा नं [PROP_WARD], कित्ता न. [PROP_KITTA_NUM] क्षेत्रफल [PROP_AREA] क्षेत्रफल जग्गा द्रितिय पक्षले कृषि प्रयोजनको लागि आजको मितिले [TERM_DURATION] वर्ष सम्मको लागि जग्गा भाडामा दिनुहोस ⟨sic⟩ भनि प्रस्ताब राख्दा सो प्रस्ताब म प्रथम पक्ष सहर्षका साथ स्वीकार गरी जग्गा भाडामा दिन मंजुर गर्दछु ।

**Variables:**

| Variable | Description | Source Evidence | Data Need ID | Field ID | Required? | Notes |
|---|---|---|---|---|---|---|
| property.district | Land revenue district | "ल.पु.जि हरिसिद्धि" (SD-01) | DN-PROP-01 | PROP_DISTRICT | Yes | |
| property.ward | Ward number | "वडा नं ३ ख" (SD-01) | DN-PROP-02 | PROP_WARD | Yes | |
| property.kittaNumber[] | Kitta number(s) | "कित्ता न. ५५१ र ६२६" (SD-01) | DN-PROP-03 | PROP_KITTA_NUM | Yes | Repeatable; two kitta in SD-01/SD-07 |
| property.area.ropani | Area — Ropani | "०-०-३-१" (SD-01) | DN-PROP-04 | PROP_AREA | Yes | R-A-P-D; one value per kitta |
| property.area.anna | Area — Anna | "०-०-३-१" (SD-01) | DN-PROP-04 | PROP_AREA | Yes | |
| property.area.paisa | Area — Paisa | "०-०-३-१" (SD-01) | DN-PROP-04 | PROP_AREA | Yes | |
| property.area.dam | Area — Dam | "०-०-३-१" (SD-01) | DN-PROP-04 | PROP_AREA | Yes | |
| property.landCategory | Land category / registration type | "जोत जनी ज.ध. महल" / "श्री हरिसिद्धि भगवानी गुठि" (SD-08) | DN-PROP-05 | PROP_TYPE_LAND | Conditional | Guthi reference observed |
| property.usePurpose | Use purpose | "कृषि प्रयोजनको लागि" (SD-01) | DN-PROP-06 | PROP_USE_PURPOSE | Yes | Trigger for conditional clauses |
| term.durationYears | Term duration (years) | "५ वर्ष सम्मको लागि" (SD-01) | DN-RENT-08 | TERM_DURATION | Yes | 5 years in all agricultural instances |

**Conditions:**
- Property description clause is present in all instances regardless of use purpose.
- Multiple kitta numbers → repeat the property reference in the clause (BR-032). `Condition requires validation.` for trigger mechanism; two-kitta rendering is source-confirmed (SD-01/SD-07).
- Guthi registration reference appears only in SD-08 (`Condition requires validation.`, consistent with BR-033 `[TO BE VALIDATED]`).

**Variants:**
- **Structural:** single kitta (SD-02, SD-05, SD-08) vs two kitta (SD-01, SD-07).
- **Wording:** `दिनुहोस` vs `दिनुस` (SD-05 "दिनुहोस"); `जग्गा` vs `जग्गाहरु`; offer phrasing differs between the "म प्रथम पक्ष... स्वीकार गरी" form (SD-01) and the "द्वितीय पक्षले ... प्रस्ताव राख्दा ... प्रथम पक्ष जग्गा भाडामा दिन ... मन्जूर गर्दछ" form (SD-05).
- **Structural:** SD-05 folds the construction intent into the offer ("भौतिक संरचना तयार पारि ... दिनुहोस").
- **Structural (context):** SD-06 includes a partial-area grant ("०-११-३-० मध्ये ०-८-०-० क्षेत्रफल जग्गा") — not present in the agricultural set.

**Related Data Needs:** DN-PROP-01..06, DN-RENT-08, DN-OWN-01..02
**Related Business Rules:** BR-020 (R-A-P-D), BR-032 (multi-kitta), BR-033 (Guthi), BR-042 (use purpose ≠ Case Type)
**Related Use Cases:** UC-006, UC-007, UC-011
**Related Functional Requirements:** FR-LR-013, FR-LR-014, FR-LR-024, FR-LR-025

**Open Questions:** OQ-CL-05 (structured vs free-text area storage — mirrors OQ-DN-01), OQ-CL-06 (partial-area grant)

**Validation Notes:**
- **Source-derived fact:** All agricultural instances state "आजको मितिले [N] वर्ष सम्मको लागि" — term start is "from today's date" and term duration is 5 years in all 5 instances.
- **Domain interpretation:** The "आजको मितिले" (from today) phrasing implies no separate lease-start-date field in the template (consistent with Data Needs §7.1 "[UNRESOLVED] lease start date").

---

### CLAUSE-AGR-004 — Rent, Escalation and Payment (Clause 2)

**Status:** Needs Review · **Legal validation:** Requires legal review (financial formulas are `[TO BE VALIDATED]` in Template Analysis §7.2) · **Domain validation:** Domain validation required (BR-024..BR-026)

**Category:** Rent & Payment

**Applicability:** All land-rent agreements (all 5 agricultural instances; present as Clause 2).

**Canonical Source Text** (SD-02; monthly-rent form, cleanest rendering):

> प्रकरण नं. १ मा उल्लेखित जग्गा [RENT_PERIOD] रु [RENT_AMOUNT] /- (अक्षेरुपिय [RENT_AMOUNT_WORDS]), को दर रेटमा [RENT_ESCALATION_PERIOD] [RENT_ESCALATION_RATE]% को दरले चक्रवत ⟨sic⟩ भाडा दर वृद्धी ⟨sic⟩ गरी भाडामा लिन दिन दुवै पक्ष मन्जूर गर्दछ । [RENT_PAYMENT_TIMING]

**Alternative rendering (SD-01; annual-rent form with advance payment):**

> उक्त जग्गा भाडा लिन द्वितीय पक्षले वार्षिक रु ६५,०००/- (अक्षेरुपिय पैसाठी हजार रुपैया), को दर रेटमा २ वर्ष पछि १०% को दरले चक्रबध ⟨sic⟩ रुपमा भाडा दर वदृधी ⟨sic⟩ गरी प्रत्येक वर्ष अग्रिम भाडा डर ⟨sic⟩ बुझाउनु पर्नेमा दुवै पक्ष मन्जूर गर्दछ।

**Source Rendering Notes:** `चक्रवत`/`चक्रबध` are the source renderings of the intended "चक्रवृद्धि" (compound); `वृद्धी`/`वदृधी` of "वृद्धि"; `भाडा डर` (SD-01) is likely "भाडा दर" — all preserved verbatim, hypotheses only.

**Variables:**

| Variable | Description | Source Evidence | Data Need ID | Field ID | Required? | Notes |
|---|---|---|---|---|---|---|
| rent.period | Rent period (monthly/annual) | "वार्षिक" (SD-01), "मासिक" (SD-02) | DN-RENT-03 | RENT_PERIOD | Yes | monthly/annual |
| rent.amount | Rent amount (NPR, figures) | "रु ६५,०००/-" (SD-01) | DN-RENT-01 | RENT_AMOUNT | Yes | High sensitivity |
| rent.amountWords | Rent amount (Nepali words) | "(अक्षेरुपिय पैसाठी हजार रुपैया)" (SD-01) | DN-RENT-02 | RENT_AMOUNT_WORDS | Yes | CALCULATED; must agree with figures (BR-023) |
| rent.escalation.period | Escalation period | "२ वर्ष पछि" (SD-01), "प्रत्येक वर्षमा" (SD-02) | DN-RENT-05 | RENT_ESCALATION_PERIOD | Yes | three observed forms |
| rent.escalation.rate | Escalation rate (%) | "१०%" (SD-01), "५%" (SD-07) | DN-RENT-04 | RENT_ESCALATION_RATE | Yes | 5% or 10% observed |
| rent.escalation.method | Escalation method | "चक्रबध/चक्रवत" (compound) | DN-RENT-07 | RENT_ESCALATION_METHOD | Optional | compound observed; simple `[TO BE VALIDATED]` |
| rent.paymentTiming | Payment timing | "प्रत्येक वर्ष अग्रिम" (SD-01) | DN-RENT-06 | RENT_PAYMENT_TIMING | Yes | "अग्रिम" (advance) observed |

**Conditions:**
- Rent-period selection drives the clause rendering: monthly rent instance (SD-02) vs annual rent instance (SD-01/05/07/08). BR-029.
- Payment-timing wording present in SD-01/05/07/08; SD-02 lacks the explicit advance-timing sentence (`Condition requires validation.`).

**Variants:**
- **Parameter:** rent amount ₹65,000 (SD-01/08), ₹20,000 monthly (SD-02), ₹35,000 (SD-05), ₹10,000 (SD-07); escalation rate 10% (SD-01/02/05/08), 5% (SD-07); escalation period "after 2 years" (SD-01/08), "every year" (SD-02/05/07).
- **Wording:** `चक्रवृद्धि` vs `चक्रवत` vs `चक्रबध`; `वृद्धी` vs `वदृधी`; "भाडा डर" (SD-01) vs "भाडा दर" (SD-02).
- **Structural:** SD-02's clause lacks the advance-payment sentence; SD-01/05/07/08 include "प्रत्येक वर्ष अग्रिम भाडा" phrasing.
- **Parameter (context, not agricultural):** SD-03/SD-04 state escalation "प्रत्येक २/२ वर्षमा १० प्रतिशत" (business instances; SD-04 duplicates clause 2 with an inconsistent second rendering "प्रत्येक २/२ वर्षमा २ प्रतिशत" / "२ %" — internal inconsistency within one instance, flagged at OQ-CL-08).

**Related Data Needs:** DN-RENT-01..07, DN-PAY-01
**Related Business Rules:** BR-021, BR-022, BR-023, BR-024, BR-025, BR-026, BR-029
**Related Use Cases:** UC-007, UC-011
**Related Functional Requirements:** FR-LR-014, FR-LR-015, FR-LR-027

**Open Questions:** OQ-CL-07 (escalation formulas — mirrors OQ-TA-23/OQ-BR-03), OQ-CL-08 (SD-04 duplicate-clause-2 inconsistency)

**Validation Notes:**
- **Source-derived fact:** All 5 agricultural instances include an escalation term; none is a flat fixed-price agreement. "Compound" escalation is asserted by the source wording in all instances.
- **Domain interpretation:** BR-024..BR-026 formulas (annual = monthly×12; increase = current×rate; compound) are `[TO BE VALIDATED]`; the library does not compute or endorse any formula.
- **Legal interpretation:** None offered. The figures-vs-words hierarchy (words override figures) is a common legal convention (BR-023 `[TO BE VALIDATED]`) — requires legal review.

---

### CLAUSE-AGR-005 — Physical Structure Construction (permission)

**Status:** Source-Derived · **Legal validation:** Not assessed · **Domain validation:** Domain validation required (structure handover interplay — see OQ-CL-09)

**Category:** Party Obligations

**Applicability:** Present in 4/5 agricultural instances (SD-01, SD-02, SD-07, SD-08; absent in SD-05). Common in business context (SD-03/04/06).

**Canonical Source Text** (SD-01):

> उक्त जग्गा कृषि प्रयोजनको लागी प्रथम पक्षको सहमतीमा भौतिक संरचना निर्माण गर्न सक्ने छ भनि द्रितिय पक्षको प्रस्ताप ⟨sic⟩ प्रथम पक्ष स्वीकार गर्दछ ।

**Source Rendering Notes:** `प्रस्ताप` is the source spelling (intended "प्रस्ताव"); preserved.

**Variables:**

| Variable | Description | Source Evidence | Data Need ID | Field ID | Required? | Notes |
|---|---|---|---|---|---|---|
| property.usePurpose | Use purpose (trigger) | "कृषि प्रयोजनको लागी" (SD-01) | DN-PROP-06 | PROP_USE_PURPOSE | Yes | Present in agricultural + business instances |

**Conditions:**
- Clause present when the agreement contemplates construction; observed in 4/5 agricultural instances. `Condition requires validation.` for the exact trigger (use purpose vs agreement intent).
- Absence from SD-05 is source-confirmed; SD-05 instead has the structure-handover clause (CLAUSE-AGR-014).

**Variants:**
- **Wording:** `जग्गा` (SD-01) vs `जग्गाहरुमा` (SD-07/08); `कृषि` vs `कृषी`; `लागी` vs `लागि`.
- **Structural (context):** SD-03/04/06 carry the construction-permission concept within business clauses; SD-06 additionally implies structures during term.

**Related Data Needs:** DN-PROP-06
**Related Business Rules:** BR-028 (business/residence construction clauses)
**Related Use Cases:** UC-011
**Related Functional Requirements:** FR-LR-025, FR-LR-026

**Open Questions:** OQ-CL-09 (construction ↔ structure-handover clause interplay)

**Validation Notes:**
- **Source-derived fact:** The permission is always conditional on First Party consent ("प्रथम पक्षको सहमतीमा").
- **Domain interpretation:** Construction permission and end-of-term structure handover (CLAUSE-AGR-014) are logically related but appear independently across instances; the pair requires domain validation.

---

### CLAUSE-AGR-006 — Prohibited Crops / Restricted Use

**Status:** Source-Derived · **Legal validation:** Not assessed · **Domain validation:** Source-confirmed (two source forms)

**Category:** Land Use & Cultivation

**Applicability:** Present in all 5 agricultural instances in one of two forms.

**Canonical Source Text** (SD-01; prohibited-crops form — agricultural instances SD-01/02/07/08):

> उक्त बहालमा लिएको जग्गा भित्र नेपाल सरकारबाट निषेधित गरेको कृषी उत्पादन गर्न पाउने छैन, गरी गराएमा त्यसको सम्पूर्ण जिम्मेवारी द्रितिय पक्षकै हुने छ ।

**Second Source Form** (SD-05; prohibited-acts→void form):

> बहालमा लिएको जग्गा उपभोग गर्ने क्रममा द्वितीय पक्षले ऐनले निषेध गरेको कार्य गर्न/गराउन पाउनेछैन। सो किसिमको कार्य गरी/गराएमा यो करारनामा स्वतः बदर हुनेछ।

**Variables:** None (clause-level restriction).

**Conditions:**
- Prohibited-crops form (crop-specific) observed in agricultural instances SD-01/02/07/08; prohibited-acts→void form in SD-05. `Condition requires validation.` for which form applies when (OQ-CL-11).

**Variants:**
- **Wording:** `गरेको` vs `गरेको`/`गरी गराएमा`; `छैन, गरी गराएमा` (SD-01) vs `पाउनेछैन।` (SD-05).
- **Structural:** SD-05 adds an express consequence (contract becomes void); SD-01/02/07/08 assign responsibility to the Second Party without the void consequence.
- **Structural:** In SD-01/02/07/08 the subletting prohibition is appended to this clause (see CLAUSE-AGR-007); in SD-05 it is appended to the notice clause.

**Related Data Needs:** DN-PROP-06 (trigger)
**Related Business Rules:** BR-027
**Related Use Cases:** UC-011
**Related Functional Requirements:** FR-LR-025

**Open Questions:** OQ-CL-11 (prohibited-crops vs prohibited-acts form selection)

**Validation Notes:**
- **Source-derived fact:** The agriculture-specific restriction exists in all 5 agricultural instances but with materially different consequences (responsibility-assignment vs voidability). The `[TO BE VALIDATED]` status of the conditional-clause model (BR-027, FR-LR-025) is consistent with this observed variation.

---

### CLAUSE-AGR-007 — Prohibition on Subletting

**Status:** Source-Derived · **Legal validation:** Not assessed · **Domain validation:** Source-confirmed (BR-035 `[TO BE VALIDATED]`)

**Category:** Subletting & Third Parties

**Applicability:** All land-rent agreements (all 5 agricultural instances; also in business context).

**Canonical Source Text** (SD-01):

> सो जग्गाहरु द्रितिय पक्षले अन्य कुनै पनि पक्षलाइ कुनै पनि बहाना बनाई तेस्रो वा अन्य पक्षलाइ पुन बहालमा दिन पाउने छैन।

**SD-05 form (appended to notice clause):**

> साथै प्रथम पक्षको सहमति बिना अन्य पक्षलाइ द्वितीय पक्षले पून बहालमा लगाउन पाउने छैन।

**Variables:** None (static standard clause).

**Conditions:** Present in all instances; clause position varies (with restricted-use clause in SD-01/02/07/08; with notice clause in SD-05). `Condition requires validation.` for position selection.

**Variants:**
- **Structural:** Position/attachment differs per instance; SD-05 requires First Party consent for re-letting (permissive-with-consent wording) vs SD-01's absolute prohibition.
- **Wording:** `पुन बहालमा दिन` vs `पून बहालमा लगाउन`; `छैन` vs `पाउनेछैन`.

**Related Data Needs:** (none — clause-level)
**Related Business Rules:** BR-035
**Related Use Cases:** UC-011
**Related Functional Requirements:** FR-LR-024, FR-LR-025

**Open Questions:** (none new)

**Validation Notes:**
- **Source-derived fact:** Subletting prohibition appears in every agricultural instance — a universal standard clause.

---

### CLAUSE-AGR-008 — Tax and Expense Responsibilities

**Status:** Source-Derived · **Legal validation:** Not assessed · **Domain validation:** Domain validation required (expense scope — OQ-CL-12)

**Category:** Party Obligations

**Applicability:** All land-rent agreements (all 5 agricultural instances; scope varies).

**Canonical Source Text** (SD-01; rent-tax-only form):

> उक्त कृषी ब्यवोसाय गर्ने क्रममा नेपाल सरकारलाई बुझाउनु पर्ने सम्पूर्ण कर (बहालकरसमेत), द्रितिय पक्ष स्वयमले सम्बन्धित निकाएमा ⟨sic⟩ बुझाउनु पर्ने छ।

**Expanded form (SD-05; utilities + rent tax + construction tax + waste):**

> बहालमा दिएको जग्गामा भौतिक संरचनाको उपभोग गर्दा लाग्ने विधुत महशुल, पानीको महशुल र नेपाल सरकारलाई तिर्नुपर्ने बहालकर र भौतिक संरचना निर्माण गर्दा लाग्ने सम्पूर्ण कर द्वितीय पक्षले व्यहोर्नुपर्नेछ। साथै उक्त व्यवसायबाट हुन जाने फोहोरको व्यवस्थापन द्वितीय पक्ष स्वयमले गर्नुपर्नेछ।

**Source Rendering Notes:** `निकाएमा` (SD-01) likely intended "निकायमा" (to the concerned office); preserved verbatim, hypothesis only.

**Variables:** None (clause-level obligations; expenses enumerated in source text).

**Conditions:**
- Rent tax (बहालकर) appears in all instances. Expanded scope (electricity/water/construction-tax/waste) appears in SD-05 only (agricultural set); in SD-03/04/06 (business context) the expanded scope also appears. `Condition requires validation.` for scope selection (OQ-CL-12).

**Variants:**
- **Structural:** rent-tax-only scope (SD-01/02/07/08) vs expanded utilities+tax+waste scope (SD-05).
- **Wording:** `बुझाउनु पर्ने` vs `व्यहोर्नुपर्नेछ`; `बहालकर` vs `बहाल कर`.

**Related Data Needs:** DN-PAY-02
**Related Business Rules:** BR-036
**Related Use Cases:** UC-007, UC-011
**Related Functional Requirements:** FR-LR-024

**Open Questions:** OQ-CL-12 (expense-scope selection)

**Validation Notes:**
- **Source-derived fact:** Rent tax is always assigned to the Second Party. No instance assigns rent tax to the First Party.

---

### CLAUSE-AGR-009 — Uninterrupted Use (First Party obligation)

**Status:** Source-Derived · **Legal validation:** Not assessed · **Domain validation:** Source-confirmed

**Category:** Party Obligations

**Applicability:** Present in 3/5 agricultural instances (SD-01, SD-07, SD-08; absent in SD-02 and SD-05).

**Canonical Source Text** (SD-01):

> प्रथम पक्षले द्वितीय पक्षलाई यस करारनामा उल्लेखित जग्गा करार अवधि भर निर्वाध रूपमा प्रयोग गर्न दिनुपर्नेछ।

**Variables:** None (static obligation).

**Conditions:** Present in SD-01/07/08, absent in SD-02/SD-05. `Condition requires validation.` for presence/absence driver.

**Variants:**
- **Wording:** `प्रथम पक्षले द्वितीय पक्षलाई` (SD-01) vs `द्वितीय पक्षले प्रथम पक्षलाई` (SD-03/04 — reversed roles, business context; not present in SD-02/SD-05).

**Related Data Needs:** (none — clause-level)
**Related Business Rules:** (none direct)
**Related Use Cases:** UC-011
**Related Functional Requirements:** FR-LR-024

**Open Questions:** OQ-CL-13 (presence/absence of uninterrupted-use clause)

**Validation Notes:**
- **Source-derived fact:** Not universal across agricultural instances; absence in SD-02/SD-05 is source-confirmed.

---

### CLAUSE-AGR-010 — Notice and Termination

**Status:** Source-Derived · **Legal validation:** Not assessed · **Domain validation:** Domain validation required (notice unit model — OQ-CL-14; mirrors AR-013)

**Category:** Termination & Notice

**Applicability:** All land-rent agreements (all 5 agricultural instances).

**Canonical Source Text** (SD-01; uniform 60-day form):

> बहालमा लिएको जग्गाबाट हटाउन वा छोडन चाहे मा एकले अर्कालाई [TERM_NOTICE_PERIOD] अग्रिम सूचना दिनु पर्नेछ।

**SD-05 form (asymmetric, per-party):**

> सो कित्ता जग्गा प्रथम पक्ष स्वोयमलाइ आवश्यक परेको खण्डमा अग्रिम तिन महिना अगाडी सूचना प्रधान गरि जग्गा खाली गराउन सक्नेछ र द्वितीय पक्षले जग्गा छोदि जानपर्ने अवस्था आएमा पनि अग्रिम ६ महिना सूचना प्रथान गरि मात्र जग्गा छोड्न सक्नेछ।

**Variables:**

| Variable | Description | Source Evidence | Data Need ID | Field ID | Required? | Notes |
|---|---|---|---|---|---|---|
| term.noticePeriod | Notice period for termination | "६० दिन" (SD-01/02/07/08); "तिन महिना" / "६ महिना" (SD-05) | DN-RENT-09 | NOTICE_PERIOD | Yes | Per-party asymmetric possible (SD-05); units days vs months |

**Conditions:**
- Uniform notice (60 days) in SD-01/02/07/08; asymmetric per-party notice (P1: 3 months; P2: 6 months) in SD-05. `Condition requires validation.` for asymmetric applicability (mirrors AR-013).

**Variants:**
- **Parameter:** 60 days (SD-01/02/07/08) vs 3 months/6 months per party (SD-05).
- **Structural:** SD-05 gives separate termination rights per party with a consent-conditional subletting rider; SD-01/02/07/08 give a single mutual 60-day notice.

**Related Data Needs:** DN-RENT-09
**Related Business Rules:** (BR-024..BR-026 not applicable) — see AR-013
**Related Use Cases:** UC-007, UC-011
**Related Functional Requirements:** FR-LR-014, FR-LR-024

**Open Questions:** OQ-CL-14 (notice unit model — days vs months, per-party)

**Validation Notes:**
- **Source-derived fact:** Notice is always "अग्रिम" (advance). Unit inconsistency (days vs months) is source-confirmed and mirrors AR-013.

---

### CLAUSE-AGR-011 — Amendment by Mutual Consent

**Status:** Source-Derived · **Legal validation:** Not assessed · **Domain validation:** Source-confirmed

**Category:** General Provisions

**Applicability:** Present in 4/5 agricultural instances (SD-01, SD-02, SD-07, SD-08; absent in SD-05).

**Canonical Source Text** (SD-01):

> यो सम्झौतामा उल्लेखित शर्तहरुमा कुनै थप घट गर्नु परे मा दुवै पक्षको आपसी समझदारीमा थप घट गर्न सकिने छ।

**Variables:** None (static).

**Conditions:** Present in SD-01/02/07/08, absent in SD-05. `Condition requires validation.` for presence driver.

**Variants:** **Wording:** `थप घट` (SD-01) vs `थप घट` (SD-05-absent); `सकिने छ` vs `सक्ने छ` (SD-03/04 context).

**Related Data Needs:** (none — clause-level)
**Related Business Rules:** (none direct)
**Related Use Cases:** UC-011
**Related Functional Requirements:** FR-LR-024

**Open Questions:** (none new)

---

### CLAUSE-AGR-012 — Governing Law (residual)

**Status:** Source-Derived · **Legal validation:** Requires legal review · **Domain validation:** Source-confirmed

**Category:** General Provisions

**Applicability:** Present in 4/5 agricultural instances (SD-01, SD-02, SD-07, SD-08; absent in SD-05).

**Canonical Source Text** (SD-01):

> यसमा लेखिएको बाहेक अन्यका हकमा प्रचलित कानून बमोजिम हुनेछ।

**Variables:** None (static).

**Conditions:** Present in SD-01/02/07/08, absent in SD-05. `Condition requires validation.` for presence driver.

**Variants:** **Wording:** `काननू` (SD-01) vs `कानून` (SD-02) — extraction variants of "कानून"; preserved.

**Related Data Needs:** (none — clause-level)
**Related Business Rules:** (none direct)
**Related Use Cases:** UC-011
**Related Functional Requirements:** FR-LR-024

**Open Questions:** OQ-CL-04 (legal-basis/reference form — see CLAUSE-AGR-002)

**Validation Notes:**
- **Source-derived fact:** The residual governing-law clause references "प्रचलित कानून" (prevailing law) without naming it; it does not assert which law.

---

### CLAUSE-AGR-013 — Agricultural Restoration on Exit

**Status:** Source-Derived · **Legal validation:** Not assessed · **Domain validation:** Source-confirmed (agriculture-specific)

**Category:** Land Use & Cultivation

**Applicability:** Present in 4/5 agricultural instances (SD-01, SD-02, SD-07, SD-08; absent in SD-05). Agriculture-specific.

**Canonical Source Text** (SD-01):

> सो सम्झौतामा उल्लेखित कृषि प्रयोजनको लागि बहाल लिएका जग्गाहरु समय अवधि समाप्त भएपछि वा छाडी/छोडी जानुपर्ने अवस्थामा उक्त जग्गालाई कृषि योग्य बनाइ छोड्नु पर्नेछ।

**Variables:** None (static agriculture obligation).

**Conditions:** Agriculture-specific; present in the 4 full agricultural instances, absent in SD-05 (which instead carries structure handover). `Condition requires validation.` for the exact trigger (mirrors BR-027).

**Variants:** **Wording:** `छाडी/छोडी जानुपर्ने` vs `छाडी/छोडी जानुपर्ने अवस्थामा`; `कृषि योग्य बनाइ छोड्नु` consistent across instances.

**Related Data Needs:** DN-PROP-06 (trigger)
**Related Business Rules:** BR-027
**Related Use Cases:** UC-011
**Related Functional Requirements:** FR-LR-025

**Open Questions:** OQ-CL-11 (form selection; absent in SD-05)

**Validation Notes:**
- **Source-derived fact:** Restoration-to-cultivable-condition obligation is the agriculture-specific exit term and is absent when the agreement is structured around structure handover (SD-05).

---

### CLAUSE-AGR-014 — Structure Handover After Term

**Status:** Source-Derived · **Legal validation:** Not assessed · **Domain validation:** Domain validation required (rare in agricultural set — OQ-CL-09)

**Category:** Party Obligations

**Applicability:** Present in 1/5 agricultural instances (SD-05); common in business context (SD-03/04/06).

**Canonical Source Text** (SD-05):

> करार अवधी समाप्त भएपछि उक्त जग्गामा निर्माण भएको भौतिक संरचना भत्काई सफा सुघर गरि जग्गाको संरचना सहमति अनुसार राखी छोड्ने कुरामा दुवै पक्ष मन्जूर गर्दछ।

**Variables:** None (static obligation).

**Conditions:** Present where construction occurred during the term; in the agricultural set observed only in SD-05. `Condition requires validation.`

**Variants:** **Wording:** `सुघर` (SD-05) vs `सुग्घर` (SD-03/04 context); `गरि` vs `गरी`.

**Related Data Needs:** (none — clause-level)
**Related Business Rules:** BR-028 (business/residence clauses)
**Related Use Cases:** UC-011
**Related Functional Requirements:** FR-LR-025

**Open Questions:** OQ-CL-09 (construction ↔ handover interplay)

**Validation Notes:**
- **Source-derived fact:** In the agricultural set, structure handover appears only in SD-05, where the agricultural-restoration clause is absent — suggesting an either/or structure between the two exit clauses that requires domain validation.

---

### CLAUSE-AGR-015 — Compliance and Breach Remedy

**Status:** Source-Derived · **Legal validation:** Requires legal review (enforcement remedy) · **Domain validation:** Domain validation required

**Category:** General Provisions

**Applicability:** Present in 1/5 agricultural instances (SD-05).

**Canonical Source Text** (SD-05):

> यसमा उल्लेखित गरेको शर्तहरु दुवै पक्षले पूर्ण रुपमा परिपालन गर्ने कुरामा दुवै पक्ष मन्जूर गर्दछ । कुनै पक्षले करार उल्लङ्घन गरे मा पिडित पक्षले सम्बन्धित कार्यालयमा गई शर्तहरु पालन गराउन सक्ने छ।

**Variables:** None (static obligation + remedy).

**Conditions:** Present in SD-05 only (agricultural set); also in business context (SD-03/04/06). `Condition requires validation.` for presence driver.

**Variants:** **Wording:** `गरेको शर्तहरु` vs `गरेको शर्तहरु`; `उल्लङ्घन` vs `उल्लङ्घन` — consistent across instances; `सक्ने छ` vs `सक्नेछ` minor.

**Related Data Needs:** (none — clause-level)
**Related Business Rules:** (none direct)
**Related Use Cases:** UC-011
**Related Functional Requirements:** FR-LR-024

**Open Questions:** OQ-CL-15 (breach-remedy clause has no C### counterpart — see §11)

**Validation Notes:**
- **Source-derived fact:** The remedy is limited to seeking enforcement "at the relevant office" (सम्बन्धित कार्यालय); it is not a liquidated-damages or penalty provision.
- **Potential Data Needs gap:** This clause does not correspond to any C01–C13 inventory entry in `Data Needs.md` §6.1. See §11.

---

## 6. Document Framework Elements (Non-Clause)

The following sections carry variables but are not clause provisions. They are catalogued for completeness of variable traceability (corresponding to S04–S08 of the Template Analysis).

| Element | Section | Variables | Data Need IDs | Sources |
|---|---|---|---|---|
| First Party Signature | S04 | party.first.signatureName | DN-P1-11 (P1_SIGNATURE_NAME) | All |
| Second Party Signature | S05 | party.second.signatureName | DN-P2-11 (P2_SIGNATURE_NAME) | All (blank in SD-08) |
| Witnesses | S06 | witness[1..3].name / .address / .age | DN-WIT-01..09 | 1–3 witnesses per instance |
| Writer | S07 | writer.name, writer.licenseNumber | DN-WRI-01; DN-WRI-02 ([UNRESOLVED] OQ-DN-03) | Most instances |
| Date | S08 | date.year, date.month, date.day, date.weekday | DN-DOC-01..04 | All |

**Notes:**
- Witness entries vary in count (1–3) and in detail (some omit address/age, e.g., SD-03 lists names only). BR-034 repeatable; minimum one witness per party per BR-008 (updated 2026-08-13 by project owner: name, age, address; citizenship optional; legal confirmation still pending).
- Writer may be a party ("लेखक प्रथम पक्ष सुनिल महर्जन आफै" SD-01), a relative of a party, or a professional with license number ("लेखक सत्य महर्जन प्र.प.नं. ३४६" SD-06). Writer license number has no Field Dictionary entry — **Potential Data Needs gap** consistent with OQ-DN-03.
- Date is always Bikram Sambat, format `इतिसम्बत [date.year] [date.month] महिना [date.day] गते रोज [date.weekday] शुभम्` (BR-019).

---

## 7. Source → Clause Matrix

Legend: **U** = Universal (all 5 agricultural instances) · **C** = Common (4/5) · **R** = Rare (2–3/5) · **UQ** = Unique (1/5) · **Cond** = Conditionally present.

| Clause | SD-01 | SD-02 | SD-05 | SD-07 | SD-08 | Classification |
|---|---|---|---|---|---|---|
| CLAUSE-AGR-001 (Party ID) | ✓ | ✓ | ✓ | ✓ | ✓ | U |
| CLAUSE-AGR-002 (Legal basis) | ✓ | ✓ | ✓ | ✓ | ✓ | U |
| CLAUSE-AGR-003 (Land description) | ✓ | ✓ | ✓ | ✓ | ✓ | U |
| CLAUSE-AGR-004 (Rent/escalation) | ✓ | ✓ | ✓ | ✓ | ✓ | U |
| CLAUSE-AGR-005 (Construction) | ✓ | ✓ | — | ✓ | ✓ | C |
| CLAUSE-AGR-006 (Restricted use) | ✓ | ✓ | ✓ | ✓ | ✓ | U (two forms) |
| CLAUSE-AGR-007 (Subletting) | ✓ | ✓ | ✓ | ✓ | ✓ | U |
| CLAUSE-AGR-008 (Tax/expenses) | ✓ | ✓ | ✓ | ✓ | ✓ | U (scope variant) |
| CLAUSE-AGR-009 (Uninterrupted use) | ✓ | — | — | ✓ | ✓ | R (3/5) |
| CLAUSE-AGR-010 (Notice) | ✓ | ✓ | ✓ | ✓ | ✓ | U (unit/parameter variant) |
| CLAUSE-AGR-011 (Amendment) | ✓ | ✓ | — | ✓ | ✓ | C |
| CLAUSE-AGR-012 (Governing law) | ✓ | ✓ | — | ✓ | ✓ | C |
| CLAUSE-AGR-013 (Agri restoration) | ✓ | ✓ | — | ✓ | ✓ | C |
| CLAUSE-AGR-014 (Structure handover) | — | — | ✓ | — | — | UQ |
| CLAUSE-AGR-015 (Breach remedy) | — | — | ✓ | — | — | UQ |

**Finding:** No single agricultural instance contains all 15 clauses. SD-01/SD-07/SD-08 are the fullest (each 9 numbered provisions); SD-05 deviates most (exit structured as structure-handover + breach-remedy instead of restoration + amendment + governing law).

---

## 8. Clause → Data Traceability Matrix

Entity abbreviations: **P1** = First Party, **P2** = Second Party, **PROP** = Property, **TERM** = Term, **WIT** = Witness, **WRI** = Writer, **DOC** = Document.

| Clause | Variable | Data Need | Field | Entity | Acquisition Method | Verification |
|---|---|---|---|---|---|---|
| CLAUSE-AGR-001 | party.first.grandfather | DN-P1-02 | P1_GRANDFATHER | P1 | Manual Entry | Required |
| CLAUSE-AGR-001 | party.first.father | DN-P1-03 | P1_FATHER | P1 | Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.first.name | DN-P1-01 | P1_FULL_NAME | P1 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.first.address.district | DN-P1-04 | P1_DISTRICT | P1 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.first.address.municipality | DN-P1-05 | P1_MUNICIPALITY | P1 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.first.address.ward | DN-P1-06 | P1_WARD | P1 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.first.age | DN-P1-07 | P1_AGE | P1 | Manual Entry | Required when present |
| CLAUSE-AGR-001 | party.first.citizenship.number | DN-P1-08 | P1_CITIZENSHIP_NUM | P1 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.first.citizenship.issueDate | DN-P1-09 | P1_CITIZENSHIP_DATE | P1 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.first.citizenship.issueDistrict | DN-P1-10 | P1_CITIZENSHIP_DIST | P1 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.second.grandfather | DN-P2-02 | P2_GRANDFATHER | P2 | Manual Entry | Required |
| CLAUSE-AGR-001 | party.second.father | DN-P2-03 | P2_FATHER | P2 | Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.second.name | DN-P2-01 | P2_FULL_NAME | P2 | Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.second.address.district | DN-P2-04 | P2_DISTRICT | P2 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.second.address.municipality | DN-P2-05 | P2_MUNICIPALITY | P2 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.second.address.ward | DN-P2-06 | P2_WARD | P2 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.second.age | DN-P2-07 | P2_AGE | P2 | Manual Entry | Required when present |
| CLAUSE-AGR-001 | party.second.citizenship.number | DN-P2-08 | P2_CITIZENSHIP_NUM | P2 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.second.citizenship.issueDate | DN-P2-09 | P2_CITIZENSHIP_DATE | P2 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.second.citizenship.issueDistrict | DN-P2-10 | P2_CITIZENSHIP_DIST | P2 | OCR / Manual Entry / Existing Client Data | Required |
| CLAUSE-AGR-001 | party.second.company.name | DN-P2-12 | P2_COMPANY_NAME | P2 | OCR / Manual Entry | Required (when company) |
| CLAUSE-AGR-001 | party.second.company.registrationNo | DN-P2-13 | P2_COMPANY_REG | P2 | OCR / Manual Entry | Required (when company) |
| CLAUSE-AGR-001 | party.second.company.registrationDate | DN-P2-14 | P2_COMPANY_REG_DATE | P2 | OCR / Manual Entry | Required (when company) |
| CLAUSE-AGR-001 | party.second.company.registrarOffice | DN-P2-15 | P2_COMPANY_REG_OFFICE | P2 | OCR / Manual Entry | Required (when company) |
| CLAUSE-AGR-001 | party.second.company.proprietor | DN-P2-16 | P2_COMPANY_PROPRIETOR | P2 | OCR / Manual Entry | Required (when company) |
| CLAUSE-AGR-003 | property.district | DN-PROP-01 | PROP_DISTRICT | PROP | OCR / Manual Entry | Required |
| CLAUSE-AGR-003 | property.ward | DN-PROP-02 | PROP_WARD | PROP | OCR / Manual Entry | Required |
| CLAUSE-AGR-003 | property.kittaNumber[] | DN-PROP-03 | PROP_KITTA_NUM | PROP | OCR / Manual Entry | Required (high sensitivity) |
| CLAUSE-AGR-003 | property.area.ropani/anna/paisa/dam | DN-PROP-04 | PROP_AREA | PROP | OCR / Manual Entry | Required (high sensitivity) |
| CLAUSE-AGR-003 | property.landCategory | DN-PROP-05 | PROP_TYPE_LAND | PROP | OCR / Manual Entry | Required (when present) |
| CLAUSE-AGR-003 | property.usePurpose | DN-PROP-06 | PROP_USE_PURPOSE | PROP | Manual Entry | Not required |
| CLAUSE-AGR-003 | term.durationYears | DN-RENT-08 | TERM_DURATION | TERM | Manual Entry | Required |
| CLAUSE-AGR-004 | rent.period | DN-RENT-03 | RENT_PERIOD | TERM | Manual Entry | Required |
| CLAUSE-AGR-004 | rent.amount | DN-RENT-01 | RENT_AMOUNT | TERM | Manual Entry | Required (high sensitivity) |
| CLAUSE-AGR-004 | rent.amountWords | DN-RENT-02 | RENT_AMOUNT_WORDS | TERM | Derived/Calculated | Required |
| CLAUSE-AGR-004 | rent.escalation.period | DN-RENT-05 | RENT_ESCALATION_PERIOD | TERM | Manual Entry | Required |
| CLAUSE-AGR-004 | rent.escalation.rate | DN-RENT-04 | RENT_ESCALATION_RATE | TERM | Manual Entry | Required |
| CLAUSE-AGR-004 | rent.escalation.method | DN-RENT-07 | RENT_ESCALATION_METHOD | TERM | Manual Entry | Required (when escalation) |
| CLAUSE-AGR-004 | rent.paymentTiming | DN-RENT-06 | RENT_PAYMENT_TIMING | TERM | Manual Entry | Required |
| CLAUSE-AGR-005 | property.usePurpose (trigger) | DN-PROP-06 | PROP_USE_PURPOSE | PROP | Manual Entry | Not required |
| CLAUSE-AGR-006 | — (clause-level) | — | — | PROP | — | — |
| CLAUSE-AGR-007 | — (clause-level) | — | — | PROP | — | — |
| CLAUSE-AGR-008 | — (clause-level) | DN-PAY-02 (expense assignment) | — | P2 | — | — |
| CLAUSE-AGR-009 | — (clause-level) | — | — | P1 | — | — |
| CLAUSE-AGR-010 | term.noticePeriod | DN-RENT-09 | NOTICE_PERIOD | TERM | Manual Entry | Required |
| CLAUSE-AGR-011..015 | — (clause-level) | — | — | — | — | — |
| Framework | party.first.signatureName | DN-P1-11 | P1_SIGNATURE_NAME | P1 | Derived/Calculated | Not required |
| Framework | party.second.signatureName | DN-P2-11 | P2_SIGNATURE_NAME | P2 | Derived/Calculated | Not required |
| Framework | witness[1..3].name/.address/.age | DN-WIT-01..09 | WITNESS_N_* | WIT | Manual Entry | Required |
| Framework | writer.name | DN-WRI-01 | WRITER_NAME | WRI | Manual Entry | Not required |
| Framework | writer.licenseNumber | **no DN** | **no Field** | WRI | Manual Entry | Not required |
| Framework | date.year/.month/.day/.weekday | DN-DOC-01..04 | DATE_YEAR/MONTH/DAY/WEEKDAY | DOC | Derived/Calculated | Not required |

---

## 9. Coverage Findings

1. **15 clauses catalogued** from the 5 agricultural instances (CLAUSE-AGR-001..015), plus 5 document framework element groups.
2. **Universal clauses (all 5 instances):** party identification (001), legal basis (002), land description/grant (003), rent/escalation/payment (004), restricted use (006), subletting prohibition (007), tax/expense (008), notice/termination (010) — 8 universal.
3. **Common clauses (4/5):** construction permission (005), amendment (011), governing law (012), agricultural restoration (013).
4. **Rare (3/5):** uninterrupted use (009).
5. **Unique (1/5):** structure handover (014), breach remedy (015) — both in SD-05.
6. **The 5 agricultural instances are not uniform:** SD-05 deviates most; SD-01/07/08 form one near-identical family; SD-02 is a monthly-rent company-tenant variant.
7. **All 5 agricultural instances use a 5-year term; all have an escalation term; none is flat-rent.**
8. **Use-purpose conditional content confirmed in-source:** agricultural-restoration (013) and prohibited-crops form (006) appear in agricultural instances and are absent in business context instances; structure-oriented clauses (014) and prohibited-acts form (006) appear where structure/business content dominates.
9. **All financial/calculation content is `[TO BE VALIDATED]` (BR-024..BR-026).**
10. **Applicability beyond the supplied file is `Not established from supplied sources.`** — only one reference file was supplied.

---

## 10. Requirements / Data Gaps Discovered

1. **Potential Data Needs gap: breach-and-remedy clause (CLAUSE-AGR-015)** — present in SD-05 and business context instances, but `Data Needs.md` §6.1 inventory (C01–C13) has no entry for it. C13 (renewal) is the only "one instance" entry and refers to the business context (SD-06). A clause-inventory entry for compliance/breach remedy may be required. (OQ-CL-15)
2. **Potential Data Needs gap: writer professional license number** — observed in SD-06 ("प्र.प.नं. ३४६"); has no Field Dictionary field or Data Need. Consistent with existing `[UNRESOLVED]` OQ-DN-03. Not resolved here.
3. **Potential Data Needs gap: property land category (Guthi/ज.ध. महल) rendering** — DN-PROP-05 exists but is `PROPOSED`; the Guthi reference (SD-08) is a property-description rendering whose storage/rendering is `[TO BE VALIDATED]` (BR-033).
4. **Potential Data Needs gap: lease-start date** — implied by "आजको मितिले" (from today's date); no field. Consistent with `[UNRESOLVED]` in Data Needs §7.1. Not resolved here.
5. **Potential Data Needs gap: deposit amount** — SRS §9.5 lists a deposit; no template instance contains a deposit clause. The template does not support a deposit clause in the supplied set. (Consistent with OQ-DN-13.)
6. **Potential FR gap: conditional clause-selection driver** — the template offers multiple forms (two legal-basis forms; two restricted-use forms; uniform vs asymmetric notice; restoration vs structure-handover exit). Existing FR-LR-025/BR-027..BR-033 assume simpler one-to-one condition→clause mappings; the observed form-selection behavior is not covered. (OQ-CL-11, OQ-CL-12, OQ-CL-13)
7. **Potential SRS inconsistency: party contact information** — SRS §9.4 lists party "contact"; no template instance contains contact info. Consistent with Data Needs §8.2 #1 (OQ-DN-11); not resolved here.
8. **~~Potential SRS inconsistency: witness citizenship / "two witnesses per party"~~** — **RESOLVED 2026-08-13.** SRS §9.4 and BR-008 updated: minimum one witness per party, identified by name, age, and address; citizenship optional (project owner). Template's 1–3 name/address/age slots remain the observed evidence base.

---

## 11. Contradictions (flagged, not auto-resolved)

| ID | Finding | Affected artifacts |
|---|---|---|
| CON-01 | ~~`Land Rent Template Analysis.md` §1.1/§17.1 stated **7 instances (6 complete + 1 partially blank)** while fresh `pdftotext -layout` extraction found **8 instances (7 complete + 1 partially blank)**. SD-03/SD-04 are near-duplicate business instances; the Template Analysis count likely merged SD-07 (Tab 7, second Sunil/Dawa instance) into its near-duplicate.~~ **RESOLVED 2026-08-13** — Template Analysis §1.1/§17.1 and `Requirements Adversarial Review.md` corrected to 8 instances. | Template Analysis vs fresh extraction |
| CON-02 | Template Analysis §1.6 states "The PDF is 20 pages" — **confirmed** (pdfinfo: 20 pages). No conflict. (Recorded for completeness against an earlier note that it was 8 pages.) | Template Analysis |
| CON-03 | Two legal-basis preamble forms coexist within the agricultural set (SD-01/02/07/08 vs SD-05). No rule selects between them. | CLAUSE-AGR-002; BR-027/BR-028 |
| CON-04 | SD-05 exits via structure-handover + breach-remedy while SD-01/02/07/08 exit via agricultural-restoration + amendment + governing law. An either/or structure is implied but unstated. | CLAUSE-AGR-013/014/015 |
| CON-05 | SD-04 duplicates clause 2 with inconsistent escalation parameters ("१० प्रतिशत ... प्रत्येक २/२ वर्षमा" vs "२ प्रतिशत"/"२ %"). One instance internally contradicts itself — an editing artifact of the WIP file. | SD-04 (context only) |
| CON-06 | BR-024..BR-026 (rent/escalation formulas) are `[TO BE VALIDATED]` while all generated financial clauses depend on them (mirrors AR-004). | BR-024..026; CLAUSE-AGR-004 |

---

## 12. Open Questions

| ID | Question | Reference |
|---|---|---|
| OQ-CL-01 | Should the clause-library's 15-clause set be cross-checked against additional (non-agricultural or future) reference documents to confirm frequency claims? Only one reference file (8 instances) was supplied. | Task guidance; §1 |
| OQ-CL-02 | Is the grandfather/father lineage format legally required for land-rent agreements, or customary? | CLAUSE-AGR-001; OQ-TA-04 |
| OQ-CL-03 | When is citizenship (number/date/district) present vs omitted? Required or optional? | CLAUSE-AGR-001; OQ-TA-13 |
| OQ-CL-04 | Which legal-basis preamble form is current/authoritative: the two-Act "करार ऐन भाग ५" form or the "मुलुकी देवानी (सहिता) ऐन २०७४" form? | CLAUSE-AGR-002; CON-03 |
| OQ-CL-05 | Should land area be stored/rendered as structured Ropani-Anna-Paisa-Dam or single text? | CLAUSE-AGR-003; OQ-DN-01; AR-020 |
| OQ-CL-06 | Does the template support partial-area grants ("०-११-३-० मध्ये ०-८-०-०")? Observed only in business context (SD-06). | CLAUSE-AGR-003 |
| OQ-CL-07 | Are the escalation calculation formulas (BR-024..BR-026) correct? Compound vs simple; "every year" vs "every 2 years" vs "after 2 years" semantics. | CLAUSE-AGR-004; OQ-TA-23; AR-017 |
| OQ-CL-08 | SD-04's duplicate clause 2 has internally inconsistent escalation parameters (10% vs 2%). Confirm whether this is an editing artifact or a real parameter range. | SD-04 (context); CON-05 |
| OQ-CL-09 | What is the relationship between construction permission (005) and structure handover (014)? Either/or with restoration (013)? | CLAUSE-AGR-005/013/014 |
| OQ-CL-10 | Is a 5-year term universal for agricultural land rents, or does the template support other durations? Only 5-year agricultural instances observed. | CLAUSE-AGR-003; OQ-TA-22 |
| OQ-CL-11 | When is the prohibited-crops form used vs the prohibited-acts→void form? | CLAUSE-AGR-006; BR-027 |
| OQ-CL-12 | When is the rent-tax-only expense scope used vs the expanded utilities+tax+waste scope? | CLAUSE-AGR-008; OQ-DN-13 |
| OQ-CL-13 | Why is the uninterrupted-use clause (009) absent from SD-02/SD-05? Required or optional? | CLAUSE-AGR-009 |
| OQ-CL-14 | Notice-period unit model: days vs months; uniform vs per-party asymmetric; what selects each? | CLAUSE-AGR-010; AR-013 |
| OQ-CL-15 | Does the compliance/breach-remedy clause require a new entry in the Data Needs clause inventory (C01–C13)? | CLAUSE-AGR-015; §10 gap 1 |

---

## 13. Quality Checklist

| # | Check | Result |
|---|---|---|
| 1 | Clause IDs follow `CLAUSE-AGR-###`; no duplicates | PASS — 001..015 |
| 2 | Every clause backed by verbatim source text | PASS — all 15 have canonical text from SD instances |
| 3 | `⟨sic⟩` used for corrupt/ambiguous text | PASS — `दिनुहोस`, `चक्रवत`, `चक्रबध`, `वृद्धी`, `वदृधी`, `भाडा डर`, `प्रस्ताप`, `निकाएमा` |
| 4 | Variables named per Schema §5; DN/Field IDs only where real | PASS — no invented DN/Field IDs |
| 5 | No invented legal rules/clauses/variables/requirements | PASS |
| 6 | No existing requirements document modified | PASS — only 2 new files created under Clause Library/ |
| 7 | Applicability recorded; "Not established from supplied sources." used | PASS |
| 8 | Conditions recorded; "Condition requires validation." used | PASS |
| 9 | Variants classified; parameter-only differences not separate clauses | PASS — escalation-rate/amount differences are parameter variants of CLAUSE-AGR-004 |
| 10 | Categories source-representative | PASS |
| 11 | Gap vocabulary used; nothing silently fixed | PASS — §10 |
| 12 | Source Documents table present | PASS — §2 |
| 13 | Source→Clause matrix present | PASS — §7 |
| 14 | Clause→Data traceability matrix present; acquisition vocabulary restricted | PASS — §8 |
| 15 | Coverage Findings present | PASS — §9 |
| 16 | Contradictions flagged, not auto-resolved | PASS — §11 |
| 17 | Open Questions raised; OQ-CL-### IDs | PASS — 15 questions |
| 18 | Legal validation status marked; no legal conclusions | PASS |
| 19 | Final report with 10 required counts | PASS — §14 |
| 20 | Project markdown conventions; no emojis/decorative content | PASS |

---

## 14. Final Report

1. **Clauses identified:** **15** (CLAUSE-AGR-001..015) + 5 document framework element groups (signatures ×2, witnesses, writer, date).
2. **Variables identified:** **56** — party identity 20 (P1 10 + P2 10), company 5, property 7 (district, ward, kitta, area R-A-P-D (4), land category, use purpose), rent/term 8 (period, amount, amountWords, escalation period, escalation rate, escalation method, payment timing, notice), signature 2, witness 9, writer 2, date 4. (Duplicated use of `property.usePurpose` across clauses counted once.)
3. **Source documents analyzed:** **1 physical file** (`Land Rent - WIP.pdf`, 20 pages) containing **8 instance documents**; **5 agricultural instances** form the primary source set; 3 business/residential instances catalogued as context.
4. **Clauses appearing in multiple documents:** **13 of 15** — 8 universal, 5 common (4/5) + 1 rare (3/5). Only 2 (structure handover, breach remedy) are single-instance.
5. **Clause variants:** **26 recorded** across the 15 clauses — wording 14, structural 8, parameter 3 (rent amount/rate/period, notice period, escalation period), conditional 1 (form selection). (Context-instance variants counted separately where noted.)
6. **Variables mapped to existing Data Needs:** **51 of 53** mapped (20 party + 5 company + 7 property + 8 rent/term + 2 signature + 9 witness... = 51). **2 unmapped:** `writer.licenseNumber` (no Field/Data Need — OQ-DN-03) and `property.landCategory` Guthi-rendering semantics (DN-PROP-05 `PROPOSED`). Witness/date/writer are framework elements, not clause variables.
7. **Data Needs gaps:** **6** reported (§10): breach-remedy clause inventory entry; writer license number; Guthi land-category rendering; lease-start date field; deposit amount; conditional form-selection driver.
8. **Legal/domain validation questions:** **15 open questions** (OQ-CL-01..15), plus inherited unresolved items (OQ-TA-12/13/23, OQ-DN-01/03/05/11/12/13, AR-004/013/017/020).
9. **Contradictions:** **6 flagged** (§11), incl. the Template Analysis instance-count discrepancy (7 vs 8), the two legal-basis forms, the either/or exit structure, SD-04's self-contradictory clause 2, and unvalidated financial formulas.
10. **Assumptions requiring human review:** **(a)** the 5-instance source set is representative of agricultural land rents generally (single supplied file); **(b)** clause presence/absence in SD-05 reflects a real structural variant, not a defect; **(c)** "चक्रवृद्धि/compound" escalation is intended wherever the source renders `चक्रवत/चक्रबध`; **(d)** `वर्ष __` (blank age) and blank citizenship render as optional blanks; **(e)** the two legal-basis forms are both legitimate variants.

> **No legal authority is claimed.** This library describes source content only; every legally consequential item is marked for legal/domain review.
