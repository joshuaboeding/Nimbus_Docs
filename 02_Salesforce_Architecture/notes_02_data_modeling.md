# Salesforce: Data Modeling

## 1. Data Model Foundations

The data model is the structural blueprint of the Salesforce database, translating
complex database tables into a human-readable interface.

- **Objects:** Function as database tables.
- **Fields:** Function as columns within those tables.
- **Records:** Function as individual rows — the actual data entries.

## 2. Object Typology

- **Standard Objects:** Pre-built tables included out of the box (Account, Contact, Lead, Opportunity).
- **Custom Objects:** Bespoke tables built for industry or company-specific data. API names always end with `__c` (e.g., `Property__c`).

## 3. Field Architecture

- **Identity Fields:** 18-character case-insensitive ID auto-generated for every record — visible in the URL.
- **System Fields:** Read-only administrative fields (e.g., `CreatedDate`, `LastModifiedById`).
- **Name Fields:** Primary identifier for a record — free-text or auto-numbered.
- **Custom Fields:** Admin-created columns for specific data points. Common types:
  - `Currency` — financial tracking
  - `Date/DateTime` — milestones and scheduling
  - `Checkbox` — Boolean (True/False) logic
  - `Formula` — read-only, auto-calculates from other fields

## 4. Relational Architecture

Relationships are specialized fields that connect objects and allow data to flow between tables.

**Lookup Relationship**
- Loose, casual link between two objects
- Objects function independently — neither requires the other to exist
- Can be one-to-one or one-to-many
- Deleting one record does not delete the linked record

**Master-Detail Relationship**
- Strict, highly dependent link
- Master controls behavior, visibility, and security of the Detail object
- Detail object cannot exist as a standalone record
- Cascade Delete: deleting the Master permanently deletes all related Detail records
- Relationship field is always created on the Detail object

**Hierarchical Relationship**
- Specialized lookup available exclusively on the User object
- Used for mapping reporting structures and management chains

## 5. Schema Builder

Native visual UI for architectural mapping and rapid development.

- View entire data model as a drag-and-drop canvas
- Identify relationships between objects visually
- Create objects and fields directly on the canvas without navigating Object Manager

## 6. Tethered Wealth Applications

**Custom vs. Standard Objects**
- Standard `Account` = Household (e.g., The Song Family)
- Standard `Contact` = Individual family members (e.g., Arthur Song)
- Custom `Financial_Asset__c` = Offshore investments — no standard Salesforce object exists for international bank accounts

**Lookup Relationship in Practice**
`CPA_Firm__c` linked to `Contact` via Lookup. If the CPA firm is deleted, the client Contact record remains intact — it simply loses the CPA link.

**Master-Detail Relationship in Practice**
`Asset_Valuation_History__c` (Detail) linked to `Financial_Asset__c` (Master). Tracks historical account values over time. If the Swiss UBS account is deleted, all valuation history records cascade delete — no database bloat.

**Formula Field in Practice**
`Advisory_Fee_Projection__c` on `Financial_Asset__c` — formula multiplies `Current_Value` by 0.01 (1% AUM fee). Advisor sees projected revenue per asset instantly without manual calculation.

**Schema Builder for Auditing**
Before data import, use Schema Builder to visually map how a single Expat Contact connects to their Primary Household, 3 Offshore Assets, and Tax Advisor. Use the diagram to walk stakeholders through system logic before executing the import.