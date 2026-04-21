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