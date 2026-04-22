# Salesforce: Lightning Experience Customization

## 1. Object & Application Foundation

- **Custom Objects & Fields:** Back-end storage. A custom object requires a
  Custom Tab to be visible in the UI — without a tab it exists in the database
  but cannot be added to a navigation bar.
- **Lightning Apps:** Tailored collection of objects, tabs, and utility items
  bundled into a single navigation bar. Managed via App Manager in Setup.
  Supports custom branding (logos and hex colors).
  - Architecture best practice: build role-specific apps, strip irrelevant tabs
    to reduce cognitive load per user group (e.g., Sales vs. Finance)
- **Feed Tracking:** Enables Chatter on an object — users can follow specific
  records and see an audit trail of field updates in a social feed format.

## 2. List Views & Data Visualization

Primary method for users to segment and filter data without running formal reports.

- **Filtering Logic:** Apply specific filters to pare down large datasets into
  actionable lists (e.g., State = WA, OR, CA)
- **List View Charts:** Donut or Bar chart visualizations built directly into a
  List View — aggregate data dynamically based on active filters
- **Inline Editing:** Pencil icon on editable fields allows record updates
  without opening the individual record page

## 3. UI Optimization: Compact Layouts

Controls the "glance-to-value" ratio of a record.

- **Highlights Panel:** Compact Layout controls the top banner of a Lightning
  Record Page — first field listed becomes the bold headline
- **Expanded Lookup Cards:** Controls fields shown when hovering over a
  related record link
- **Mobile Responsiveness:** Compact Layouts strictly control what users see
  in the Salesforce Mobile App where screen real estate is limited

## 4. Record Page Architecture

Two separate engines for building record pages.

**Page Layout Editor (Classic Engine)**
- Controls standard/custom buttons and Related Lists (Files, Opportunities,
  and other associated records attached to the main record)

**Lightning App Builder (Modern Engine)**
- Drag-and-drop interface for overall page structure (tabs, columns, components)

**Dynamic Forms**
- Migration feature within App Builder — breaks rigid classic page layout into
  individual modular fields
- Allows single fields to be placed anywhere on the page
- Supports conditional visibility rules per field

**Page Activation & Assignment**
- Built pages must be activated before going live
- Different layouts assignable based on intersection of App + Record Type +
  User Profile

## 5. Tethered Wealth Applications

**Lightning App Architecture**
Custom "Tethered Wealth Dashboard" app built via App Manager. Branded with
charcoal hex (`#333333`). Navigation limited to: Home, Contacts, Financial
Assets, Chatter. All irrelevant tabs removed.

**List View Engineering**
`Financial_Asset__c` list view "High Value Global Assets" — filter logic:
Asset Value > $100,000 AND Country ≠ USA. Donut chart attached summing total
asset value grouped by Country — instant portfolio visualization before
opening any record.

**Compact Layout Implementation**
`Financial_Asset__c` compact layout surfaces `Asset_Value`, `Asset_Type`, and
`Country_of_Residence` at the top of every record. Mobile-first — advisor
sees the three critical fields immediately on the Salesforce Mobile App during
client meetings.

**Dynamic Forms & Lightning App Builder**
Client Record page upgraded to Dynamic Forms. Custom "Tax & Compliance"
section created at top of page. `Foreign_Tax_ID__c` field visible for
international clients, hidden for domestic clients — keeps UI clean per
client type.

**Page Layout Editor — Related Lists**
`Files` related list added to `Financial_Asset__c` layout via Page Layout
Editor. Ensures immediate access to PDF tax returns and wire transfer receipts
directly from the asset record.

Here are your clean, formatted notes ready to be pasted directly into VS Code and then synced to your GitHub and Notion.

Salesforce Customization: Buttons, Links, and Quick Actions
1. Custom Buttons and Links
Custom buttons and links integrate Salesforce data with external URLs, applications, or intranets. They can include Salesforce fields as "tokens" (merge fields) within the URL to pass data automatically (e.g., passing a client's zip code into Google Maps).

Three Primary Types:
List Button: Appears on a related list on an object record page. (e.g., A button on the "Energy Audits" related list).

Detail Page Link: Appears in the "Links" section of the record details on an object record page. (Note: Only supported on record pages that don't use Dynamic Forms).

Detail Page Button: Appears in the action menu in the highlights panel at the top of a record page.

Configuration Steps:

Navigate to Object Manager -> Select Object -> Buttons, Links, and Actions.

Define the URL using the formula editor and merge fields.

Add the button/link to the Object's Page Layout.

2. Quick Actions
Actions allow users to quickly perform tasks (create records, log calls, send emails) with minimal clicks and without navigating away from their current workspace.

Object-Specific Actions
The Core Trait: They have an automatic relationship to other records. If you create a Contact from an Account using an object-specific action, the new Contact is automatically linked to that Account.

Location: They live on the specific object's page layout.

Types: Create a Record, Update a Record, Log a Call, Custom (Visualforce/Lightning Components), Send Email.

Layout Editor: After creating the action, you use the Action Layout Editor to define exactly which fields the user needs to fill out (keeping it clean and uncluttered).

Global Actions
The Core Trait: They have no automatic relationship to a specific record. Someone has to manually link the new record to a parent if necessary.

Location: They live in the Salesforce Header (the + icon) and are accessible from anywhere in the system.

Configuration: Created in Setup under Global Actions, and then added to the Publisher Layouts (not the Object Manager).

3. Page Layout Integration
To make actions visible in the modern UI, they must be added to a specific section of the page layout.

Drag actions from the "Mobile & Lightning Actions" category in the palette.

Drop them into the "Salesforce Mobile and Lightning Experience Actions" section of the page layout (you may need to click the wrench icon to override the defaults first).

🏦 Application for Tethered Wealth (Boutique Advisory)
To make the Salesforce UI incredibly efficient for an advisor managing expat portfolios, these tools can be configured to eliminate data entry friction and connect to external financial tools.

Buttons & Links for Wealth Management
List Button (Compliance): A button on the "Financial Accounts" related list that points directly to the IRS PDF guidelines for FBAR reporting.

Detail Page Link (Due Diligence): A custom link on the Contact page that passes the {!Contact.FirstName} and {!Contact.LastName} into the FINRA BrokerCheck search URL to quickly verify credentials or history.

Detail Page Button (External Portfolio): A button that passes the client's {!Account.AccountNumber} into the URL of Orion or Black Diamond (portfolio management software) to instantly open their performance dashboard in a new tab.

Quick Actions for Advisor Workflows
Object-Specific Action ("Log Discovery Call"): Placed on the Account (Household) record. When the advisor finishes a call, clicking this opens a clean, 3-field pop-up: Notes, Action Items, and Next Meeting Date. It automatically attaches to the Household, saving time and keeping the UI uncluttered.

Object-Specific Action ("Add Foreign Asset"): A "Create a Record" action on the Account that only shows the specific fields needed for an expat asset (Currency Type, Country of Origin, Value).

Global Action ("Quick Prospect"): Placed in the top header. If the advisor is reviewing a complex tax document and gets a phone call from a new lead, they can click the Global Action to capture the Prospect's name, email, and country of residence without navigating away from the tax document they were currently studying.