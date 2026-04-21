# Project Nimbus — Vision & Strategic Roadmap

> **Project Nimbus** is the portfolio build.
> **Tethered Wealth Advisors** is the fictional firm it is built for.
> These are intentionally separate: Nimbus is the engineering project; Tethered Wealth is the business context that gives every architectural decision a real-world reason to exist.

---

## The Firm: Tethered Wealth Advisors

Tethered Wealth is a mock AI-forward wealth advisory firm serving expatriates — individuals navigating cross-border financial complexity, multi-currency portfolios, and jurisdiction-specific compliance requirements.

Expats are underserved by traditional wealth advisory. They face:
- Tax obligations in multiple jurisdictions
- Currency exposure and FX risk on savings and income
- Pension portability and foreign account reporting requirements (FBAR, FATCA)
- Life events (repatriation, relocation, retirement abroad) that trigger complex financial decisions

Tethered Wealth exists to serve this client. Every data model, CRM workflow, AI governance layer, and compliance control in Project Nimbus is designed with this client in mind.

**Business Model:** Subscription-based advisory tiers
| Tier | Description |
|------|-------------|
| Core | Self-serve financial tracking, document vault, automated reporting |
| Premium | Human advisor access, quarterly reviews, tax coordination |
| Concierge | Dedicated advisor, estate planning, multi-jurisdiction compliance |

**Key SaaS Metrics:** MRR, churn, LTV, CAC, expansion revenue — tracked from Day 1 because the business model demands it, and because SaaS hiring managers speak this language fluently.

---

## The Project: Nimbus

Project Nimbus is an end-to-end AI-assisted RevOps data pipeline, built as a unified governed system — not a collection of isolated tool demonstrations.

Every layer is observable, idempotent, and designed with regulatory auditability as a first-class constraint.

**Started:** April 20, 2026
**Pre-hire target:** April 2027 (Salesforce Admin cert + live GitHub repo)
**Firm launch horizon:** 2030–2031 (pending co-founder readiness)

---

## Positioning Statement

> Project Nimbus demonstrates end-to-end systems thinking across CRM, data infrastructure, AI governance, and SaaS metrics. It separates a candidate who has learned tools from one who understands why those tools exist and how they fail.

Most junior portfolios demonstrate automation. Nimbus demonstrates **controlled automation** — with a sovereign compliance intercept, enforced human accountability, and a closed-loop feedback system that improves over time.

---

## Core Differentiators

**End-to-end system integration**
The pipeline is a single governed system: Python ingestion → Snowflake → dbt → Salesforce FSC → Agentforce (cloud AI) → Local SLM Audit Intercept → HITL approval. No layer operates in isolation.

**Dual-layer AI governance**
Cloud AI (Agentforce) handles scale. A local SLM running on-device via Ollama acts as an independent compliance auditor before any draft reaches the human advisor. One generates. One evaluates. The human approves or rejects.

**Human-in-the-Loop by architecture, not by policy**
AI-generated outputs are held in a staging field and cannot dispatch until a human approval gate is explicitly cleared. Autonomous AI is not permitted at any client-facing stage.

**Auditability by design**
Quarantine logs, MODEL_AUDIT_LOG, SYSTEM_EVENTS, SLM_Audit_Grade__c, and approval timestamps are not added after the fact. They are structural requirements from Day 1.

**Idempotency as a production standard**
The pipeline can be rerun against any dataset without producing duplicates or corrupting state. MERGE semantics are enforced throughout.

**Closed-loop outcome tracking**
Every dispatched lead that returns an outcome becomes a training signal. The system learns. Phase 3 model retraining consumes real conversion data — not synthetic assumptions.

**FinOps governance at the infrastructure layer**
The Snowflake warehouse is hard-capped at 15 credits/month via Resource Monitor, with 60-second AUTO_SUSPEND. Budget overrun is architecturally impossible during the portfolio build.

---

## Strategic Career Roadmap

### Pre-Hire (Year 1 — April 2026 to April 2027)
Secure a junior Salesforce Admin or RevOps contract role through a staffing agency.

**Primary lane:** WealthTech / B2B SaaS
**Parallel lane:** HealthTech — the clinical governance philosophy and PharmD background translate directly. If WealthTech placement stalls, HealthTech activates immediately with no changes to the portfolio.

**Minimum viable credential for application:**
- Salesforce Certified Administrator
- Live Project Nimbus V1 repository on GitHub

Do not wait past April 2027 looking for more readiness. The first contract is the unlock for everything that follows.

### Post-Hire (Years 2–4)
40 hours/week outside work. Deep mastery of the data stack, ML layer, and Salesforce platform. One certification per quarter maximum — earned by someone who has built the system it validates.

### Firm Launch (2030–2031)
Co-found Tethered Wealth Advisors with CFP co-founder. Project Nimbus becomes the production system. Every architectural decision made during the portfolio build has a real business consequence.

---

## Pre-Hire Certifications

| Certification | Provider | Target |
|---------------|----------|--------|
| Salesforce Certified Administrator | Salesforce | Month 3 — hard requirement |
| Salesforce Platform App Builder | Salesforce | Month 4–5 — strong bonus |
| dbt Certified Developer | dbt Labs | Stretch — only after Admin + App Builder |

---

## Pre-Hire Reading

Three books maximum before hire. More is procrastination disguised as preparation.

- **Lean Analytics** — Croll. SaaS metrics, CAC, LTV, churn — directly informs Intent_Score design and interview vocabulary. ✅ Started
- **The WealthTech Book** — Chishti. Industry vocabulary and systemic friction points for the advisory firm context. ✅ Started
- **The Trusted Advisor** — Maister. The human element of implementing automation — relevant to both hiring interviews and eventual client relationships.

---

## Architecture Decision Records

Every significant technical decision is documented as an ADR in `/docs/adr/`. Written at the time of the decision — not post-hoc. Context, options considered, decision, consequences.

Over 12 months, 15–20 ADRs accumulate into a record of architectural judgment that no résumé can replicate. Each ADR is also a blog post and an interview talking point.

**Founding ADRs:**
- **ADR-001:** Snowflake over DuckDB — DuckDB retained for local prototyping; Snowflake chosen for MERGE semantics, Resource Monitor governance, and Salesforce Data Cloud compatibility
- **ADR-002:** Ollama (local) over Snowflake Cortex — sovereignty requirement: the compliance audit layer must be architecturally independent of cloud API availability
- **ADR-003:** HITL gate as Salesforce field lock, not Flow restriction — Flow restrictions are bypassable via API; field-level enforcement is the stronger constraint
- **ADR-004:** Outcome feedback loop designed at V1, not retrofitted — fct_lead_outcomes schema established before Phase 3 ML layer to ensure training dataset stability
- **ADR-005:** SYSTEM_VERSION metadata tag on every synthetic record — allows scoring engine iteration without warehouse purges; preserves full lineage

---

## The Repository as Résumé

> The project-nimbus GitHub repository is not a prototype that gets archived. It is a living technical product that grows in sophistication alongside the skills that built it.

Version tagging marks the progression: `v1.0` at Phase 1 completion, `v2.0` at Phase 2, forward indefinitely. The git history — daily commits, atomic messages, real content — becomes a résumé in itself. A record of deliberate, governed, compounding technical growth.

---

*Project Nimbus — Confidential Portfolio Document*
*Started: April 20, 2026 | Joshua Boeding*