# Salesforce: Product Ecosystem and Agentforce

## 1. Platform vs. Clouds

The Salesforce Platform is the underlying engine — database, security,
automation, and UI framework. The "Clouds" are applications built on top
of that platform to solve specific business problems.

- **Sales Cloud** — tracks Leads, Opportunities, and revenue generation
- **Service Cloud** — manages Cases, Knowledge, and customer support.
  Omni-channel unification across chat, email, and phone.
- **Experience Cloud** — custom-branded portals for partners and customers.
  Relevant for Tethered Wealth client-facing login portals.

Common terminology trap: marketing often refers to Sales Cloud as "the
Salesforce platform." Technically, Sales Cloud is an app running on top
of the actual Salesforce Platform. Data is shared between clouds by default.

## 2. Agentforce 360 — AI Integration

Salesforce is moving toward human-agent co-piloting rather than human-only
workflows. Agentforce is not a standalone silo — it connects humans, AI
agents, and structured data in real-time across Sales, Service, and Marketing.

**Key Components**
- AI agents use LLMs, business context, and metadata to assist both
  end-customers and human employees
- Omni-channel: human and AI agents are unified in Service Cloud — the
  client experience follows them regardless of channel (chat, email, phone)
- Sales productivity: AI handles predictive lead scoring and automates
  administrative data entry

## 3. Security & Administration

- A professional admin never manages individual user passwords directly
- Security is maintained through SSO (Single Sign-On) and enforced MFA
  (Multi-Factor Authentication)
- Admin credentials are personal — not shared or used to reset user passwords

## 4. Tethered Wealth Applications

**Experience Cloud — Client Portal**
Expat clients need a secure, branded portal to view portfolio performance,
upload documents, and communicate with their advisor. Experience Cloud
provides this without exposing the internal Salesforce org.

**Agentforce — Lead Scoring and Advisory Drafts**
Agentforce handles predictive intent scoring and first-draft advisory
communications at scale. The local Ollama SLM layer audits outputs before
any draft reaches the human advisor — consistent with the HITL architecture
defined in ARCHITECTURE.md.