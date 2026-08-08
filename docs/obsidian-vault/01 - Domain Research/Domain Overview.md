# Domain Overview — Nepali Land Documentation

**Status:** Living Document — Phase 0.2 Domain Research  
**Last Updated:** 2026-07-27  
**Next Review:** After stakeholder/expert feedback

---

## 1. Purpose of Domain Research

The Nepal Land Document Assistant project aims to build a mobile-first application that assists users with preparing land- and property-related documents in Nepal. Before any software requirements can be written or technical architectures proposed, the real-world domain must be understood on its own terms.

Domain research serves these objectives:

- **Establish what is known**: Identify documented processes, document types, stakeholders, and government bodies from publicly available sources.
- **Establish what is unknown**: Explicitly mark gaps, ambiguities, and uncertainties that require further investigation.
- **Separate fact from assumption**: Distinguish information supported by sources from inferences or hypotheses.
- **Prevent premature requirements**: Avoid converting domain observations directly into software features without understanding domain constraints.
- **Inform scope decisions**: Provide the project team with enough domain knowledge to make informed decisions about what the system should and should not do.

This document does not define software requirements. It does not propose architecture. It does not select technology.

---

## 2. Project Domain Scope

The application is conceived as a mobile-first tool to assist users with land/property document preparation in Nepal. The following describes the domain scope at this research stage.

### 2.1 Confirmed Scope (from project concept)

- Land rent / lease documentation
- Land sale / trade documentation
- Land transfer documentation
- Supporting property and identity documentation
- Document preparation assistance
- Document information extraction (from source document photographs)

### 2.2 Potential Scope

- OCR-based capture of text from source documents (Nepali/Devanagari script)
- User verification and correction of extracted information
- Structured information management (storage, retrieval, organization)
- Document generation in Nepali language
- Support for multiple document types (beyond the initial three transaction types)
- Document printing or export

### 2.3 Scope Requiring Further Investigation

- Whether the system should store or transmit documents to government systems
- Whether the system should interact with Land Revenue Office (Malpot) systems
- Whether identity verification or authentication is needed beyond user self-identification
- Whether the system should support offline operation in areas with limited connectivity
- Whether the system should support Non-Resident Nepali (NRN) users
- Whether the system should assist with document translation (Nepali to English or vice versa)
- Whether document templates must conform to government-mandated formats
- The extent to which handwritten text on documents must be processed

---

## 3. Land and Property Documentation Context

The following document types are relevant to the project's intended use cases. Information is sourced from publicly available guides and legal references. Each document's relevance to the application is noted.

### 3.1 Lalpurja (Land Ownership Certificate)

| Attribute | Description |
|---|---|
| **Document Name** | Lalpurja (लालपुर्जा) — formally known as "Field Book" or Certificate of Ownership |
| **Purpose** | Official government record of land ownership. Constitutes the primary proof of who owns a specific parcel of land. Issued by the District Land Revenue Office. |
| **Information Typically Contained** | Owner's name, plot (kitta) number, land area, location, boundaries, land classification, survey details |
| **Relevant Transaction Types** | All types — sale, purchase, inheritance, gift, partition, mortgage |
| **Issuing Authority** | District Land Revenue Office (Malpot Karyalaya) |
| **Types** | Individual Lalpurja, Joint Lalpurja (Amsha Patta), Guthi/Organisation Land, Government Land (Ainsh) |
| **Application Relevance** | The system may need to capture/extract information from this document during sale, transfer, or rental workflows. It is the foundational ownership document. |
| **Source** | basobaas.com, punarvaasunepal.com, courtmarriageinnepal.com |

### 3.2 Napi Naksha (Land Parcel / Survey Map)

| Attribute | Description |
|---|---|
| **Document Name** | Napi Naksha (नापी नक्सा) / Field Book |
| **Purpose** | Official cadastral survey map showing land parcel boundaries, dimensions, and location |
| **Information Typically Contained** | Plot boundaries, kitta number, adjacent plots, area measurements, survey control points |
| **Relevant Transaction Types** | Sale, purchase, land transfer, boundary disputes, mortgage |
| **Issuing Authority** | Survey Office (Napi Karyalaya) under the Department of Survey |
| **Application Relevance** | May need to be referenced during transactions. The system is unlikely to extract information from a map image, but may need to reference kitta numbers and parcel details. |
| **Source** | dos.gov.np, punarvaasunepal.com |

### 3.3 Rajinama (Transfer Deed / Sale Deed)

| Attribute | Description |
|---|---|
| **Document Name** | Rajinama (राजिनामा) |
| **Purpose** | The official deed executed at the Land Revenue Office that formally records the transfer of ownership from seller to buyer |
| **Information Typically Contained** | Parties' details, property description, sale price, terms, signatures, witness information |
| **Relevant Transaction Types** | Sale, purchase |
| **Issuing Authority** | Land Revenue Office (Malpot Karyalaya), executed in the presence of staff |
| **Application Relevance** | The system may assist in preparing this document for presentation at the Land Revenue Office. **Requires Verification**: Whether this document must be prepared on government-specified paper/format. |
| **Source** | courtmarriageinnepal.com, basobaas.com, aafnaighar.com |

### 3.4 Baikalpatra / Bainapatra (Preliminary Sale Agreement)

| Attribute | Description |
|---|---|
| **Document Name** | Baikalpatra (बैकल्पत्र) or Bainapatra (बैनापत्र) |
| **Purpose** | A preliminary agreement between buyer and seller specifying the agreed price, advance payment (typically 10–20%), and completion timeline. Not strictly legally mandatory but serves as evidence of the agreement. |
| **Information Typically Contained** | Parties' details, property description, agreed price, advance payment amount, timeline, terms |
| **Relevant Transaction Types** | Sale, purchase |
| **Application Relevance** | The system may assist in preparing this document. |
| **Source** | courtmarriageinnepal.com, aafnaighar.com |

### 3.5 Lease / Rental Agreement

| Attribute | Description |
|---|---|
| **Document Name** | Bhadā Samjhautā (भाडा सम्झौता) / Lease Agreement |
| **Purpose** | Legally binding contract between landlord (lessor) and tenant (lessee) defining terms of property use |
| **Information Typically Contained** | Property details, rent amount and payment schedule, duration of tenancy, rights and obligations, witness signatures, citizenship information of both parties |
| **Relevant Transaction Types** | Land rent / lease, house rent |
| **Application Relevance** | High relevance. This is a core document type the system may assist in preparing. |
| **Legal Threshold** | Written agreement mandatory when monthly rent exceeds NPR 20,000 (Section 386, Muluki Civil Code). Registration at Land Revenue Office required when annual rent exceeds NPR 500,000 or lease exceeds 10 years. |
| **Witness Requirement** | Minimum two witnesses per party (Section 386, Muluki Civil Code) |
| **Source** | commonlaw.com.np, notarykathmandu.com, lawimperial.com |

### 3.6 Ghar Bato Sifaris (Ward Office Recommendation Letter)

| Attribute | Description |
|---|---|
| **Document Name** | Ghar Bato Sifaris (घर बाटो सिफारिस) |
| **Purpose** | Recommendation letter from the local ward office evaluating the property's characteristics (road access, location, etc.). Required for property registration. |
| **Relevant Transaction Types** | Sale, property registration |
| **Application Relevance** | Low direct relevance. The system is unlikely to generate this as it requires ward office evaluation. May need to inform users about this requirement. |
| **Source** | aafnaighar.com |

### 3.7 Tax Clearance Certificate (Malpot Tiro / Sampati Kar)

| Attribute | Description |
|---|---|
| **Document Name** | Tax Clearance Certificate / Tiro Rasid (तिरो रसिद) |
| **Purpose** | Proof that all land/property taxes have been paid up to date. Required before any property transaction can be registered. |
| **Relevant Transaction Types** | All — sale, purchase, inheritance, transfer |
| **Issuing Authority** | Local municipality / rural municipality (for property tax) or Land Revenue Office (for malpot tax) |
| **Application Relevance** | The system may need to inform users that this must be obtained before a transaction. Not a document the system would generate. |
| **Source** | courtmarriageinnepal.com, attorneynepal.com |

### 3.8 Citizenship Certificate (Nagarikta Praman Patra)

| Attribute | Description |
|---|---|
| **Document Name** | Nagarikta Praman-Patra (नागरिकता प्रमाण-पत्र) |
| **Purpose** | Foundational proof of Nepali nationality and identity. Required for virtually all property transactions, land registration, and legal agreements. |
| **Information Typically Contained** | Full name, date of birth, place of birth, parent/ spouse details, photograph, citizenship number |
| **Issuing Authority** | District Administration Office (DAO) |
| **Application Relevance** | High. The system may need to capture/extract identity information from this document during user onboarding or document preparation workflows. Is the primary identity document used in Nepal. |
| **Types** | By Descent (Bansaj), By Birth (closed category), Naturalized (Angikrit), NRN Citizenship |
| **Source** | notarynepal.com, unionnepal.com |

### 3.9 National Identity Card (Rastriya Parichaya Patra / NID)

| Attribute | Description |
|---|---|
| **Document Name** | Rastriya Parichaya Patra (राष्ट्रिय परिचय पत्र) |
| **Purpose** | Biometric digital identity card issued by the Department of National ID and Civil Registration (DoNIDCR). Increasingly used for service delivery. Recommended but not yet mandatory for land registration. |
| **Application Relevance** | May become relevant as the system develops. Currently secondary to the citizenship certificate. |
| **Source** | notarykathmandu.com, lawalpine.com |

### 3.10 Other Relevant Documents

| Document | Relevance |
|---|---|
| **Power of Attorney (Mukhtyarnama / Adhikar Patra)** | Required when one party cannot be present for a transaction. Notarised. The system may assist in preparing this. |
| **Partition Deed (Ansha Banda / Banda Patra)** | Required for division of family or ancestral property among co-parceners. Relevant for inheritance workflows. |
| **Relationship Certificate (Nata Pramanit)** | Required for inheritance and family-related land transfers. |
| **Death Certificate** | Required for inheritance/succession transfers. |
| **Will (Sheshpachhiko Bakaspatra)** | Relevant to succession and inheritance. The system may potentially assist with will preparation. |
| **Land Tax Receipt (Tiro Rasid)** | Proof of annual land revenue tax payment. Required for transactions. |

**Source for legal-heir / relationship document requirements:** toolspasal.com, notarynepal.com, courtmarriageinnepal.com.np

---

## 4. Transaction Types

### 4.1 Land Rent / Lease

#### What the Transaction Represents

A land or property lease is a contractual agreement where the owner (lessor) grants the tenant (lessee) the right to use a property for a specified period in exchange for rent. Residential leases in Nepal are governed by the House Rent Control Act 2048 (1992) and the Muluki Civil Code 2074 (2017). Land lease may be for agricultural, commercial, or residential purposes.

#### Parties Involved

- **Lessor (Landlord / Property Owner)**: The legal owner of the property
- **Lessee (Tenant)**: The person or entity renting the property
- **Witnesses**: Minimum two per party (required by Section 386 of Muluki Civil Code)
- **Notary / Advocate**: May be involved for notarisation of the agreement
- **Ward Office**: For registration of the agreement
- **Land Revenue Office (Malpot)**: For registration of high-value or long-term leases

#### Typical Workflow

1. Parties negotiate terms (rent, duration, conditions)
2. Agreement is drafted (may be done by parties, lawyer, or deed writer)
3. Agreement is signed by both parties with witnesses (minimum two per party)
4. Agreement is notarised (recommended for enforceability but not mandatory for all cases)
5. Agreement is registered at Ward Office (recommended)
6. Registration at Land Revenue Office if annual rent exceeds NPR 500,000 or lease exceeds 10 years

**Source:** notarykathmandu.com, commonlaw.com.np, lawimperial.com

#### Relevant Documents

- Lease / Rental Agreement (primary document)
- Citizenship certificates of both parties
- Lalpurja (to prove ownership)
- Witness identification documents

#### Government / Administrative Involvement

- **Ward Office**: Registration of agreement
- **Land Revenue Office**: Registration for high-value/long-term leases
- **Municipality**: Tax collection on rental income
- **Inland Revenue Department**: Rental income tax

#### Where Document Preparation Occurs

Agreements are typically drafted by the parties themselves, by a lawyer, or by a document writer (lekhandas). The project's application could assist in this preparation step.

#### Remaining Uncertainty

- The extent to which rental agreement templates are standardised vs. freely negotiated
- Whether the system should handle residential lease, agricultural land lease, commercial lease, or all three
- The specific format requirements for Ward Office registration

---

### 4.2 Land Sale / Trade

#### What the Transaction Represents

A land sale is the transfer of ownership of a land parcel from a seller to a buyer in exchange for payment. This is the most formal and heavily regulated of the three transaction types. Under the Land Act 2021 (1964) and Land Revenue Act 2034 (1978), ownership is not legally transferred until the transaction is registered at the District Land Revenue Office.

#### Parties Involved

- **Seller**: The current registered owner(s) of the land
- **Buyer**: The person or entity acquiring the land
- **Witnesses**: Required for deed execution
- **Lawyer / Legal Professional**: Often engaged for due diligence and deed drafting (recommended but not legally required)
- **Land Revenue Office (Malpot) Staff**: Verify documents and execute the transfer
- **Survey Office (Napi) Staff**: Verify maps and boundaries
- **Ward Office**: Issue tax clearance and recommendation letter
- **Notary Public**: May notarise documents

#### Typical Workflow

1. **Negotiation**: Buyer and seller negotiate price and terms
2. **Due Diligence (Sampatti Janch)**:
   - Verify Lalpurja at Malpot Office
   - Check for encumbrances (jagga rokka) — mortgages, court orders, restrictions
   - Verify survey map (Napi Naksha) at Survey Office
   - Confirm tax status at municipality
   - Check ownership history
   - Physical inspection of property
3. **Preliminary Agreement**: Baikalpatra/Bainapatra signed with advance payment (typically 10–20%)
4. **Obtain Documents**:
   - Tax clearance certificate from municipality
   - Ghar Bato Sifaris from ward office (if required)
5. **Visit Land Revenue Office**: Both parties appear in person with all documents
6. **Valuation**: Government assesses minimum valuation (nyunatam mulya)
7. **Fee Payment**:
   - Buyer pays registration fee (typically 4–6% of value)
   - Seller pays capital gains tax (5–7.5% of gain depending on holding period)
8. **Deed Execution**: Rajinama prepared and signed in presence of Malpot staff
9. **New Lalpurja Issued**: Issued in buyer's name

**Sources:** aafnaighar.com, courtmarriageinnepal.com, basobaas.com, nepallegalfirm.com.np, nepallawyer.com

#### Relevant Documents

- Lalpurja (original)
- Citizenship certificates (buyer and seller)
- Tax clearance certificate
- Survey map (Napi Naksha)
- Baikalpatra (if advance agreement was signed)
- Passport-size photographs (4 copies per party)
- PAN card (for transactions above NPR 5 lakh)
- Consent from co-owners (if joint ownership)
- Family partition deed (if selling inherited land)

#### Government / Administrative Involvement

- **Land Revenue Office (Malpot)**: Central authority — handles verification, valuation, deed execution, and Lalpurja issuance
- **Survey Office (Napi)**: Map/boundary verification
- **Municipality / Ward Office**: Tax clearance, recommendation letter
- **Inland Revenue Department**: Capital gains tax collection
- **Designated Banks**: Fee payment collection

#### Where Document Preparation Occurs

The sale deed (Rajinama) is typically prepared by a lawyer or deed writer (lekhandas). The preliminary agreement (Baikalpatra) may be drafted by the parties or a lawyer. The project's application could potentially assist with:
- Preparing the Baikalpatra
- Organizing document checklists
- Preparing the Rajinama (requires verification of format requirements)

#### Remaining Uncertainty

- Whether the Rajinama format is prescribed by the Land Revenue Office or can be freely drafted
- Whether digital preparation of documents is accepted by Malpot offices
- The extent of digital systems in different district Malpot offices

---

### 4.3 Land Transfer (Inheritance / Succession / Gift)

#### What the Transaction Represents

Land transfer covers the change of ownership through means other than a commercial sale. This includes:

- **Inheritance (Succession)**: Transfer of property from a deceased person to their legal heirs under the Muluki Civil Code 2074, Chapter 11
- **Gift Transfer (Dan Bakaspatra)**: Voluntary transfer of property without financial consideration
- **Partition (Ansha Banda)**: Division of jointly held family property among co-parceners
- **Family Transfer**: Transfer between family members at concessional rates

#### Parties Involved

- **Transferor (Donor / Deceased's Estate)**: The person transferring or the estate of the deceased
- **Transferee (Heir / Donee)**: The recipient
- **Co-heirs**: Other legal heirs who must consent (in inheritance cases)
- **Lawyer**: May assist with documentation
- **Land Revenue Office (Malpot)**: Processes the transfer
- **Ward Office**: Issues relationship certificates as needed

#### Typical Workflow (Inheritance)

1. Death registration obtained
2. Legal heirs identified per Muluki Civil Code 2074, Chapter 11
3. Relationship certificates (Nata Pramanit) obtained from ward office
4. Consent/no-objection obtained from other heirs
5. Application submitted to Land Revenue Office with:
   - Original Lalpurja
   - Death certificate
   - Legal-heir certificate / relationship certificates
   - Citizenship certificates of all heirs
6. Concessional registration fee paid (typically 0.5–1% vs. 4% for sale)
7. Ownership transferred (Dakhil Kharij — mutation process)

**Sources:** notarynepal.com, courtmarriageinnepal.com.np, mijarlawassociates.com.np, nepalrepublic.org

#### Relevant Documents

- Lalpurja (original)
- Death certificate (for inheritance)
- Legal-heir certificate / heir list
- Relationship certificates for all heirs
- Citizenship certificates of all heirs
- Partition deed (if dividing among co-heirs)
- Consent/no-objection letters from co-heirs

#### Government / Administrative Involvement

- **Land Revenue Office**: Processes the transfer/mutation
- **Ward Office**: Issues relationship certificates, death registration
- **District Administration Office**: Issues some legal-heir documents

#### Where Document Preparation Occurs

Legal-heir documents and relationship certificates are obtained from ward offices. The transfer application is prepared for submission to Malpot. The project's application may assist with:
- Preparing document checklists
- Drafting consent letters
- Organizing required documentation

#### Remaining Uncertainty

- Whether the system should handle inheritance transfers given the complexity of heir identification
- Whether the system should assist with partition deed preparation
- The role of legal professionals in inheritance transfers and whether the system should recommend professional assistance

---

## 5. Stakeholders

### 5.1 Primary Stakeholders (Potential Direct Users)

| Stakeholder | Real-World Role | Application Relationship |
|---|---|---|
| **Property Owner / Landlord** | Owns land or property. May want to sell, lease, or transfer. | Likely direct user — may use the app to prepare sale agreements, rental agreements, or transfer documents. |
| **Tenant / Lessee** | Rents property from an owner. | Likely direct user — may use the app to prepare or review rental agreements. |
| **Buyer** | Purchasing land or property. | Likely direct user — may use the app for due diligence checklists, document preparation, and transaction tracking. |
| **Seller** | Selling land or property. | Likely direct user — may use the app to prepare sale agreements and organize transaction documents. |
| **Heir / Successor** | Receiving property through inheritance. | Potential direct user — may use the app to understand inheritance documentation requirements and prepare paperwork. |

### 5.2 Secondary Stakeholders (Indirect Users / Influencers)

| Stakeholder | Real-World Role | Application Relationship |
|---|---|---|
| **Family Members / Co-owners** | May have joint ownership or inheritance rights. Must consent to transactions. | Indirect stakeholders — their consent may be required within the workflow. The system may need to capture their information. |
| **Witnesses** | Required to sign agreements (minimum two per party for rental agreements). | Indirect — the system may need to record witness details and make space for signatures. Not likely to be direct users. |
| **Lawyers / Legal Professionals** | Advise clients on property transactions, draft deeds, conduct due diligence. | Indirect — may use the system as a tool to organise documents. Could also be a channel partner. **Requires domain expert verification** on whether lawyers would adopt such a tool. |
| **Document Writers (Lekhandas / Lekhapadhibyabasayi)** | Traditional document writers who draft deeds and agreements in Nepal. | Important indirect stakeholders. The system may partially or fully replace some of their current role in document preparation. Their role in land administration is noted in academic sources as not clearly defined under law. |
| **Notary Public** | Notarises documents, verifies identities and signatures. | Indirect — processed documents may require notarisation. Partnership potential. |

### 5.3 External Authorities (Not Users)

| Stakeholder | Real-World Role | Application Relationship |
|---|---|---|
| **Land Revenue Office (Malpot Karyalaya)** | Government authority for land registration, ownership records, revenue collection | External authority. The system does not interact with Malpot systems directly. Produces documents that are presented at Malpot. |
| **Survey Office (Napi Karyalaya)** | Maintains cadastral maps and survey records | External authority. Users may need survey information to complete documents. |
| **Municipality / Ward Office** | Issues tax clearance, recommendation letters, relationship certificates | External authority. Documents from these offices are inputs to the workflows. |
| **District Administration Office (DAO)** | Issues citizenship certificates, some legal documents | External authority. Source of identity documents. |
| **Inland Revenue Department** | Collects capital gains tax, rental income tax | External authority. Tax obligations arise from transactions the system assists with. |
| **Department of Land Management and Archive (DOLMA)** | Oversight body for land administration | External authority. Not directly involved in individual transactions. |
| **Department of Survey (DOS)** | National mapping and survey authority | External authority. Provides map data referenced in transactions. |

---

## 6. Government and Administrative Context

### 6.1 Ministry of Land Management, Cooperatives and Poverty Alleviation

| Attribute | Description |
|---|---|
| **Name** | Ministry of Land Management, Cooperatives and Poverty Alleviation (भूमि व्यवस्था, सहकारी तथा गरिबी निवारण मन्त्रालय) |
| **Role** | The federal ministry responsible for land policy, land reform, land administration, survey, cooperatives, and poverty alleviation |
| **Relevance** | Oversees all land administration bodies in Nepal. Sets policy direction for land management. |
| **Source** | molmcpa.gov.np |

### 6.2 Department of Land Management and Archive (DOLMA)

| Attribute | Description |
|---|---|
| **Name** | Department of Land Management and Archive (भूमि व्यवस्था तथा अभिलेख विभाग) |
| **Role** | The federal department responsible for land registration, land revenue, and land record management. Oversees all District Land Revenue (Malpot) Offices. |
| **Relevance** | Administers the Land Revenue Offices where all property transactions must be registered. Land Information Management System (LIMS) digitization falls under this department. |
| **Source** | dolma.gov.np |

### 6.3 District Land Revenue Office (Malpot Karyalaya)

| Attribute | Description |
|---|---|
| **Name** | Malpot Karyalaya (मालपोत कार्यालय) / Land Revenue Office |
| **Role** | The district-level office responsible for: land registration, ownership transfer, Lalpurja issuance, land record maintenance, revenue collection, and mutation of records |
| **Relevance** | Central to all land transactions. Every district has at least one Malpot office. Users of the proposed application will be preparing documents for submission at these offices. |
| **Source** | dolma.gov.np, hamrobhumi.com |

### 6.4 Department of Survey (Napi Bibhag)

| Attribute | Description |
|---|---|
| **Name** | Department of Survey (नापी विभाग) |
| **Role** | National mapping organization responsible for cadastral surveying, land parcel mapping, and maintaining survey records |
| **Relevance** | Survey Offices (Napi Karyalaya) at district level support land administration with cadastral maps and boundary verification. The Mero Kitta portal provides some digital map services. |
| **Source** | dos.gov.np |

### 6.5 District Survey Office (Napi Karyalaya)

| Attribute | Description |
|---|---|
| **Name** | Napi Karyalaya (नापी कार्यालय) / Survey Office |
| **Role** | District-level survey office that maintains cadastral maps and survey records. Responsible for map updates, boundary verification, and providing certified land parcel maps. |
| **Relevance** | Users may need to obtain Napi Naksha (survey maps) for transactions. The system may reference these. |
| **Source** | dos.gov.np, educatenepal.com |

### 6.6 Ward Office (Wada Karyalaya)

| Attribute | Description |
|---|---|
| **Name** | Ward Office (वडा कार्यालय) |
| **Role** | Local administrative unit within municipalities/rural municipalities. Issues tax clearance certificates, Ghar Bato Sifaris, relationship certificates, and birth/death/marriage registration. |
| **Relevance** | Required for multiple documents that feed into property transactions. Users may need to visit ward offices to obtain supporting documents. |
| **Source** | aafnaighar.com, toolspasal.com |

### 6.7 District Administration Office (DAO / Jilla Prashasan Karyalaya)

| Attribute | Description |
|---|---|
| **Name** | District Administration Office (जिल्ला प्रशासन कार्यालय) |
| **Role** | Issues citizenship certificates, national identity card registration, some legal documents. Functions under the Ministry of Home Affairs. |
| **Relevance** | Source of citizenship certificates, which are required for all property transactions. |
| **Source** | notarynepal.com |

### 6.8 Municipality / Rural Municipality (Nagarpalika / Gaunpalika)

| Attribute | Description |
|---|---|
| **Name** | Nagarpalika (नगरपालिका) / Gaunpalika (गाउँपालिका) |
| **Role** | Local government bodies responsible for property tax (Sampati Kar) assessment and collection. They set local registration fee rates within their jurisdictions. |
| **Relevance** | Property tax clearance from the municipality is required before any land transaction can proceed. Rate variations across municipalities affect transaction costs. |
| **Source** | attorneynepal.com, courtmarriageinnepal.com |

### 6.9 Government Digital Services

| Service                                       | Description                                                       | URL                         |
| --------------------------------------------- | ----------------------------------------------------------------- | --------------------------- |
| **Mero Kitta**                                | Online portal for parcel map and survey information               | merokitta.dos.gov.np        |
| **Land Information Management System (LIMS)** | Digital land records system (pilot districts, not yet nationwide) | via DOLMA                   |
| **Government Revenue Portal**                 | Online tax and fee payment                                        | Portal for revenue payments |
| **DoNIDCR Portal**                            | National ID pre-enrollment                                        | via donidcr.gov.np          |

**Note:** Digital service availability varies by district. Full online registration is not yet available nationwide.

---

## 7. High-Level Real-World Workflows

### 7.1 Land Rent / Lease Workflow

```
1. Owner and tenant negotiate terms
   ├── Rent amount, duration, deposit, utilities, permitted use
   └── [Requires Verification: Common rental term lengths, renewal practices]

2. Collect required identity documents
   ├── Citizenship certificates of both parties
   └── Lalpurja (to verify ownership)

3. Draft lease agreement
   ├── Include: parties' details, property info, rent, duration, terms
   ├── Must be in writing if monthly rent > NPR 20,000
   ├── Minimum 2 witnesses per party required
   └── [Requires Verification: Standard template vs. free-form drafting]

4. Execute agreement
   ├── Both parties and witnesses sign
   ├── Notarisation (recommended, not mandatory for all)
   └── [Requires Verification: Whether digital signatures are accepted]

5. Register agreement
   ├── At Ward Office (recommended for most cases)
   ├── At Land Revenue Office if annual rent > NPR 500,000 or lease > 10 years
   └── [Requires Verification: Specific Ward Office registration procedure]

6. Ongoing obligations
   ├── Rent payment and receipts
   ├── House rent tax (owner's obligation unless agreed otherwise)
   ├── Utility payments
   └── Renewal or termination at end of term
```

### 7.2 Land Sale / Trade Workflow

```
1. Buyer identifies property and negotiates with seller
   └── Price, terms, timeline agreed

2. Due Diligence (Sampatti Janch)
   ├── Verify Lalpurja at Malpot Office
   ├── Check encumbrances (mortgages, court orders, restrictions)
   ├── Verify survey map at Survey Office (Napi)
   ├── Confirm tax status at municipality
   ├── Physical inspection of property
   ├── Check ownership history
   └── [Requires Verification: Whether buyers typically use lawyers for this step]

3. Preliminary Agreement (Baikalpatra)
   ├── Drafted and signed by both parties
   ├── Advance payment exchanged (10-20% typical)
   └── [Requires Verification: Whether this step is universal or varies]

4. Prepare supporting documents
   ├── Obtain tax clearance certificate from municipality
   ├── Obtain Ghar Bato Sifaris from ward office
   ├── Gather citizenship copies, photos, PAN cards
   ├── Obtain consent from co-owners if applicable
   └── [Requires Verification: Exact document requirements per district]

5. Visit Land Revenue Office (Malpot)
   ├── Both parties appear in person (or via Power of Attorney)
   ├── Submit all documents for verification
   ├── Government valuation assessment
   └── Fee calculation

6. Pay fees and taxes
   ├── Registration fee (buyer, typically 4%)
   ├── Capital gains tax (seller, 5-7.5%)
   ├── Local development tax
   └── Other applicable fees

7. Deed Execution (Rajinama)
   ├── Transfer deed prepared and signed
   ├── Old Lalpurja cancelled
   ├── New Lalpurja issued in buyer's name
   └── Survey records updated (recommended)
```

### 7.3 Land Transfer (Inheritance) Workflow

```
1. Death of property owner
   └── Death registration obtained

2. Identify legal heirs
   ├── Per Muluki Civil Code 2074, Chapter 11
   ├── Order: spouse and children first, then parents, then siblings
   ├── Sons and daughters have equal inheritance rights
   └── [Requires Verification: Process for disputed inheritance]

3. Obtain supporting documents
   ├── Relationship certificates (Nata Pramanit) from ward office
   ├── Legal-heir certificate / heir list
   ├── Death certificate
   ├── Citizenship certificates of all heirs
   └── Consent/no-objection from co-heirs

4. Apply at Land Revenue Office
   ├── Submit original Lalpurja
   ├── Submit all supporting documents
   ├── Concessional registration fee (0.5-1% typically)
   └── Mutation (Dakhil Kharij) process

5. New Lalpurja issued
   ├── In heir's name (or partitioned among heirs)
   └── [Requires Verification: Timeline for inheritance transfer processing]
```

---

## 8. Legal and Regulatory Context

> **IMPORTANT**: This section is research only. It identifies laws and regulations that appear relevant based on publicly available sources. It does not constitute legal advice. Legal interpretation and determination of legal validity require review by a qualified legal professional in Nepal.

### 8.1 Primary Legislation

| Law | Year | Relevance |
|---|---|---|
| **Constitution of Nepal** | 2072 BS (2015 AD) | Article 25: Right to property; Article 38: Equal lineage rights for women. Establishes the federal structure for land administration. |
| **Muluki Civil Code (Muluki Dewani Sanhita)** | 2074 BS (2017 AD) | Part 5: Provisions on contracts, property transfer, lease, co-ownership, partition, inheritance (Chapters 11-13), and will. The primary code governing private property transactions. |
| **Land Act (Bhumi Sambandhi Ain)** | 2021 BS (1964 AD) | Land ownership rights, ceiling limits, tenancy rights, land reform provisions |
| **Land Revenue Act (Malpot Ain)** | 2034 BS (1978 AD) | Registration process, revenue collection, Lalpurja issuance, Land Revenue Office procedures |
| **Land (Survey and Measurement) Act** | 2019 BS (1962 AD) | Cadastral survey, land measurement standards, map maintenance |
| **House Rent Control Act** | 2048 BS (1992 AD) | Rent fixation, eviction rules, dispute resolution for residential tenancies |
| **Income Tax Act** | 2058 BS (2002 AD) | Capital gains tax on property sales (Section 95Ka), rental income tax |
| **Local Government Operation Act** | 2074 BS (2017 AD) | Municipal authority to levy property tax, set local fee rates, issue certificates |
| **National Identity Card and Registration Act** | 2076 BS (2019 AD) | National ID card framework |
| **Electronic Transaction Act** | 2063 BS (2008 AD) | Legal validity of digital payments and records |
| **Guthi Corporation Act** | 2033 BS (1976 AD) | Rules for Guthi (trust) land, which has transfer restrictions |
| **Land Acquisition Act** | 2034 BS (1977 AD) | Government's power to acquire private land for public use |

### 8.2 Other Relevant Legal Concepts

- **Deed System**: Nepal operates a deed system (not a title registration system). The government acts as witness to transactions but does not guarantee title. This places significant responsibility on parties to verify ownership independently.
- **Stamp Duty**: Documents for property transactions are typically prepared on stamp paper of specified value.
- **Notary Public Rules 2063**: Governs notarisation of documents, including fee ceilings for translation and notarisation.
- **Land Ceiling**: Maximum land ownership limits exist (e.g., 25 Ropani in Kathmandu Valley, 10 Bigha in Terai). Buyers must not exceed these limits.
- **Foreign Ownership**: Foreign nationals generally cannot own land in Nepal. Non-Resident Nepalis (NRNs) may own property under specific conditions defined by the NRN Act 2064.

### 8.3 Source References

- **Primary legislation sources**: nepaldivorce.com, nepallegalfirm.com.np, courtmarriageinnepal.com, attorneynepal.com
- **Land classification and tenure**: CSRC Nepal land data, GLTN land policy report, 1library.net Nepal land tenure article
- **Cadastral surveying context**: Nepalese Journal on Geoinformatics (academic source on survey practices and land disputes)

---

## 9. Domain Boundaries

### 9.1 Within Potential Domain Scope

Activities the application may potentially assist with:

- Drafting lease/rental agreements
- Drafting preliminary sale agreements (Baikalpatra)
- Drafting transfer deeds (Rajinama) — **Requires verification** of format constraints
- Drafting gift deeds (Dan Bakaspatra)
- Organizing document checklists for property transactions
- Capturing photographs of source documents
- Extracting text from documents via OCR
- Presenting extracted information for user verification/correction
- Storing structured information for reuse
- Generating documents in Nepali language
- Providing informational guidance on transaction workflows
- Preparing Power of Attorney documents
- Managing document templates

### 9.2 Outside / Unconfirmed

Activities that require further research, may be outside the application scope, or may require official systems or professional involvement:

| Activity                                                       | Status                                                                                                          |
| -------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Legally validating documents                                   | Outside — requires legal professional qualification                                                             |
| Providing legal advice                                         | Outside — requires legal professional qualification                                                             |
| Registering transactions at Land Revenue Office                | Unconfirmed — may be outside scope; requires verification of system integration feasibility                     |
| Interacting with government digital systems (LIMS, Mero Kitta) | Unconfirmed — requires technical and legal research                                                             |
| Guaranteeing land title or ownership verification              | Outside — no system can guarantee title certainty                                                               |
| Replacing lawyers or legal professionals                       | Outside — the system assists with document preparation, not legal representation                                |
| Replacing document writers (Lekhandas)                         | Unconfirmed — this may be a domain impact, not a feature goal                                                   |
| Verifying the authenticity of identity documents               | Unconfirmed — may be outside scope; requires research                                                           |
| Handling disputed property or contested inheritance            | Likely outside — these require legal/court processes                                                            |
| Multi-language translation (Nepali to English, etc.)           | Unconfirmed — potential scope if users need bilingual documents                                                 |
| Offline operation                                              | Unconfirmed — depends on target deployment context                                                              |
| Digital signature / e-signature                                | Unconfirmed — requires legal verification of acceptance                                                         |
| Notarisation of documents                                      | Unconfirmed — the system likely cannot perform notarisation; may assist in preparing documents for notarisation |

---

## 10. Key Domain Questions

### 10.1 Legal Verification

| # | Question | Reason |
|---|---|---|
| L1 | Are there legal requirements for the format/content of a Rajinama (transfer deed) that constrain how the document can be generated? | Determines whether document generation is feasible as an app feature. |
| L2 | What are the legal requirements for a valid lease agreement beyond what the Muluki Civil Code specifies? | Ensures generated lease agreements are legally compliant. |
| L3 | Is there a legal requirement for documents to be on specific stamp paper or government-specified formats? | Affects whether the app can print/export documents that are legally acceptable. |
| L4 | What are the legal constraints on storing or processing users' personal and property data? | Data privacy and security requirements. |
| L5 | Are digital/e-signatures legally recognized for property documents in Nepal? | Affects whether the app can support digital execution of documents. |

### 10.2 Domain Expert Verification

| # | Question | Reason |
|---|---|---|
| D1 | How do typical Nepali users currently approach land document preparation? | Understand current practice to design a useful tool. |
| D2 | What is the role of Lekhandas (document writers) in practice, and how would an app affect them? | Understand potential adoption barriers and stakeholder impacts. |
| D3 | Do users typically engage lawyers for sale transactions, or is DIY common? | Determines whether the app serves end users directly or through intermediaries. |
| D4 | What are common errors or pitfalls in document preparation that an app could help avoid? | Identifies specific user needs. |
| D5 | What is the literacy level and digital literacy level of the target user population? | Affects UI/UX design and language choices. |

### 10.3 Government Process Verification

| # | Question | Reason |
|---|---|---|
| G1 | Do different districts' Malpot offices have different document requirements? | Affects whether the system needs location-specific templates. |
| G2 | What is the current state of digitalization in Malpot offices across Nepal? | Determines whether digital document submission is possible. |
| G3 | Can documents prepared outside the Malpot office be accepted, or must the deed be written at the office? | Fundamental feasibility question for document generation. |
| G4 | What is the exact process and timeline for inheritance/mutation (Dakhil Kharij) at Malpot? | Required to design inheritance workflow support. |
| G5 | Are there any current or planned government systems that the app should align with? | Avoids building something that will be superseded. |

### 10.4 Product Scope Decisions

| # | Question | Reason |
|---|---|---|
| P1 | Should the app support all three transaction types (rent, sale, transfer) at launch, or focus on one? | Scope and prioritization decision. |
| P2 | Should the app support residential lease, agricultural lease, commercial lease, or all? | Scope decision affecting templates and workflows. |
| P3 | Should the app support Non-Resident Nepali (NRN) users specifically? | Affects feature requirements and compliance. |
| P4 | Should the app attempt OCR on handwritten Devanagari text? | Significant technical scope decision. |
| P5 | Should the app provide informational guidance on processes, or only document generation tools? | Product positioning decision. |

### 10.5 Technical Research

| # | Question | Reason |
|---|---|---|
| T1 | What OCR engines/devices support Nepali (Devanagari) script with acceptable accuracy? | Core technical feasibility question (to be addressed in workstream 0.8). |
| T2 | Can OCR handle stamped/sealed sections of land documents? | Technical feasibility. |
| T3 | What document generation libraries support Nepali script output in PDF? | Technical feasibility. |
| T4 | What is the expected document image quality from mobile phone cameras? | Affects OCR approach. |
| T5 | Can the app operate offline, or is cloud connectivity required for OCR/document generation? | Architecture constraint. |

---

## 11. Sources and References

### Government and Official Sources

| Title | Organization | URL | Date Accessed | Information Supported |
|---|---|---|---|---|
| Department of Land Management and Archive | DOLMA, Government of Nepal | dolma.gov.np | 2026-07-27 | Land administration structure, Malpot offices |
| Department of Survey | DOS, Government of Nepal | dos.gov.np | 2026-07-27 | Survey offices, cadastral mapping, Mero Kitta |
| Mero Kitta Portal | Department of Survey | merokitta.dos.gov.np | 2026-07-27 | Online survey/map services |
| Ministry of Land Management, Cooperatives and Poverty Alleviation | Government of Nepal | molmcpa.gov.np | 2026-07-27 | Ministry oversight, policy reference |

### Legal and Professional Sources

| Title | Organization | URL | Date Accessed | Information Supported |
|---|---|---|---|---|
| Property Registration in Nepal | Basobaas.com | basobaas.com/blog/property-registration-process-nepal-2026 | 2026-07-27 | Sale workflow, registration fees, documents required |
| Land Registration in Nepal | Court Marriage in Nepal | courtmarriageinnepal.com/blog/land-registration-nepal | 2026-07-27 | Land registration process, fees, documents, legal framework |
| Buying Property in Nepal | Court Marriage in Nepal | courtmarriageinnepal.com/blog/buying-property-nepal | 2026-07-27 | Due diligence process, sale agreement, registration steps |
| Transfer of Land and Property in Nepal | Summit Legal | summitlegal.com.np/blog/transfer-of-land-and-property-in-nepal | 2026-07-27 | Transfer process overview |
| Lease Agreement Law in Nepal | Common Law Nepal | commonlaw.com.np/publications/lease-agreement-law-in-nepal | 2026-07-27 | Rental agreement legal framework |
| Lease Agreement in Nepal 2026 | Notary Kathmandu | notarykathmandu.com/blog/lease-agreement-in-nepal | 2026-07-27 | Lease rules, tax, notarisation, format |
| House Rent Law in Nepal | Law Imperial | lawimperial.com/rent-in-nepal | 2026-07-27 | Residential tenancy law, Muluki Civil Code provisions |
| How to Verify Land in Nepal | Punarvaas Un Nepal | punarvaasunepal.com/how-to-verify-land-in-nepal | 2026-07-27 | Due diligence process, Lalpurja verification |
| Buying & Registration of Land | Aafnai Ghar | aafnaighar.com/buying-registration-of-land-and-houses-in-nepal | 2026-07-27 | Step-by-step buying process, document list |
| Real Estate Law in Nepal | Nepal Divorce | nepaldivorce.com/blog/real-estate-law-in-nepal | 2026-07-27 | Legal framework overview, land types |
| Property Transfer Process in Nepal | Nepal Lawyer | nepallawyer.com/blog/property-transfer-process-in-nepal | 2026-07-27 | Transfer process, legal requirements |
| Land Registration Requirements in Nepal | Nepal Lawyer | nepallawyer.com/blog/land-registration-requirements-in-nepal | 2026-07-27 | Registration requirements, fees |
| Inheritance Law Nepal | Wakil Nepal | wakilnepal.com/articles/inheritance-succession-nepal-complete-guide | 2026-07-27 | Succession framework, heir order |
| Inheritance Laws in Nepal | Notary Nepal | notarynepal.com/blog/inheritance-laws-in-nepal | 2026-07-27 | Inheritance, partition, will, mutation |
| Succession and Inheritance Law Nepal | Court Marriage in Nepal | courtmarriageinnepal.com.np/publication/succession-inheritance-law-nepal | 2026-07-27 | Succession legal framework |
| Citizenship in Nepal 2026 | Notary Nepal | notarynepal.com/blog/citizenship-in-nepal | 2026-07-27 | Citizenship types, identity documents |
| National ID Card Nepal 2026 | Notary Kathmandu | notarykathmandu.com/blog/national-id-card-nepal | 2026-07-27 | National ID process |
| Land Tax Payment Online Nepal | Attorney Nepal | attorneynepal.com/blog/land-tax-payment-online-nepal | 2026-07-27 | Land tax types, online payment, legal framework |
| Lalpurja Guide | Basobaas | basobaas.com/blog/lalpurja-land-ownership-certificate-nepal-guide | 2026-07-27 | Lalpurja types, verification |

### Academic and Reference Sources

| Title | Organization | URL | Date Accessed | Information Supported |
|---|---|---|---|---|
| Land in Data Statistical Information | CSRC Nepal | csrcnepal.org/wp-content/uploads/2023/12/Land-Data-CSRC-2023-4.pdf | 2026-07-27 | Land data context |
| Land Policy Development in Nepal | GLTN | gltn.net/sites/default/files/2025-10/Land-policy-development-in-Nepal.pdf | 2026-07-27 | Land policy evolution |
| Technical Deficiencies and Human Factors in Land Disputes | Nepalese Journal on Geoinformatics | nepjol.info/article/51259 | 2026-07-27 | Survey practices, role of Lekhandas |
| Nepal Land Tenure and Access | 1Library.net | 1library.net/article/nepal-land-tenure-access-practices.92n46rz | 2026-07-27 | Historical land tenure, land administration evolution |

---

## Document Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 0.1 | 2026-07-27 | Project Team | Initial draft based on publicly available research |
