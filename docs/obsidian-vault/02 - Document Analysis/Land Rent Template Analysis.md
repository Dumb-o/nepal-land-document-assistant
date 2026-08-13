# Land Rent Template Analysis

> **Working Analysis Document** — This document is a formal analysis of the actual land-rent template provided for the Nepal Land Document Assistant project. Findings are based on template examination and may require domain validation. This is NOT a finalized specification.

| Field | Value |
|---|---|
| **Analysis Status** | Draft — Initial Analysis Complete |
| **Date Analyzed** | 2026-07-28 |
| **Source Template Filename** | `Land Rent - WIP.pdf` |
| **Template Version** | Unknown — appears to be a working document (WIP) containing multiple filled examples |
| **Related SRS** | `docs/obsidian-vault/03 - Requirements/SRS/SRS.md` (v0.1 Working Draft) |
| **Analysis Scope** | Document structure, field extraction, static/variable/conditional content, source document mapping, template generation requirements |

---

## 1. Document Overview

### 1.1 General Description

The source document is a collection of **7 filled-in examples** of the Nepali **जग्गा बहाल सम्झौता पत्र** (Land Rent Agreement Letter), with the last instance partially filled (containing blank fields for the tenant/second party). The document is marked **"WIP"** (Work In Progress), suggesting it is a working reference document for template design.

### 1.2 Document Purpose

To establish a formal rental/lease agreement between a landowner (प्रथम पक्ष — First Party) and a tenant (द्वितीय/द्रितिय पक्ष — Second Party) for agricultural, commercial, or residential use of land in Nepal.

### 1.3 Apparent Document Type

Private contractual agreement. The template references governing law: **मुलुकी देवानी सहिंता ऐन २०७४** (Muluki Civil Code 2074) and **मुलुकी कार्यबिधि ऐन २०७४** (Muluki Procedure Code 2074), specifically **करार ऐन भाग ५** (Contract Act Part 5).

### 1.4 Language and Script

- **Language:** Nepali
- **Script:** Devanagari
- **Numerals:** Nepali/Devanagari numerals for dates (Bikram Sambat); mixed usage of Nepali and English/Hindu-Arabic numerals for monetary amounts (e.g., `रु ६५,०००/-`, `रु २०,०००/-`)
- **Dates:** Bikram Sambat (Nepali calendar) — format: इतिसम्बत २०८३ साउन महिना १० गते रोज १

### 1.5 Overall Structure

A consistent structure across all 7 instances:

1. **Title** — जग्गा बहाल सम्झौता पत्र
2. **Preamble (लिखितम)** — Party identification, legal references, consent statement
3. **Body (तपसिल)** — Numbered clauses (7–9 items)
4. **Signature Area** — First Party and Second Party
5. **Witness Section (साक्षी)** — 1–3 witnesses
6. **Writer Identification (लेखक/मसौदाकार)** — Who drafted the document
7. **Date (इति सम्बत)** — Bikram Sambat date

### 1.6 Approximate Length

~0.5–1 page per agreement instance in printed form. The PDF is 20 pages.

### 1.7 Structure Stability

The overall structure appears **stable** and consistent across all 7 examples. The core preamble formula and clause pattern are repeated with minimal variation.

### 1.8 Reusable Template Status

The document **is** a reusable template. The last instance (Ram Maharjan) shows explicitly blank fields for the tenant's identifying information, indicating the intended blank-template form.

### 1.9 Variants / Conditional Sections

Multiple variants exist (see Section 11 for full analysis):

| Variation | Examples |
|---|---|
| **Use Purpose** | Agriculture (कृषि प्रयोजन), Business (व्यापार व्यवसाय), Residence (बसोबास) |
| **Rent Period** | Monthly (मासिक), Annual (वार्षिक) |
| **Escalation Pattern** | Per year, every 2 years, after 2 years |
| **Escalation Rate** | 5%, 10%, ₹10,000 fixed step |
| **Notice Period** | 30 days, 60 days, 3 months, 6 months |
| **Party 2 Type** | Individual, Company with registration number |
| **Number of Party 1 Individuals** | Single person, multiple co-owners (up to 3) |

---

## 2. Document Structure Analysis

The template follows this consistent section ordering:

| Section ID | Section (Nepali)                                       | Purpose                                                | Content Type                    | Notes                                        |
| ---------- | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------- | -------------------------------------------- |
| S01        | शीर्षक — जग्गा बहाल सम्झौता पत्र                       | Document title                                         | Static                          | Identical across all instances               |
| S02        | लिखितम — Preamble                                      | Party identification, legal basis, consent declaration | Static + Variable               | Contains party lineage, citizenship, address |
| S03        | तपसिल — Body/Clauses                                   | Numbered terms and conditions                          | Static + Variable + Conditional | 7–9 clauses depending on variant             |
| S04        | प्रथम पक्ष हस्ताक्षर — First Party Signature           | Landlord/Owner signature area                          | Static + Variable               | Names of first party individuals             |
| S05        | दोश्रो/द्वितीय पक्ष हस्ताक्षर — Second Party Signature | Tenant signature area                                  | Static + Variable               | Name of second party individual              |
| S06        | साक्षी — Witnesses                                     | Witness names and addresses                            | Static + Variable               | 1–3 witnesses                                |
| S07        | लेखक/मसौदाकार — Writer                                 | Name of person who drafted the document                | Variable                        | Sometimes same as one of the parties         |
| S08        | मिति/सम्बत — Date                                      | Bikram Sambat date                                     | Variable                        | इतिसम्बत YYYY मिति महिना GG गते रोज N        |

---

## 3. Static Content Analysis

### 3.1 Confirmed Static (appears identically in all instances)

| Content | Location | Description |
|---|---|---|
| जग्गा बहाल सम्झौता पत्र | S01 — Title | Document title — identical across all instances |
| लिखितम | S02 — Preamble start | Standard preamble opening |
| (जसलाई यस लिखतमा प्रथम पक्ष भनि सम्बोधन गरिएको) | S02 — Party 1 designation | Standard party designation clause |
| (जसलाई यस लिखतमा द्रितिय/द्वितीय पक्ष भनि सम्बोधन गरिएको) | S02 — Party 2 designation | Standard party designation clause |
| का बीचमा दुवै पक्षको सहमति मंजुर भै जग्गा बहालमा लिने दिने सम्बन्धमा मुलुकी देवानी सहिंता ऐन २०७४, मुलुकी कार्यबिधि ऐन २०७४ को करार ऐन भाग ५ बमोजिम परिपालन गर्ने गरी | S02 — Legal basis | Reference to governing law — identical wording |
| दुवै पक्षको सहमतिमा प्रथम पक्षको घर बैठकमा बसी । लेखि लेखाई दुवै पक्षले दाया दाया बाया सहिछाप गरी एक/एक प्रति लियौ दियौ । साक्षी तपसिलमा मानिस सदर । | S02 — Consent and execution clause | Standard closing of preamble |
| तपसिल | S03 — Body heading | Standard heading for the clauses section |
| प्रथम पक्ष | S04 — First Party label | Signature area label |
| दोश्रो/द्वितीय पक्ष | S05 — Second Party label | Signature area label |
| साक्षी | S06 — Witness label | Witness section heading |
| इति सम्बत | S08 — Date prefix | Standard date prefix |
| शुभम् | S08 — Auspicious closing | Standard closing word |

### 3.2 Likely Static (appears in most instances with minor wording variations)

Standard clauses that appear in most/all instances with near-identical wording:

- **Clause 1** — Land description and offer/acceptance formula
- **Party obligation clause** — First party shall allow uninterrupted use
- **Prohibition on subletting** — Second party shall not sublet
- **Amendment clause** — Terms may be amended by mutual consent
- **Governing law clause** — Matters not covered shall follow prevailing law
- **Agriculture restoration clause** — Land must be returned in cultivable condition

### 3.3 Potentially Variable

| Content | Location | Notes |
|---|---|---|
| Legal references | S02 | Some instances vary between संहिता vs सहिंता, कार्यबिधि vs कार्यविधि |


## 4. Variable Field Extraction

### 4.1 Field Inventory

| Field ID | Field Name (English) | Field Name (Nepali) | Human Meaning | Data Type | Required? | Classification | Location in Template | Notes |
|---|---|---|---|---|---|---|---|---|
| P1_FULL_NAME | First Party Full Name | प्रथम पक्षको पुरा नाउँ | Landowner's full name | Text (string) | CONFIRMED | VARIABLE | S02 — Preamble | Appears in all instances |
| P1_GRANDFATHER | First Party Grandfather | प्रथम पक्षको नाती/नातिनी | Grandfather's name | Text (string) | PROPOSED | VARIABLE | S02 — Preamble | Appears in most instances |
| P1_FATHER | First Party Father | प्रथम पक्षको छोरा/बुवा | Father's name | Text (string) | CONFIRMED | VARIABLE | S02 — Preamble | Appears in all instances |
| P1_DISTRICT | First Party District | प्रथम पक्षको जिल्ला | Home district | Text (string) | CONFIRMED | VARIABLE | S02 — Preamble | |
| P1_MUNICIPALITY | First Party Municipality | प्रथम पक्षको नगरपालिका/गाउँपालिका | Municipality/Village body | Text (string) | CONFIRMED | VARIABLE | S02 — Preamble | |
| P1_WARD | First Party Ward | प्रथम पक्षको वडा | Ward number | Text (string/number) | CONFIRMED | VARIABLE | S02 — Preamble | |
| P1_AGE | First Party Age | प्रथम पक्षको उमेर | Age in years | Number | CONFIRMED | VARIABLE | S02 — Preamble | Blank in some instances (__) |
| P1_CITIZENSHIP_NUM | First Party Citizenship | प्रथम पक्षको ना.प्र.न. | Citizenship number | Text (string) | PROPOSED | VARIABLE | S02 — Preamble | Not present in all instances |
| P1_CITIZENSHIP_DATE | First Party Citizenship Issue Date | प्रथम पक्षको ना.प्र.न. जारी मिति | Citizenship issue date | Date (BS) | PROPOSED | VARIABLE | S02 — Preamble | |
| P1_CITIZENSHIP_DIST | First Party Citizenship District | प्रथम पक्षको ना.प्र.न. जारी जिल्ला | Citizenship issue district | Text (string) | PROPOSED | VARIABLE | S02 — Preamble | Sometimes at end of line |
| P2_FULL_NAME | Second Party Full Name | द्वितीय पक्षको पुरा नाउँ | Tenant's full name | Text (string) | CONFIRMED | VARIABLE | S02 — Preamble | Blank in Ram Maharjan template |
| P2_GRANDFATHER | Second Party Grandfather | द्वितीय पक्षको नाती/नातिनी | Grandfather's name | Text (string) | PROPOSED | VARIABLE | S02 — Preamble | |
| P2_FATHER | Second Party Father | द्वितीय पक्षको छोरा/बुवा | Father's name | Text (string) | CONFIRMED | VARIABLE | S02 — Preamble | |
| P2_DISTRICT | Second Party District | द्वितीय पक्षको जिल्ला | Home district | Text (string) | CONFIRMED | VARIABLE | S02 — Preamble | |
| P2_MUNICIPALITY | Second Party Municipality | द्वितीय पक्षको नगरपालिका/गाउँपालिका | Municipality/Village body | Text (string) | CONFIRMED | VARIABLE | S02 — Preamble | |
| P2_WARD | Second Party Ward | द्वितीय पक्षको वडा | Ward number | Text (string/number) | CONFIRMED | VARIABLE | S02 — Preamble | |
| P2_AGE | Second Party Age | द्वितीय पक्षको उमेर | Age in years | Number | CONFIRMED | VARIABLE | S02 — Preamble | Blank in some instances |
| P2_CITIZENSHIP_NUM | Second Party Citizenship | द्वितीय पक्षको ना.प्र.न. | Citizenship number | Text (string) | PROPOSED | VARIABLE | S02 — Preamble | |
| P2_CITIZENSHIP_DATE | Second Party Citizenship Issue Date | द्वितीय पक्षको ना.प्र.न. जारी मिति | Citizenship issue date | Date (BS) | PROPOSED | VARIABLE | S02 — Preamble | |
| P2_CITIZENSHIP_DIST | Second Party Citizenship District | द्वितीय पक्षको ना.प्र.न. जारी जिल्ला | Citizenship issue district | Text (string) | PROPOSED | VARIABLE | S02 — Preamble | |
| P2_COMPANY_NAME | Second Party Company Name | द्वितीय पक्षको कम्पनी नाम | Company name (if entity) | Text (string) | CONDITIONAL | VARIABLE | S02 — Preamble | One instance shows company with registration |
| P2_COMPANY_REG | Second Party Company Registration | द्वितीय पक्षको दर्ता नं. | Company registration number | Text (string) | CONDITIONAL | VARIABLE | S02 — Preamble | |
| P2_COMPANY_REG_DATE | Second Party Company Reg. Date | द्वितीय पक्षको दर्ता मिति | Company registration date | Date (BS/AD) | CONDITIONAL | VARIABLE | S02 — Preamble | |
| P2_COMPANY_REG_OFFICE | Second Party Company Reg. Office | कम्पनी रजिष्ट्रारको कार्यालय | Company registrar office | Text (string) | CONDITIONAL | VARIABLE | S02 — Preamble | |
| P2_COMPANY_PROPRIETOR | Second Party Company Proprietor | प्रप्राइतर | Company proprietor name | Text (string) | CONDITIONAL | VARIABLE | S02 — Preamble | |
| PROP_DISTRICT | Property District | ल.पु.जि. | Land revenue district | Text (string) | CONFIRMED | VARIABLE | S03 — Clause 1 | |
| PROP_WARD | Property Ward | वडा नं. | Ward number | Text (string/number) | CONFIRMED | VARIABLE | S03 — Clause 1 | |
| PROP_KITTA_NUM | Property Kitta Number | कित्ता नं. | Plot/Kitta number | Text (string) | CONFIRMED | VARIABLE | S03 — Clause 1 | One instance has two kitta numbers |
| PROP_AREA | Property Area | क्षेत्रफल | Land area in Ropani-Anna-Paisa-Dam | Text (string) | CONFIRMED | VARIABLE | S03 — Clause 1 | Format: ०-०-०-० (R-A-P-D) |
| PROP_TYPE_LAND | Property Land Category | ज.ध. महल / ल.पु.जी. | Land category/registration type | Text (string) | PROPOSED | VARIABLE | S03 — Clause 1 | Guthi registration appears in some |
| PROP_USE_PURPOSE | Property Use Purpose | प्रयोजन | Intended use (agriculture/business/residence) | Text (string) | CONFIRMED | VARIABLE | S03 — Clause 1 | Affects which clauses are included |
| RENT_AMOUNT | Rent Amount | भाडा रकम | Monetary rent amount | Number (NPR) | CONFIRMED | VARIABLE | S03 — Clause 2 | In words and figures |
| RENT_AMOUNT_WORDS | Rent Amount (Words) | अक्षेरुपिय | Rent amount in Nepali words | Text (string) | CONFIRMED | VARIABLE | S03 — Clause 2 | Always follows figure amount |
| RENT_PERIOD | Rent Period | भाडा अवधि | Monthly or annual rent | Text (मासिक/वार्षिक) | CONFIRMED | VARIABLE | S03 — Clause 2 | Determines calculation formulas |
| RENT_ESCALATION_RATE | Escalation Rate | भाडा वृद्धि दर | Percentage or fixed amount increase | Number (%) | CONFIRMED | VARIABLE | S03 — Clause 2 | Typically 5% or 10% |
| RENT_ESCALATION_PERIOD | Escalation Period | भाडा वृद्धि अवधि | How often rent increases | Text (string) | CONFIRMED | VARIABLE | S03 — Clause 2 | "प्रत्येक वर्ष", "प्रत्येक २/२ वर्षमा", "२ वर्ष पछि" |
| RENT_PAYMENT_TIMING | Rent Payment Timing | भाडा भुक्तानी समय | When rent is paid | Text (अग्रिम/पश्चात्) | CONFIRMED | VARIABLE | S03 — Clause 2 | Observed: "अग्रिम" (advance) |
| RENT_ESCALATION_METHOD | Escalation Method | चक्रवृद्धि / साधारण | Compound or simple escalation | Text (string) | PROPOSED | VARIABLE | S03 — Clause 2 | "चक्रवत/चक्रवृद्धि" — compound appears in template |
| TERM_DURATION | Term Duration | करार अवधि | Lease duration in years | Number (years) | CONFIRMED | VARIABLE | S03 — Clause 1 | 3, 5, or 10 years observed |
| NOTICE_PERIOD | Notice Period | पूर्वसूचना अवधि | Notice period for termination | Number (days/months) | CONFIRMED | VARIABLE | S03 — Various | 30 days, 60 days, 3 months, 6 months observed |
| WITNESS_1_NAME | Witness 1 Name | साक्षी १ नाम | First witness name | Text (string) | PROPOSED | VARIABLE | S06 | |
| WITNESS_1_ADDRESS | Witness 1 Address | साक्षी १ ठेगाना | First witness address | Text (string) | PROPOSED | VARIABLE | S06 | "ल.पु.म.न.पा. वडा न २९ बस्ने" |
| WITNESS_1_AGE | Witness 1 Age | साक्षी १ उमेर | First witness age | Number | PROPOSED | VARIABLE | S06 | "वर्ष ५१ को" |
| WITNESS_2_NAME | Witness 2 Name | साक्षी २ नाम | Second witness name | Text (string) | PROPOSED | VARIABLE | S06 | |
| WITNESS_2_ADDRESS | Witness 2 Address | साक्षी २ ठेगाना | Second witness address | Text (string) | PROPOSED | VARIABLE | S06 | |
| WITNESS_2_AGE | Witness 2 Age | साक्षी २ उमेर | Second witness age | Number | PROPOSED | VARIABLE | S06 | |
| WITNESS_3_NAME | Witness 3 Name | साक्षी ३ नाम | Third witness name | Text (string) | PROPOSED | VARIABLE | S06 | Appears in one instance only |
| WITNESS_3_ADDRESS | Witness 3 Address | साक्षी ३ ठेगाना | Third witness address | Text (string) | PROPOSED | VARIABLE | S06 | |
| WITNESS_3_AGE | Witness 3 Age | साक्षी ३ उमेर | Third witness age | Number | PROPOSED | VARIABLE | S06 | |
| WRITER_NAME | Writer Name | लेखक/मसौदाकार | Person who drafted the document | Text (string) | PROPOSED | VARIABLE | S07 | Sometimes same as a party |
| DATE_YEAR | Date Year | सम्बत वर्ष | Bikram Sambat year | Number (BS) | CONFIRMED | VARIABLE | S08 | Format: २०८३ |
| DATE_MONTH | Date Month | महिना | Nepali month name | Text (string) | CONFIRMED | VARIABLE | S08 | e.g., साउन, वैशाख, जेठ |
| DATE_DAY | Date Day | गते | Day of month | Number | CONFIRMED | VARIABLE | S08 | |
| DATE_WEEKDAY | Date Weekday | रोज | Day of week (1-7) | Number | CONFIRMED | VARIABLE | S08 | "रोज १" through "रोज ७" |
| P1_SIGNATURE_NAME | First Party Signature Name | प्रथम पक्ष हस्ताक्षर नाम | Name as written in signature area | Text (string) | CONFIRMED | VARIABLE | S04 | Same as P1_FULL_NAME in practice |
| P2_SIGNATURE_NAME | Second Party Signature Name | दोश्रो पक्ष हस्ताक्षर नाम | Name as written in signature area | Text (string) | CONFIRMED | VARIABLE | S05 | Same as P2_FULL_NAME in practice |


## 5. Party Information

### 5.1 First Party (प्रथम पक्ष) — Landlord / Lessor

The template represents the first party as an individual with a detailed family lineage:

| Field | Notes |
|---|---|
| **Full Name** | Always present |
| **Grandfather's Name** | Pattern: `[Grandfather]को नाती/नातिनी` — almost always present |
| **Father's Name** | Pattern: `[Father]को छोरा/छोरी` — always present |
| **Address:** District/Municipality/Ward | Always present; one instance shows "हाल परिवर्तित" (currently changed) followed by new address |
| **Age** | Often left as `वर्ष __` (blank underscore) |
| **Citizenship Number** | Present in most but not all instances; prefix: ना.प्र.न. |
| **Citizenship Issue Date** | Present when citizenship number is present; Bikram Sambat date |
| **Citizenship Issue District** | Present when citizenship number is present |

**Multi-party support:** One instance shows three co-owners as first party (गंगालाल महर्जन - १, शुक्रराज महर्जन - १, चन्द्र गोविन्द महर्जन - १). The template supports multiple individuals in the same party role, listed sequentially with `- १`, `- १` markers (likely copy-paste indicators rather than formal enumeration).

### 5.2 Second Party (द्वितीय/द्रितिय पक्ष) — Tenant / Lessee

Same structure as First Party with one additional variant:

| Variant | Observed In |
|---|---|
| **Individual** (same fields as first party) | 6 of 7 instances |
| **Company/Organization** with: company name, registration number, registration date, registrar office, proprietor name | 1 of 7 instances |

### 5.3 Witnesses (साक्षी)

The template includes 1–3 witnesses:

| Field | Notes |
|---|---|
| **Witness Name** | Always present; sometimes includes relationship to party (e.g., "प्रथम पक्षको श्रीमती") |
| **Witness Address** | Present in most cases; follows address pattern: District/Municipality/Ward |
| **Witness Age** | Present in most cases; "वर्ष N को" |
| **Witness Count** | Varies from 1 to 3. No fixed minimum/maximum is apparent from the template alone. |

### 5.4 Writer (लेखक/मसौदाकार)

Present in most instances. The person who drafted the document. Sometimes same as one of the parties (e.g., "लेखक प्रथम पक्ष सुनिल महर्जन आफै"). In one instance includes a professional license number: "लेखक सत्य महर्जन प्र.प.नं. ३४६".


## 6. Property Information

### 6.1 Property Fields

| Field | Details | Example |
|---|---|---|
| **Land Revenue District** | ल.पु.जि. (Lalpurja Jilla) — the district where the land is registered | हरिसिद्धि |
| **Ward Number** | वडा नं. | ३ ख, ८ क, ५-क, ७-क |
| **Kitta Number** | कित्ता नं. (Plot identifier) | ५५१ र ६२६ (two kitta numbers in one instance), ७५, ६२६, २९८, ४५२, २६१ |
| **Area** | क्षेत्रफल in Ropani-Anna-Paisa-Dam format | ०-०-३-१, ०-४-३-१, ०-१५-१-०, ०-११-३-०, १-०-२-० |
| **Land Registration Type** | Registration category reference | जोत जनी ज.ध. महल, भवानी गुठि |

### 6.2 Area Format

The land area follows the **Ropani** system: Ropani-Anna-Paisa-Dam (०-०-०-० format). Examples observed:
- `०-०-३-१` (0 Ropani, 0 Anna, 3 Paisa, 1 Dam)
- `०-४-३-१` (0 Ropani, 4 Anna, 3 Paisa, 1 Dam)
- `०-१५-१-०` (0 Ropani, 15 Anna, 1 Paisa, 0 Dam)
- `०-११-३-०` (0 Ropani, 11 Anna, 3 Paisa, 0 Dam)
- `१-०-२-०` (1 Ropani, 0 Anna, 2 Paisa, 0 Dam)

### 6.3 Property Information Source

The property information appears to be **SOURCE_DERIVED** — obtained from the Lalpurja (land ownership certificate) or similar land records.

### 6.4 Property Use Purpose

Explicitly stated in Clause 1 of each instance:
- कृषि प्रयोजन (Agricultural purpose)
- व्यापार व्यवसाय (Business/commercial purpose)
- बसोबास प्रयोजन (Residential purpose)
- Mixed: व्यापार व्यवसाय तथा बसोबास प्रयोजन

The purpose affects which clauses are included in the agreement (see Conditional Content).


## 7. Rental and Financial Information

### 7.1 Financial Fields

| Field | Details | Examples |
|---|---|---|
| **Rent Amount (Figures)** | In Nepali rupees | रु ६५,०००/-, रु २०,०००/-, रु ३०,०००/-, रु ३५,०००/-, रु ५,५००/-, रु १०,०००/- |
| **Rent Amount (Words)** | Nepali words in parentheses | (अक्षेरुपिय पैसाठी हजार रुपैया), (अक्षेरुपिय बिस हजार रुपैया) |
| **Rent Period** | Monthly or annual | मासिक (monthly), वार्षिक (annual) |
| **Escalation Rate** | Percentage increase | ५% (5%), १०% (10%) |
| **Escalation Schedule** | When increase applies | प्रत्येक वर्ष (every year), प्रत्येक २/२ वर्षमा (every 2 years), २ वर्ष पछि (after 2 years) |
| **Escalation Method** | Compound or simple | चक्रवत/चक्रवृद्धि (compound) |
| **Payment Timing** | When payment is due | अग्रिम (in advance) |

### 7.2 Apparent Calculation Patterns

The following formulas appear to be implied by the template wording:

| Formula | Example |
|---|---|
| **Monthly rent × 12 = Annual rent** (for annual rent clauses) | रु ५,५००/मास × १२ = रु ६६,०००/वार्षिक |
| **Annual rent × Escalation rate = Increase amount** | रु ६५,००० × १०% = रु ६,५०० increase |
| **Compounding:** Year N rent = Base rent × (1 + rate)^(N-1) | "चक्रवृद्धि" method stated explicitly |

> **[TO BE VALIDATED]** These formulas are inferred from the template wording and require domain expert confirmation. The exact calculation method may vary by agreement.

### 7.3 Other Expenses Referenced

Expenses assigned to the second party (tenant) in various clauses:
- बहालकर (rent tax / land revenue tax)
- विद्युत महसुल (electricity charges)
- पानीको महसुल (water charges)
- भौतिक संरचना निर्माण कर (construction taxes)
- फोहोर व्यवस्थापन (waste management)

These are referenced as obligations in standard clauses rather than as variable fields.


## 8. Date and Term Information

### 8.1 Date Fields

| Field | Format | Example |
|---|---|---|
| **Agreement Date** | Bikram Sambat: इतिसम्बत YYYY महिना MMMM GG गते रोज N | इतिसम्बत २०८३ साउन महिना १० गते रोज १ |
| **Month Name** | Nepali month names | साउन, वैशाख, जेठ |
| **Weekday** | रोज १–७ (Sunday = 1) | रोज १ (Sunday), रोज ४ (Wednesday), रोज ६ (Friday) |
| **Term Start** | Implied: आजको मितिले (from today's date) | — |
| **Term Duration** | Explicit in years | ५ वर्ष, ३ वर्ष, १० वर्ष |

### 8.2 Calendar System

All dates use the **Bikram Sambat (BS)** calendar. No Gregorian/AD dates were observed. The system must support:
- BS year (e.g., २०८३)
- BS month names (१२ months: वैशाख, जेठ, असार, साउन, भदौ, असोज, कात्तिक, मंसिर, पुष, माघ, फाल्गुन, चैत्र)
- BS day within month (१–३२ depending on month)
- BS weekday (रोज १–७)

> **[TO BE VALIDATED]** Whether the system should also support AD dates or date conversion is not determined from the template alone.

### 8.3 Term Duration

Observed term durations in the sample instances:
- 3 years (३ वर्ष)
- 5 years (५ वर्ष)
- 10 years (१० वर्ष)

No other duration formats (months, indefinite) were observed, but these may exist in practice.


## 9. Conditional Content

### 9.1 Conditional Sections Identified

| Condition | Resulting Content | Evidence | Confidence |
|---|---|---|---|
| **Use Purpose = Agriculture** | Includes clause about prohibited crops and agriculture restoration | Clauses about निषेधित कृषी उत्पादन and कृषि योग्य बनाइ छोड्नु appear only in agriculture-focused instances | High |
| **Physical Structure Construction** | Includes clause permitting/requiring structure handover | "भौतिक संरचना निर्माण गर्न सक्ने" / "भत्काई सफा गरी छोड्ने" — present in business/residence instances | High |
| **Second Party is a Company** | Includes company registration details (registration number, date, office, proprietor) | One instance has company details with registration number | Medium |
| **Multiple First Party Individuals** | Multiple person entries in preamble and signature area | Instance with गंगालाल, शुक्रराज, चन्द्र as co-owners | High |
| **Two Kitta Numbers** | Two property entries in a single clause | "कित्ता न. ५५१ र ६२६" — one instance | Medium |
| **Guthi (Trust) Land** | References Guthi registration in property description | "हरिसिद्धि भवानी गुठि कायम" in multiple instances | Medium |
| **Professional Writer** | Writer includes professional license number | "लेखक सत्य महर्जन प्र.प.नं. ३४६" | Low |

### 9.2 Conditional Clause Analysis

The following clause-level conditionals were observed across the 7 instances:

| Clause Topic | Present In | Notes |
|---|---|---|
| Notice period for termination | Most instances | Varies: 30 days, 60 days, 3 months, 6 months |
| Physical infrastructure construction/removal | Agriculture+Business instances | Not in all agreements |
| Subletting prohibition | All instances | Standard clause |
| Tax/expense responsibility | Most instances | Varies in scope |
| Amendment by mutual consent | 4 instances | Not in all |
| Governing law | Most instances | Near-identical wording |
| Agriculture restoration | Agriculture instances only | Conditional on use purpose |
| Structure handover after term | Business instances | Conditional on physical construction |


## 10. Source Document Mapping

### 10.1 Field-to-Source Mapping

| Field ID | Field | Potential Source Document | Source Type | Extraction Method | Human Verification |
|---|---|---|---|---|---|
| P1_FULL_NAME | First Party Name | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P1_GRANDFATHER | First Party Grandfather | Citizenship Certificate, Verbal | SOURCE_DERIVED / USER_PROVIDED | Manual entry | Required |
| P1_FATHER | First Party Father | Citizenship Certificate, Verbal | SOURCE_DERIVED / USER_PROVIDED | Manual entry | Required |
| P1_DISTRICT | First Party District | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P1_MUNICIPALITY | First Party Municipality | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P1_WARD | First Party Ward | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P1_AGE | First Party Age | Citizenship Certificate / Verbal | SOURCE_DERIVED / USER_PROVIDED | Manual entry | Required |
| P1_CITIZENSHIP_NUM | First Party Citizenship No. | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required — high sensitivity |
| P1_CITIZENSHIP_DATE | First Party Citizenship Date | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P2_FULL_NAME | Second Party Name | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P2_FATHER | Second Party Father | Citizenship Certificate / Verbal | SOURCE_DERIVED / USER_PROVIDED | Manual entry | Required |
| P2_DISTRICT | Second Party District | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P2_MUNICIPALITY | Second Party Municipality | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P2_WARD | Second Party Ward | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P2_AGE | Second Party Age | Citizenship Certificate / Verbal | SOURCE_DERIVED / USER_PROVIDED | Manual entry | Required |
| P2_CITIZENSHIP_NUM | Second Party Citizenship No. | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required — high sensitivity |
| P2_CITIZENSHIP_DATE | Second Party Citizenship Date | Citizenship Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P2_COMPANY_NAME | Second Party Company Name | Company Registration Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| P2_COMPANY_REG | Second Party Company Reg. No. | Company Registration Certificate | SOURCE_DERIVED | Manual entry or OCR | Required |
| PROP_DISTRICT | Property District | Lalpurja (Land Ownership Cert.) | SOURCE_DERIVED | Manual entry or OCR | Required |
| PROP_WARD | Property Ward | Lalpurja | SOURCE_DERIVED | Manual entry or OCR | Required |
| PROP_KITTA_NUM | Kitta Number | Lalpurja | SOURCE_DERIVED | Manual entry or OCR | Required — high sensitivity |
| PROP_AREA | Property Area | Lalpurja | SOURCE_DERIVED | Manual entry or OCR | Required |
| PROP_USE_PURPOSE | Use Purpose | Client / Operator | USER_PROVIDED | Manual entry | Not required (judgment call) |
| RENT_AMOUNT | Rent Amount | Client / Operator | USER_PROVIDED | Manual entry | Required |
| RENT_AMOUNT_WORDS | Rent Amount (Words) | CALCULATED | SYSTEM_GENERATED | Auto from figures | Required |
| RENT_PERIOD | Rent Period | Client / Operator | USER_PROVIDED | Manual entry | Required |
| RENT_ESCALATION_RATE | Escalation Rate | Client / Operator | USER_PROVIDED | Manual entry | Required |
| RENT_ESCALATION_PERIOD | Escalation Period | Client / Operator | USER_PROVIDED | Manual entry | Required |
| RENT_PAYMENT_TIMING | Payment Timing | Client / Operator | USER_PROVIDED | Manual entry | Required |
| TERM_DURATION | Term Duration | Client / Operator | USER_PROVIDED | Manual entry | Required |
| NOTICE_PERIOD | Notice Period | Client / Operator | USER_PROVIDED | Manual entry | Required |
| WITNESS_DATA | Witness Information | Verbal / Client | USER_PROVIDED | Manual entry | Required |
| WRITER_NAME | Writer Name | Operator | USER_PROVIDED | Manual entry | Not required (operator knows) |
| DATE fields | Date | SYSTEM_GENERATED / USER_PROVIDED | SYSTEM_GENERATED | Auto-generated or entered | Not required |


## 11. Field Origin Classification

| Origin | Count | Fields |
|---|---|---|
| SOURCE_DERIVED | ~20 | Party identity fields, citizenship, property details, company registration |
| USER_PROVIDED | ~10 | Rent amount, purpose, duration, escalation terms, notice period, witness info |
| CALCULATED | ~2 | Rent amount in words, escalation amounts (implied) |
| STATIC_TEMPLATE | ~12 | Title, section headings, legal references, standard clauses (most of the boilerplate) |
| SYSTEM_GENERATED | ~2 | Date, case ID |
| CONDITIONAL | ~6 | Company fields, multiple kitta fields, Guthi references, multi-party fields |
| UNKNOWN | ~2 | Exact set of conditional clauses, whether all fields in every party lineage are always needed |


## 12. Data Verification Requirements

### 12.1 High-Sensitivity Fields

The following fields are particularly sensitive and require careful human verification:

| Field | Sensitivity | Reason |
|---|---|---|
| P1_CITIZENSHIP_NUM | High | Legal identification number; errors affect party identity |
| P2_CITIZENSHIP_NUM | High | Same as above |
| PROP_KITTA_NUM | High | Unique land identifier; errors could misidentify property |
| PROP_AREA | High | Affects rental obligations; embedded in legal description |
| RENT_AMOUNT (figures and words) | High | Financial obligation; words override figures in legal context |
| Party names and addresses | High | Core party identification |
| Term duration | High | Affects contract period |
| DATE fields | Medium | Dates affect contract commencement |

### 12.2 Verification Workflow

Based on the template analysis, the verification workflow should be:

```
Source Documents (Citizenship, Lalpurja)
    → Manual Entry or OCR (Candidate Data)
    → Human Verification (against source documents)
    → Verified Case Data

Client Verbal Information (rent, purpose, duration)
    → Operator Manual Entry (Candidate Data)
    → Human Verification (confirm with client notes or verbally)
    → Verified Case Data

Calculated Values (words, escalation)
    → System Generated
    → Human Verification
    → Verified Case Data
```


## 13. Template Variable Model

> [PROPOSED — BASED ON TEMPLATE ANALYSIS] This is NOT a database schema. It is a proposed logical variable model for document generation.

### 13.1 Proposed Variable Names

| Variable Name | Human Meaning | Template Location | Data Type | Source | Required | Verification |
|---|---|---|---|---|---|---|
| party.first.name | First Party Full Name | Preamble | string | SOURCE_DERIVED | Yes | Required |
| party.first.grandfather | First Party Grandfather | Preamble | string | SOURCE_DERIVED | Likely | Required |
| party.first.father | First Party Father | Preamble | string | SOURCE_DERIVED | Yes | Required |
| party.first.address.district | First Party District | Preamble | string | SOURCE_DERIVED | Yes | Required |
| party.first.address.municipality | First Party Municipality | Preamble | string | SOURCE_DERIVED | Yes | Required |
| party.first.address.ward | First Party Ward | Preamble | string/number | SOURCE_DERIVED | Yes | Required |
| party.first.age | First Party Age | Preamble | number | SOURCE_DERIVED | Yes | Required |
| party.first.citizenship.number | First Party Citizenship No. | Preamble | string | SOURCE_DERIVED | Conditional | Required |
| party.first.citizenship.issueDate | First Party Citizenship Issue Date | Preamble | date (BS) | SOURCE_DERIVED | Conditional | Required |
| party.first.citizenship.issueDistrict | First Party Citizenship Iss. District | Preamble | string | SOURCE_DERIVED | Conditional | Required |
| party.second.name | Second Party Full Name | Preamble | string | SOURCE_DERIVED | Yes | Required |
| party.second.grandfather | Second Party Grandfather | Preamble | string | SOURCE_DERIVED | Likely | Required |
| party.second.father | Second Party Father | Preamble | string | SOURCE_DERIVED | Yes | Required |
| party.second.address.district | Second Party District | Preamble | string | SOURCE_DERIVED | Yes | Required |
| party.second.address.municipality | Second Party Municipality | Preamble | string | SOURCE_DERIVED | Yes | Required |
| party.second.address.ward | Second Party Ward | Preamble | string/number | SOURCE_DERIVED | Yes | Required |
| party.second.age | Second Party Age | Preamble | number | SOURCE_DERIVED | Yes | Required |
| party.second.citizenship.number | Second Party Citizenship No. | Preamble | string | SOURCE_DERIVED | Conditional | Required |
| party.second.citizenship.issueDate | Second Party Citizenship Issue Date | Preamble | date (BS) | SOURCE_DERIVED | Conditional | Required |
| party.second.citizenship.issueDistrict | Second Party Citizenship Iss. District | Preamble | string | SOURCE_DERIVED | Conditional | Required |
| party.second.company.name | Second Party Company Name | Preamble | string | SOURCE_DERIVED | Conditional | Required |
| party.second.company.registrationNo | Second Party Co. Reg. Number | Preamble | string | SOURCE_DERIVED | Conditional | Required |
| party.second.company.registrationDate | Second Party Co. Reg. Date | Preamble | date | SOURCE_DERIVED | Conditional | Required |
| party.second.company.proprietor | Second Party Co. Proprietor | Preamble | string | SOURCE_DERIVED | Conditional | Required |
| property.district | Property District | Clause 1 | string | SOURCE_DERIVED | Yes | Required |
| property.ward | Property Ward | Clause 1 | string | SOURCE_DERIVED | Yes | Required |
| property.kittaNumber[] | Kitta Number(s) | Clause 1 | string[] | SOURCE_DERIVED | Yes | Required |
| property.area.ropani | Area — Ropani | Clause 1 | number | SOURCE_DERIVED | Yes | Required |
| property.area.anna | Area — Anna | Clause 1 | number | SOURCE_DERIVED | Yes | Required |
| property.area.paisa | Area — Paisa | Clause 1 | number | SOURCE_DERIVED | Yes | Required |
| property.area.dam | Area — Dam | Clause 1 | number | SOURCE_DERIVED | Yes | Required |
| property.usePurpose | Use Purpose | Clause 1 | string | USER_PROVIDED | Yes | Not required |
| rent.amount | Rent Amount (Figures) | Clause 2 | number (NPR) | USER_PROVIDED | Yes | Required |
| rent.amountWords | Rent Amount (Words) | Clause 2 | string | CALCULATED | Yes | Required |
| rent.period | Rent Period (monthly/annual) | Clause 2 | string | USER_PROVIDED | Yes | Required |
| rent.escalation.rate | Escalation Rate (%) | Clause 2 | number | USER_PROVIDED | Yes | Required |
| rent.escalation.period | Escalation Period | Clause 2 | string | USER_PROVIDED | Yes | Required |
| rent.paymentTiming | Payment Timing (advance/etc) | Clause 2 | string | USER_PROVIDED | Yes | Required |
| term.durationYears | Term Duration (years) | Clause 1 | number | USER_PROVIDED | Yes | Required |
| term.noticeDays | Notice Period (days) | Various | number | USER_PROVIDED | Yes | Required |
| witness[N].name | Witness N Name | Witness Section | string | USER_PROVIDED | Yes | Required |
| witness[N].address | Witness N Address | Witness Section | string | USER_PROVIDED | Yes | Required |
| witness[N].age | Witness N Age | Witness Section | number | USER_PROVIDED | Yes | Required |
| writer.name | Writer Name | Writer Section | string | USER_PROVIDED | Yes | Not required |
| date.year | Date — BS Year | Date Section | number (BS) | SYSTEM_GENERATED | Yes | Not required |
| date.month | Date — BS Month Name | Date Section | string (Nepali) | SYSTEM_GENERATED | Yes | Not required |
| date.day | Date — BS Day | Date Section | number | SYSTEM_GENERATED | Yes | Not required |
| date.weekday | Date — BS Weekday (रोज) | Date Section | number (1-7) | SYSTEM_GENERATED | Yes | Not required |
| case.id | Case Identifier | Header/Footer | string | SYSTEM_GENERATED | Yes | Not required |


## 14. Template Generation Requirements

### 14.1 Required Generation Capabilities

Based on template analysis, the document generation system must support:

| Capability | Required? | Evidence |
|---|---|---|
| **Variable replacement in body text** | YES | All filled fields in preamble and clauses |
| **Repeated party sections** | YES | Multiple co-owners in first party |
| **Repeated witness sections** | YES | 1–3 witnesses |
| **Conditional clauses** | YES | Agriculture vs business clauses differ |
| **Calculated values** | YES | Rent amount in words, escalation amounts |
| **Date formatting — BS calendar** | YES | इतिसम्बत YYYY महिना MMMM GG गते रोज N |
| **Number formatting — Nepali words** | YES | अक्षेरुपिय पैसाठी हजार रुपैया |
| **Nepali numerals** | YES | Area in Ropani/Anna/Paisa/Dam format |
| **Mixed Devanagari and Latin text** | YES | Amount figures use both systems |
| **Signature areas** | YES | प्रथम पक्ष / दोश्रो पक्ष with names |
| **Fixed formatting / layout** | YES | Consistent structure across all examples |
| **Tables** | No | Not observed; numbered list format only |
| **Page breaks** | Unlikely | Single-page agreement per instance |
| **Nepali-english mixed text** | YES | "रु ६५,०००/- (अक्षेरुपिय पैसाठी हजार रुपैया)" |

### 14.2 Conditional Generation Logic

The system should conditionally include/exclude content based on:

| Condition | Affects |
|---|---|
| `property.usePurpose === "agriculture"` | Add agriculture-specific clauses (prohibited crops, soil restoration) |
| `property.usePurpose === "business"` | Add business clauses (infrastructure, tax responsibilities) |
| `rent.period === "monthly"` | Generate monthly rent amount; do not generate annual rent clause |
| `rent.period === "annual"` | Generate annual rent amount; do not generate monthly rent clause |
| `party.second.company` is present | Include company registration details in preamble |
| Multiple kitta numbers | Repeat property reference in clause |
| Multiple first party individuals | Repeat signature block section and preamble lineage entries |


## 15. Open Questions

### A. Domain Workflow Questions

| ID | Question |
|---|---|
| OQ-TA-01 | What is the actual process for determining which clauses to include? Is it purely based on use purpose, or are there other drivers? |
| OQ-TA-02 | Are there multiple versions of this template in actual use, or is this single template representative? |
| OQ-TA-03 | What determines the number of witnesses? Is there a legal minimum requirement? |
| OQ-TA-04 | Are the grandfather/father lineage fields always required, or can they be omitted in some cases? |
| OQ-TA-05 | Is the writer/लेखक always specified, or can this be optional? |
| OQ-TA-06 | Are there different templates for residential vs commercial vs agricultural leases? Or are clauses selected from a single template? |

### B. User Workflow Questions

| ID | Question |
|---|---|
| OQ-TA-07 | Does the operator typically type the agreement from scratch, modify an existing file, or fill in a template? |
| OQ-TA-08 | Which fields does the operator typically copy from source documents versus ask the client? |
| OQ-TA-09 | How does the operator handle the "words" version of the rent amount? Is it manually typed or calculated? |
| OQ-TA-10 | Who typically acts as witnesses? Are they present during document creation or named later? |

### C. Legal / Regulatory Questions

| ID | Question |
|---|---|
| OQ-TA-11 | Does the generated document need to match this exact format, or are variations acceptable? |
| OQ-TA-12 | Are there any legally mandated minimum or maximum values (rent, duration, notice period) that should be enforced? |
| OQ-TA-13 | Is the citizenship number required in the document, or is it optional? What about citizenship issue date? |
| OQ-TA-14 | Does the law require a specific number of witnesses? |
| OQ-TA-15 | Is the company registration format observed (०७७/०७८) standard, or was it instance-specific? |
| OQ-TA-16 | Are Bikram Sambat dates legally required, or are AD dates also acceptable? |

### D. Data Questions

| ID | Question |
|---|---|
| OQ-TA-17 | Should the system store the area in structured Ropani-Anna-Paisa-Dam fields or as a single text string? |
| OQ-TA-18 | Should the system support both Ropani and Square Meter area systems? |
| OQ-TA-19 | Should addresses be stored as structured fields (district/municipality/ward) or as free text? |
| OQ-TA-20 | What is the complete list of possible use purposes? |

### E. Template Questions

| ID | Question |
|---|---|
| OQ-TA-21 | Is the template structure identical for all rental scenarios, or do different property types have different templates? |
| OQ-TA-22 | Are there templates for month-to-month or indefinite-term rentals (not just fixed-year terms)? |
| OQ-TA-23 | Is the "Palpatory/Chakravriddhi" (compound escalation) wording standard, or are there other escalation methods? |

### F. OCR / Automation Questions

| ID | Question |
|---|---|
| OQ-TA-24 | How legible are typical citizenship certificates and Lalpurja for OCR purposes? |
| OQ-TA-25 | Would OCR of Nepali Devanagari text on these documents be sufficiently accurate? |
| OQ-TA-26 | Are source documents typically printed, handwritten, or mixed? |

### G. Storage / Retention Questions

| ID | Question |
|---|---|
| OQ-TA-27 | Does the operator need to retain copies of the source documents (citizenship, Lalpurja) with the finalized agreement? |
| OQ-TA-28 | Is the finalized agreement printed for signatures, or is it signed digitally? |


## 16. Template-to-SRS Gap Analysis

### 16.1 Implications for SRS

This section identifies where the current SRS v0.1 aligns with, falls short of, or differs from the actual template.

#### A. SRS Requirements Confirmed by Template Evidence

| Finding | SRS Section | Template Evidence | Recommendation | Priority |
|---|---|---|---|---|
| Case-based workflow confirmed | FR-004–FR-008 | Each agreement is a distinct case with parties, property, terms | Continue as-is | Medium |
| Human verification required for party data | FR-016, Human Authority Principle | Birthdates, citizenship numbers, and property IDs are critical | Continue as-is; this is well-supported | High |
| Document generation from verified data | FR-021, DG-001 | Template has structured variable fields | Continue as-is | High |
| Template-based generation approach | FR-023, DG-001 | Consistent structure across all 7 instances confirms template approach | Continue as-is | High |
| Nepali language requirement | FR-022, DG-002 | All documents entirely in Nepali (Devanagari) | Confirmed — no change needed | High |
| Fixed + Variable template structure | FR-023 | Existing templates have clear fixed preamble + variable fields | Continue as-is | Medium |
| Source document capture required | FR-009–FR-012 | Citizenship and Lalpurja are primary source documents | Continue as-is | Medium |

#### B. SRS Requirements That Appear Incomplete

| Finding | SRS Section | Template Evidence | Recommendation | Priority |
|---|---|---|---|---|
| Ropani-Anna-Paisa-Dam area format not addressed | 9.3 Data Requirements | Template uses R-A-P-D format (0-0-0-0) | Add area format to data requirements | High |
| Bikram Sambat date handling not specified | 7.9, 9.11 | All dates are BS calendar | Add BS date support requirement | High |
| Party lineage (grandfather/father) not included in SRS | 9.4 Party Information | Every instance has grandfather → father → name lineage | Add lineage fields to party data | High |
| Multiple co-owners not addressed | 9.4 | One instance has 3 co-owners as first party | Add multi-party support to data model | Medium |
| Company as tenant not addressed | 9.4 | One instance has company with registration as tenant | Add entity-type party variant | Medium |
| Conditional clauses not detailed | FR-024 | Agriculture vs business clauses differ | Expand conditional content requirements | Medium |
| Escalation calculation not addressed | 9.5 Rental Terms | Compound escalation with varying periods | Add escalation model to requirements | Medium |

#### C. SRS Requirements That May Be Too Broad

| Finding | SRS Section | Template Evidence | Recommendation | Priority |
|---|---|---|---|---|
| "Land-rent document" may need sub-typing | 2.3 Scope | Agriculture vs business use affects clauses significantly | Consider adding use-purpose variant | Medium |
| "Source document types" too vague | FR-011 | Primary types evident: Citizenship, Lalpurja, Company Reg | Add specific source doc types to requirements | Medium |

#### D. SRS Requirements That May Be Unnecessary

| Finding | SRS Section | Template Evidence | Recommendation | Priority |
|---|---|---|---|---|
| "Document classification" (auto) | 7.4 | Only one document type exists in template | Reaffirm that auto-classification is not needed for MVP | Low |

#### E. New Requirements Suggested by the Template

| Finding | SRS Section | Template Evidence | Recommendation | Priority |
|---|---|---|---|---|
| BS date handling | New requirement | All dates in Bikram Sambat with month names and रोज | Add BS calendar support requirement | High |
| Number-to-Nepali-words conversion | New requirement | Rent amount always written in words after figures | Add Nepali words conversion for amounts | High |
| Conditional clause selection based on use purpose | FR-024 expansion | Different clauses for agriculture vs business | Expand FR-024 with use-purpose conditions | High |
| Multi-party (co-owner) support | New / Data model | 3 co-owners as first party | Add repeated party section support | Medium |
| Company/entity party support | New / Data model | Company with registration as tenant | Add entity party variant | Medium |
| Notice period as variable field | New | Varies across instances (30, 60 days, 3, 6 months) | Add notice period as explicit variable | Medium |
| Witness data fields structured | New | Witness name, address, age documented | Add witness data structure | Medium |
| Writer/scribe identification field | New | लेखक/मसौदाकार with optional license number | Add writer field to data model | Low |
| Ropani-Anna-Paisa-Dam structured area | New / Data model | Area format is structured R-A-P-D | Add R-A-P-D field structure | High |

#### F. New Open Questions for SRS

See Section 15 (Open Questions) above — all 28 OQ-TA questions should be considered for inclusion in the SRS.

#### G. Existing SRS Assumptions Requiring Validation

| SRS Assumption | Status | Template Evidence |
|---|---|---|
| AS-001: Users are notary/document-prep professionals | [TO BE VALIDATED] | Writer with license number "प्र.प.नं. ३४६" suggests professional scribe registration |
| AS-002: Currently prepared with word processors | [TO BE VALIDATED] | PDF created with Google Docs ("Skia/PDF m152 Google Docs Renderer") confirms digital authoring |
| AS-007: Template has stable structure | [TO BE VALIDATED] | Highly consistent across all 7 instances — assumption appears well-founded |
| AS-009: Manual workflow follows Section 3.2 pattern | [TO BE VALIDATED] | Template structure aligns with hypothesized workflow |

#### H. Potential Contradictions

| Finding | SRS | Template | Resolution |
|---|---|---|---|
| Number of witnesses | BR-008 claims minimum 2 witnesses per party | Template shows 1–3 witnesses total (not per party) | BR-008 is already [UNVERIFIED — CANDIDATE DOMAIN RULE]; template evidence doesn't confirm the "per party" requirement |
| Rent threshold for written agreement | BR-009 NPR 20,000 threshold | Template shows instances with रु ५,५०० (below threshold) | BR-009 candidate rule already correctly marked as unverified |
| Registration threshold | BR-010 NPR 500,000 / 10 years | Template shows 10-year term in one instance | Template alone cannot confirm or deny this requirement |


## 17. Summary

### 17.1 Key Findings

| Metric | Count |
|---|---|
| **Files Analyzed** | 1 PDF (`Land Rent - WIP.pdf`), 1 SRS (`SRS.md`) |
| **Template Instances in Document** | 7 filled-in examples (6 complete, 1 partially blank) |
| **Document Structure** | 8 logical sections (title, preamble, clauses, signatures × 2, witnesses, writer, date) |
| **Variable Fields Identified** | ~45 distinct fields |
| **Static Content Blocks** | ~12 confirmed static elements |
| **Conditional Sections** | ~4 substantive conditionals (use purpose, multi-party, company party, guthi land) |
| **Potential Source-Derived Fields** | ~20 (party identity, citizenship, property) |
| **User-Provided Fields** | ~10 (rent, term, purpose, notice, witnesses) |
| **Calculated Fields** | ~2 (rent words, escalation) |
| **System-Generated Fields** | ~3 (date, case ID, template version) |

### 17.2 Major Unknowns

1. Whether the exact set of conditional clauses and their triggers is fully captured
2. Whether the lineage (grandfather/father) format is legally required or customary
3. Whether company-as-tenant is common or rare
4. Whether a single operator typically types agreements for both parties or represents one side
5. Whether the template covers all rental scenarios or only fixed-term land leases
6. Whether digital signatures or only physical signatures are used

### 17.3 Major Implications for the SRS

1. **BS calendar support** must be added as a requirement
2. **Ropani-Anna-Paisa-Dam area format** must be added to data requirements
3. **Party lineage** (grandfather/father) must be added to party information
4. **Multi-party support** (co-owners) must be addressed in data model
5. **Company/entity party variant** must be supported
6. **Use-purpose-driven conditional clauses** must be explicitly modeled
7. **Nepali words generation for amounts** is required
8. **Notice period** should be an explicit variable field
9. **Witness data** should be structured

### 17.4 Recommended Next Steps

1. **Validate template analysis** with domain experts (project owner's parents) — confirm structure, clauses, and field requirements
2. **Update SRS** to incorporate findings — add BS calendar, R-A-P-D area, party lineage, multi-party support
3. **Expand conditional content model** — determine exact clause selection rules per use purpose
4. **Design template variable model** — convert proposed variable names to structured template format
5. **Research BS date handling** — determine if BS-to-AD conversion or BS-only is needed
6. **Analyze additional templates** — if other rental document variants exist, analyze those as well
