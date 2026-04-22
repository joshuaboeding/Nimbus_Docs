# Salesforce: User Engagement & Prompts

## 1. Core Philosophy

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

## 2. Prompts vs. Walkthroughs

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

## 3. Design Frameworks

**M.A.P. (Message, Audience, Purpose)**
- **Message** — exactly what you are telling the user
- **Audience** — all users, admins only, new hires only, etc.
- **Purpose** — what behavior are you trying to change

**F.A.C.E. Principles**
Keep all prompt text: **Friendly, Accurate, Concise, Educational**

## 4. Tethered Wealth Applications

**Targeted Prompt — Compliance**
New `Requires_FBAR_Reporting__c` checkbox added to the Expat Contact page.
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