# Salesforce: Agentforce 360 Platform Basics

## 1. Core Architecture & Infrastructure

- **Multitenancy:** All orgs share the same infrastructure but data remains isolated — like an apartment building.
- **Metadata:** The structural blueprint of the org. Fields, layouts, security rules — everything that remains when data is deleted.
- **Data 360 (Data Lakehouse):** Handles structured and unstructured data natively. Includes Zero Copy Integration — act on data in external warehouses like Snowflake without duplicating it.
- **API:** Every piece of metadata is API-enabled on creation (e.g., `{!Contact.Name}`). Connects internal apps, mobile, and external software seamlessly.

## 2. Database Hierarchy

- **App:** A tailored collection of objects, fields, and tabs for a specific business process.
- **Object:** A database table. Standard objects are built-in (Accounts, Contacts, Leads). Custom objects are built for unique business needs.
- **Record:** A single row within an object table — the actual data.
- **Field:** A column within an object table.

## 3. Setup — The Command Center

Centralized hub for all admin configuration and RevOps architecture.

- **Object Manager:** Workspace for creating and editing objects and fields.
- **Quick Find:** Bypasses manual menu navigation.

**Top 5 Setup Pages:**
- **Company Information:** Org ID, licensing, data limits
- **Users:** Deactivate/freeze users, reset passwords
- **Profiles:** Manage permissions and system visibility
- **View Setup Audit Trail:** 6-month log of who changed what — critical for troubleshooting
- **Login History:** 6-month security and adoption log

## 4. Automation & Ecosystem

- **Flow Builder:** No-code automation — targets heavy email collaboration, manual spreadsheet updates, repetitive data entry.
- **Prompt Builder:** Generative AI for draft generation within workflows.
- **AppExchange:** Enterprise app store. Best practice: Identify stakeholders → Research → Test in Sandbox → Evaluate → Deploy to production.

## 5. Tethered Wealth Applications

**Database Hierarchy in Practice**
- App: Custom "Expat Advisory Dashboard" with console navigation for CFP daily workflow
- Object: `Financial_Asset__c` to track offshore accounts
- Field: `Foreign_Tax_Status__c` picklist on Contact for FATCA reporting
- Record: "Arthur Song's Swiss UBS Account - $450,000"

**Automation**
Screen Flow + Prompt Builder for quarterly review initiation — pulls client asset data and generates a personalized email draft for advisor review before sending.

**Zero Copy Integration**
Data 360 allows Salesforce to read Snowflake portfolio data in real-time directly on the client Contact record — no CSV export/import cycle.

**Setup Audit Trail for Compliance**
Field history tracking on risk tolerance changes — who changed it, when, full accountability trail for regulators.

**AppExchange Strategy**
Currency conversion via AppExchange package rather than custom Apex. Install in Sandbox first to verify no conflicts with `Financial_Asset__c` before production deploy.