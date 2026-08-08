# Data Needs — Land-Rent Document Preparation

> **Working Analysis Document** — Data needs derived from the Field Dictionary (`Land Rent Template Analysis.md` §4.1) and the SRS data requirements (`SRS/SRS.md` §9). This document is an intermediate requirements artifact feeding the SRS Gap Analysis and SRS v0.2. It is NOT a final specification or database schema.

| Field | Value |
|---|---|
| **Document Status** | Draft — Initial Analysis Complete |
| **Date** | 2026-08-08 |
| **Derived From** | Field Dictionary (Template Analysis §4.1), Field Origin Classification (§11), Template Variable Model (§13), SRS §9 |
| **Related SRS** | `SRS/SRS.md` (v0.1 Working Draft) §9 |
| **Related Analysis** | `Land Rent Template Analysis.md` |
| **Related Use Cases** | `Use Cases.md` |

---

## 1. Data Need Groups

Data needs are organized into the following groups, which correspond to the template's logical data areas:

| Group ID | Group Name | Purpose | Primary Source Documents |
|---|---|---|---|
| DN-P1 | First Party Information | Landowner/lessor identity | Citizenship Certificate, verbal |
| DN-P2 | Second Party Information | Tenant/lessee identity (individual or company) | Citizenship Certificate, Company Registration Certificate, verbal |
| DN-PROP | Property Information | Land description | Lalpurja / land record |
| DN-RENT | Rental and Term Information | Financial and term conditions | Client verbal / operator |
| DN-WIT | Witnesses | Witness identity | Client verbal |
| DN-WRI | Writer | Document drafter identity | Operator |
| DN-DOC | Document and Date Information | Output document metadata, BS date | System-generated |
| DN-CASE | Case Information | Case-level data and lifecycle | System-generated / operator |
| DN-SRC | Source Document Metadata | Capture/upload provenance | System-generated |

---

## 2. Data Need Inventory

**Legend:** Source types follow Template Analysis §11 — `SOURCE_DERIVED` (from a source document), `USER_PROVIDED` (client/operator verbal), `CALCULATED` (computed by system), `SYSTEM_GENERATED` (created by system), `STATIC_TEMPLATE` (fixed template text, not a data need).

### DN-P1 — First Party Information

| Data Need ID | Field Dict ID | Human Meaning | Source | Type | Required | Sensitivity | Verification |
|---|---|---|---|---|---|---|---|
| DN-P1-01 | P1_FULL_NAME | First Party Full Name | SOURCE_DERIVED | string | CONFIRMED | High | Required |
| DN-P1-02 | P1_GRANDFATHER | First Party Grandfather | SOURCE_DERIVED | string | PROPOSED | Medium | Required |
| DN-P1-03 | P1_FATHER | First Party Father | SOURCE_DERIVED | string | CONFIRMED | Medium | Required |
| DN-P1-04 | P1_DISTRICT | First Party District | SOURCE_DERIVED | string | CONFIRMED | Medium | Required |
| DN-P1-05 | P1_MUNICIPALITY | First Party Municipality | SOURCE_DERIVED | string | CONFIRMED | Medium | Required |
| DN-P1-06 | P1_WARD | First Party Ward | SOURCE_DERIVED | string/number | CONFIRMED | Medium | Required |
| DN-P1-07 | P1_AGE | First Party Age | SOURCE_DERIVED / USER_PROVIDED | number | CONFIRMED | Low | Required |
| DN-P1-08 | P1_CITIZENSHIP_NUM | First Party Citizenship Number | SOURCE_DERIVED | string | PROPOSED | High | Required |
| DN-P1-09 | P1_CITIZENSHIP_DATE | Citizenship Issue Date (BS) | SOURCE_DERIVED | date (BS) | PROPOSED | Medium | Required |
| DN-P1-10 | P1_CITIZENSHIP_DIST | Citizenship Issue District | SOURCE_DERIVED | string | PROPOSED | Medium | Required |
| DN-P1-11 | P1_SIGNATURE_NAME | First Party Signature Name | SYSTEM_GENERATED / USER_PROVIDED | string | CONFIRMED | Medium | Required |

> **Conditional:** First Party may consist of multiple co-owners (up to 3 observed). Each co-owner repeats DN-P1-01 through DN-P1-10. **Multiplicity:** DN-P1 group repeats per co-owner.

### DN-P2 — Second Party Information

| Data Need ID | Field Dict ID | Human Meaning | Source | Type | Required | Sensitivity | Verification |
|---|---|---|---|---|---|---|---|
| DN-P2-01 | P2_FULL_NAME | Second Party Full Name | SOURCE_DERIVED | string | CONFIRMED | High | Required |
| DN-P2-02 | P2_GRANDFATHER | Second Party Grandfather | SOURCE_DERIVED | string | PROPOSED | Medium | Required |
| DN-P2-03 | P2_FATHER | Second Party Father | SOURCE_DERIVED | string | CONFIRMED | Medium | Required |
| DN-P2-04 | P2_DISTRICT | Second Party District | SOURCE_DERIVED | string | CONFIRMED | Medium | Required |
| DN-P2-05 | P2_MUNICIPALITY | Second Party Municipality | SOURCE_DERIVED | string | CONFIRMED | Medium | Required |
| DN-P2-06 | P2_WARD | Second Party Ward | SOURCE_DERIVED | string/number | CONFIRMED | Medium | Required |
| DN-P2-07 | P2_AGE | Second Party Age | SOURCE_DERIVED / USER_PROVIDED | number | CONFIRMED | Low | Required |
| DN-P2-08 | P2_CITIZENSHIP_NUM | Second Party Citizenship Number | SOURCE_DERIVED | string | PROPOSED | High | Required |
| DN-P2-09 | P2_CITIZENSHIP_DATE | Citizenship Issue Date (BS) | SOURCE_DERIVED | date (BS) | PROPOSED | Medium | Required |
| DN-P2-10 | P2_CITIZENSHIP_DIST | Citizenship Issue District | SOURCE_DERIVED | string | PROPOSED | Medium | Required |
| DN-P2-11 | P2_SIGNATURE_NAME | Second Party Signature Name | SYSTEM_GENERATED / USER_PROVIDED | string | CONFIRMED | Medium | Required |

**Company variant (CONDITIONAL — when Second Party is an entity):**

| Data Need ID | Field Dict ID | Human Meaning | Source | Type | Required | Sensitivity | Verification |
|---|---|---|---|---|---|---|---|
| DN-P2-12 | P2_COMPANY_NAME | Company Name | SOURCE_DERIVED | string | CONDITIONAL | Medium | Required |
| DN-P2-13 | P2_COMPANY_REG | Company Registration Number | SOURCE_DERIVED | string | CONDITIONAL | Medium | Required |
| DN-P2-14 | P2_COMPANY_REG_DATE | Company Registration Date | SOURCE_DERIVED | date (BS/AD) | CONDITIONAL | Medium | Required |
| DN-P2-15 | P2_COMPANY_REG_OFFICE | Company Registrar Office | SOURCE_DERIVED | string | CONDITIONAL | Medium | Required |
| DN-P2-16 | P2_COMPANY_PROPRIETOR | Company Proprietor | SOURCE_DERIVED | string | CONDITIONAL | Medium | Required |

> **Conditional:** DN-P2-12..16 apply only when the Second Party is a company. Individual variant uses DN-P2-01..11.

### DN-PROP — Property Information

| Data Need ID | Field Dict ID | Human Meaning | Source | Type | Required | Sensitivity | Verification |
|---|---|---|---|---|---|---|---|
| DN-PROP-01 | PROP_DISTRICT | Property District (ल.पु.जि.) | SOURCE_DERIVED | string | CONFIRMED | Medium | Required |
| DN-PROP-02 | PROP_WARD | Property Ward | SOURCE_DERIVED | string/number | CONFIRMED | Medium | Required |
| DN-PROP-03 | PROP_KITTA_NUM | Kitta Number(s) | SOURCE_DERIVED | string[] | CONFIRMED | High | Required |
| DN-PROP-04 | PROP_AREA | Land Area (Ropani-Anna-Paisa-Dam) | SOURCE_DERIVED | string (R-A-P-D) | CONFIRMED | High | Required |
| DN-PROP-05 | PROP_TYPE_LAND | Land Category / Registration Type | SOURCE_DERIVED | string | PROPOSED | Medium | Required |
| DN-PROP-06 | PROP_USE_PURPOSE | Use Purpose | USER_PROVIDED | string (enum) | CONFIRMED | Medium | Not required (judgment) |

> **Area format note:** Area uses the Ropani system: `Ropani-Anna-Paisa-Dam` (०-०-०-०). The SRS does not currently specify this format — see Gap Analysis.
> **Conditional:** DN-PROP-03 may contain multiple kitta numbers (two observed). DN-PROP-05 may carry Guthi references.

### DN-RENT — Rental and Term Information

| Data Need ID | Field Dict ID | Human Meaning | Source | Type | Required | Sensitivity | Verification |
|---|---|---|---|---|---|---|---|
| DN-RENT-01 | RENT_AMOUNT | Rent Amount (figures, NPR) | USER_PROVIDED | number | CONFIRMED | High | Required |
| DN-RENT-02 | RENT_AMOUNT_WORDS | Rent Amount (Nepali words) | CALCULATED | string | CONFIRMED | High | Required |
| DN-RENT-03 | RENT_PERIOD | Rent Period (मासिक/वार्षिक) | USER_PROVIDED | string (enum) | CONFIRMED | Medium | Required |
| DN-RENT-04 | RENT_ESCALATION_RATE | Escalation Rate | USER_PROVIDED | number (%) | CONFIRMED | Medium | Required |
| DN-RENT-05 | RENT_ESCALATION_PERIOD | Escalation Period | USER_PROVIDED | string | CONFIRMED | Medium | Required |
| DN-RENT-06 | RENT_PAYMENT_TIMING | Payment Timing (अग्रिम etc.) | USER_PROVIDED | string | CONFIRMED | Medium | Required |
| DN-RENT-07 | RENT_ESCALATION_METHOD | Escalation Method (compound/simple) | USER_PROVIDED | string (enum) | PROPOSED | Medium | Required |
| DN-RENT-08 | TERM_DURATION | Term Duration (years) | USER_PROVIDED | number | CONFIRMED | High | Required |
| DN-RENT-09 | NOTICE_PERIOD | Notice Period | USER_PROVIDED | number (days/months) | CONFIRMED | Medium | Required |

> **Calculation note:** DN-RENT-02 (words) is CALCULATED from DN-RENT-01. Escalation amounts are implied CALCULATED values — see Template Analysis §7.2 (patterns [TO BE VALIDATED]).

### DN-WIT — Witnesses

| Data Need ID | Field Dict ID | Human Meaning | Source | Type | Required | Sensitivity | Verification |
|---|---|---|---|---|---|---|---|
| DN-WIT-01 | WITNESS_1_NAME | Witness 1 Name | USER_PROVIDED | string | PROPOSED | Medium | Required |
| DN-WIT-02 | WITNESS_1_ADDRESS | Witness 1 Address | USER_PROVIDED | string | PROPOSED | Medium | Required |
| DN-WIT-03 | WITNESS_1_AGE | Witness 1 Age | USER_PROVIDED | number | PROPOSED | Low | Required |
| DN-WIT-04 | WITNESS_2_NAME | Witness 2 Name | USER_PROVIDED | string | PROPOSED | Medium | Required |
| DN-WIT-05 | WITNESS_2_ADDRESS | Witness 2 Address | USER_PROVIDED | string | PROPOSED | Medium | Required |
| DN-WIT-06 | WITNESS_2_AGE | Witness 2 Age | USER_PROVIDED | number | PROPOSED | Low | Required |
| DN-WIT-07 | WITNESS_3_NAME | Witness 3 Name | USER_PROVIDED | string | PROPOSED | Medium | Required |
| DN-WIT-08 | WITNESS_3_ADDRESS | Witness 3 Address | USER_PROVIDED | string | PROPOSED | Medium | Required |
| DN-WIT-09 | WITNESS_3_AGE | Witness 3 Age | USER_PROVIDED | number | PROPOSED | Low | Required |

> **Multiplicity:** 1–3 witnesses observed. Repeatable structure (WITNESS_3 appears in one instance only).

### DN-WRI — Writer

| Data Need ID | Field Dict ID | Human Meaning | Source | Type | Required | Sensitivity | Verification |
|---|---|---|---|---|---|---|---|
| DN-WRI-01 | WRITER_NAME | Writer / Scribe (लेखक/मसौदाकार) | USER_PROVIDED | string | PROPOSED | Low | Not required (operator knows) |

> Note: One instance includes a professional license number (प्र.प.नं. ३४६). Whether license number is a distinct data need is [OPEN QUESTION].

### DN-DOC — Document and Date Information

| Data Need ID | Field Dict ID | Human Meaning | Source | Type | Required | Sensitivity | Verification |
|---|---|---|---|---|---|---|---|
| DN-DOC-01 | DATE_YEAR | Bikram Sambat Year | SYSTEM_GENERATED | number (BS) | CONFIRMED | Medium | Not required |
| DN-DOC-02 | DATE_MONTH | Nepali Month Name | SYSTEM_GENERATED | string (Nepali) | CONFIRMED | Medium | Not required |
| DN-DOC-03 | DATE_DAY | BS Day | SYSTEM_GENERATED | number | CONFIRMED | Medium | Not required |
| DN-DOC-04 | DATE_WEEKDAY | BS Weekday (रोज १–७) | SYSTEM_GENERATED | number | CONFIRMED | Medium | Not required |
| DN-DOC-05 | (proposed) | Template Identity & Version | SYSTEM_GENERATED | string | CONFIRMED | Low | Not required |
| DN-DOC-06 | (proposed) | Generation / Finalization Metadata | SYSTEM_GENERATED | timestamp/operator | CONFIRMED | Low | Not required |

> The SRS (FR-021, FR-029) requires template identity/version and finalization metadata. BS date support is not currently specified in the SRS — see Gap Analysis.

### DN-CASE — Case Information

| Data Need ID | SRS Reference | Human Meaning | Source | Required | Notes |
|---|---|---|---|---|---|
| DN-CASE-01 | §9.2 | Case Identifier | SYSTEM_GENERATED | CONFIRMED | FR-005 |
| DN-CASE-02 | §9.2 | Case Status | SYSTEM_GENERATED | CONFIRMED | FR-007 |
| DN-CASE-03 | §9.2 | Creation date and operator | SYSTEM_GENERATED | CONFIRMED | FR-008 |
| DN-CASE-04 | §9.2 | Finalization date and operator | SYSTEM_GENERATED | CONFIRMED | FR-029 |
| DN-CASE-05 | §9.2 | Case notes | USER_PROVIDED | PROPOSED | — |

### DN-SRC — Source Document Metadata

| Data Need ID | SRS Reference | Human Meaning | Source | Required | Notes |
|---|---|---|---|---|---|
| DN-SRC-01 | §9.6 | Document type label | USER_PROVIDED | CONFIRMED | FR-011 |
| DN-SRC-02 | §9.6 | Capture/upload timestamp | SYSTEM_GENERATED | CONFIRMED | — |
| DN-SRC-03 | §9.6 | File format | SYSTEM_GENERATED | CONFIRMED | — |
| DN-SRC-04 | §9.6 | Association to case | SYSTEM_GENERATED | CONFIRMED | — |
| DN-SRC-05 | §9.6 | Stored image/file | SYSTEM_GENERATED | CONFIRMED | Retention [OPEN QUESTION] |

---

## 3. Data Lifecycle Needs

In addition to the field-level needs above, the system must support the Candidate → Verified lifecycle (SRS §9.7, §9.8, §10.1):

| Data Need ID | SRS Reference | Need | Notes |
|---|---|---|---|
| DN-LIFE-01 | §9.7 | Retain Candidate Data (pre-verification values) | Origin indicator, confidence (if extraction), original value [OPEN QUESTION: permanent retention] |
| DN-LIFE-02 | §9.8 | Retain Verified Case Data | Verification timestamp, verifying operator, correction history |
| DN-LIFE-03 | §10.4 | Retain draft generation/edit metadata | Whether previous drafts are retained is [OPEN QUESTION] |
| DN-LIFE-04 | §10.5 | Persist Finalized System Records | Immutable, non-editable after finalization |
| DN-LIFE-05 | §9.12 | Audit records | Event, timestamp, operator, reference |

---

## 4. Origin Summary

Derived from Template Analysis §11 (Field Origin Classification):

| Origin | Count | Data Needs |
|---|---|---|
| SOURCE_DERIVED | ~20 | Party identity, citizenship, property, company registration |
| USER_PROVIDED | ~10+ | Rent, purpose, duration, escalation, notice, witnesses, writer |
| CALCULATED | ~2 | Rent words, escalation amounts |
| SYSTEM_GENERATED | ~3 | Date (BS), case ID, template metadata |
| CONDITIONAL | ~6 | Company fields, multi-kitta, multi-party, Guthi |

---

## 5. Open Questions

| ID | Question |
|---|---|
| OQ-DN-01 | Should area be stored as structured Ropani-Anna-Paisa-Dam fields or as a single text string? [OQ-TA-17] |
| OQ-DN-02 | Should addresses be structured (district/municipality/ward) or free text? [OQ-TA-19] |
| OQ-DN-03 | Should writer license number be a distinct data need? |
| OQ-DN-04 | Should the system support both Ropani and Square Meter area systems? [OQ-TA-18] |
| OQ-DN-05 | What is the complete list of use purposes? [OQ-TA-20] |
| OQ-DN-06 | Should original Candidate Data values be retained permanently? [SRS §9.8 OPEN QUESTION] |
