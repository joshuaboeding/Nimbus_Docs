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

Controls the glance-to-value ratio of a record.

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

## 5. Tethered Wealth Applications — Lightning Customization

**Lightning App Architecture**
Custom "Tethered Wealth Dashboard" app built via App Manager. Branded with
charcoal hex (#333333). Navigation limited to: Home, Contacts, Financial
Assets, Chatter. All irrelevant tabs removed.

**List View Engineering**
Financial_Asset__c list view "High Value Global Assets" — filter logic:
Asset Value > $100,000 AND Country not equal to USA. Donut chart attached
summing total asset value grouped by Country — instant portfolio visualization
before opening any record.

**Compact Layout Implementation**
Financial_Asset__c compact layout surfaces Asset_Value, Asset_Type, and
Country_of_Residence at the top of every record. Mobile-first — advisor sees
the three critical fields immediately on the Salesforce Mobile App during
client meetings.

**Dynamic Forms & Lightning App Builder**
Client Record page upgraded to Dynamic Forms. Custom "Tax & Compliance"
section created at top of page. Foreign_Tax_ID__c field visible for
international clients, hidden for domestic clients — keeps UI clean per
client type.

**Page Layout Editor — Related Lists**
Files related list added to Financial_Asset__c layout via Page Layout Editor.
Ensures immediate access to PDF tax returns and wire transfer receipts
directly from the asset record.

---

## 6. Custom Buttons, Links, and Quick Actions

### Custom Buttons and Links

Custom buttons and links integrate Salesforce data with external URLs,
applications, or intranets. Salesforce fields can be passed as merge fields
into URLs to transfer data automatically.

**Three Primary Types**

- **List Button** — appears on a related list on an object record page
- **Detail Page Link** — appears in the Links section of record details.
  Note: only supported on record pages that do not use Dynamic Forms
- **Detail Page Button** — appears in the action menu in the highlights panel
  at the top of a record page

**Configuration Steps**
- Navigate to Object Manager, select the object, then Buttons, Links, and Actions
- Define the URL using the formula editor and merge fields
- Add the button or link to the object's Page Layout

### Quick Actions

Allow users to perform tasks (create records, log calls, send emails) with
minimal clicks and without navigating away from their current workspace.

**Object-Specific Actions**
- Automatic relationship to other records — a Contact created from an Account
  action is automatically linked to that Account
- Live on the specific object's page layout
- Types: Create a Record, Update a Record, Log a Call, Send Email, Custom
- Use the Action Layout Editor to define exactly which fields appear in the
  pop-up — keeps it clean and uncluttered

**Global Actions**
- No automatic relationship to a specific record — parent must be linked manually
- Accessible from anywhere via the Salesforce header (+ icon)
- Created in Setup under Global Actions, added to Publisher Layouts

**Page Layout Integration**
- Drag actions from the Mobile & Lightning Actions category in the palette
- Drop into the Salesforce Mobile and Lightning Experience Actions section
- May need to click the wrench icon to override defaults first

### Tethered Wealth Applications — Buttons and Actions

**List Button — Compliance**
Button on the Financial Accounts related list linking directly to IRS PDF
guidelines for FBAR reporting.

**Detail Page Link — Due Diligence**
Custom link on the Contact page passing Contact.FirstName and Contact.LastName
into the FINRA BrokerCheck search URL for instant credential verification.

**Detail Page Button — External Portfolio**
Button passing Account.AccountNumber into the URL of Orion or Black Diamond
portfolio management software — opens the client performance dashboard in a
new tab instantly.

**Object-Specific Action — Log Discovery Call**
Placed on the Account (Household) record. Three-field pop-up: Notes, Action
Items, Next Meeting Date. Automatically attaches to the Household. No
navigation required.

**Object-Specific Action — Add Foreign Asset**
Create a Record action on the Account showing only the fields needed for an
expat asset: Currency Type, Country of Origin, Value.

**Global Action — Quick Prospect**
Available in the top header from anywhere in the system. Captures Prospect
name, email, and country of residence without navigating away from the
current screen.

---

## 7. User Engagement & Prompts

### Core Philosophy

The goal of user engagement is to deliver the "Aha!" moment — the exact second
a user realizes a tool makes their job easier. Good engagement gives users
actionable, relevant information without interrupting their workflow unnecessarily.

**The Four Key Scenarios**
- **Onboarding** — guiding users where to begin, highlighting what is new
- **Feature Discovery & Adoption** — nudging users toward unused features
- **Troubleshooting Help** — providing just-in-time assistance when stuck
- **Deeper Learning** — offering advanced training for complex tasks

**Push vs. Pull Delivery**
- **Push** — system shows it automatically (pop-up prompt, empty state message).
  Use when users would not know to look for help.
- **Pull** — user requests it (hovering over an info icon, clicking Help menu).
  Use when users are motivated to seek answers.

### Prompts vs. Walkthroughs

- **Prompt** — a single small window. Best for short messages or a single
  call-to-action.
- **Walkthrough** — a connected series of prompts. Best for step-by-step
  multi-page processes.

**The Three Prompt Types**

- **Floating** — non-intrusive, placeable in 9 screen positions. Best for
  short messages (e.g., "Check out this new list view").
- **Targeted** — visually points to a specific field or button on the page.
  Best for highlighting a new custom button or required field.
- **Docked** — stays pinned to the bottom right while the user clicks around.
  Supports embedded video. Best for step-by-step guides where the user needs
  to read instructions while actively working through the screen.

### Design Frameworks

**M.A.P. (Message, Audience, Purpose)**
- **Message** — exactly what you are telling the user
- **Audience** — all users, admins only, new hires only, etc.
- **Purpose** — what behavior are you trying to change

**F.A.C.E. Principles**
Keep all prompt text: Friendly, Accurate, Concise, Educational

### Tethered Wealth Applications — User Engagement

**Targeted Prompt — Compliance**
New Requires_FBAR_Reporting__c checkbox added to the Expat Contact page.
Targeted Prompt points directly at the checkbox on first load.
Message: "If your client holds over $10k in foreign accounts, check this box
to trigger the automated CPA alert workflow."

**Docked Prompt — Live Discovery Call Script**
Advisor is on a live call with a new expat prospect. He clicks a button to
open a Docked Prompt containing 5 key Expat Tax Discovery Questions. Because
it stays pinned, he reads the questions aloud while simultaneously entering
the client's answers into Salesforce fields on the rest of the screen.

**Floating Prompt — Feature Adoption**
New Kanban view built for "Expats in Onboarding" pipeline. Floating Prompt
appears on next login: "Tired of lists? View your pipeline as a visual
Kanban board." One click drives adoption without any training session required.