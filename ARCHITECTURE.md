# Project Nimbus — System Architecture

> Built for: **Tethered Wealth Advisors** — AI-forward wealth advisory for expatriates
> Repository: `project-nimbus`
> Status: 🟡 Phase 0 — Environment setup and foundational learning
> Started: April 20, 2026

---

## System Overview

Project Nimbus is a fully governed, end-to-end RevOps data pipeline. It is designed as a single integrated system — not a collection of isolated tools. Every layer connects to the next with explicit contracts, audit trails, and human control points.

```
Synthetic Data / Future Live Sources
            │
            ▼
    [ Ingestion Layer ]
    validate_leads.py
    UUID + timestamp assignment
    Pre-load schema validation
    Quarantine log (failures)
            │
            ▼
    [ Warehouse Layer ]
       Snowflake
    nimbus_wh (15 credit/mo cap)
    MERGE upsert — idempotent
            │
            ▼
  [ Transformation Layer ]
          dbt
    stg_leads → dim_clients
    fct_lead_scoring
    schema.yml contracts
            │
            ▼
    [ CRM Layer ]
   Salesforce FSC
   Record-Triggered Flow
   Custom fields + objects
            │
            ▼
  [ Cloud AI Draft Layer ]
      Agentforce
   Personalised outreach draft
   Stored in staging field
   NOT visible until audit clears
            │
            ▼
[ Local SLM Governance Layer ]
     Ollama (Llama 3)
     RTX 3060 — on-device
  Independent compliance audit
  JSON grade → Salesforce REST
            │
            ▼
   [ Human-in-the-Loop Gate ]
  Human_Approval_Status__c
  Advisor reviews draft + grade
  Approves or rejects — no bypass
            │
            ▼
      [ Dispatch ]
   Email sends only on approval
   Outcome written back to SF
   Nightly sync → Snowflake
   Closes the feedback loop
```

---

## The Firm Context: Tethered Wealth Advisors

Tethered Wealth serves expatriates navigating cross-border wealth management. This context justifies every architectural decision:

- **Local SLM governance** — client data never leaves the device for compliance checks; sovereignty is a fiduciary requirement
- **HITL enforcement** — no autonomous AI action on client assets; regulatory and trust requirements demand human sign-off
- **Subscription tiers** — Core, Premium, Concierge — drive SaaS metrics (MRR, churn, LTV, CAC) tracked from Day 1
- **Multi-jurisdiction awareness** — KYC, AML, FATCA, FBAR vocabulary baked into data models from the start

---

## Layer-by-Layer Breakdown

### 1. Ingestion & Idempotency Layer
**Tool:** Python (`validate_leads.py`)

- Synthetic records generated via Faker (Phase 1); real sources via Fivetran (Phase 2+)
- UUID + Created_At timestamp assigned at generation — every record traceable to origin
- Pre-load validation: catches malformed emails, null required fields, out-of-range values before warehouse contact
- Failed records written to `quarantine_log.csv` with failure reason and timestamp
- Upsert via Snowflake MERGE — fully idempotent, reruns produce no duplicates

### 2. Warehouse Layer
**Tool:** Snowflake

- Warehouse: `nimbus_wh`
- AUTO_SUSPEND: 60 seconds — idle compute cannot accumulate
- Resource Monitor: hard-capped at 15 credits/month (~$30 max)
- Every query tagged by pipeline component for cost attribution
- MERGE semantics enforced throughout — no INSERT-only patterns

### 3. Transformation Layer
**Tool:** dbt

| Model | Purpose |
|-------|---------|
| `stg_leads` | Cleans raw data, standardises formats, casts types |
| `dim_clients` | Flattens household and asset dimension data |
| `fct_lead_scoring` | Computes Intent_Score and Priority_Signal |
| `fct_lead_outcomes` | Joins scores to real outcomes — model training dataset |

**Intent Score Formula:**
```
Intent_Score = (0.30 × Page_Visit_Count)
             + (0.40 × e^(−0.05 × Days_Since_Last_Touch))
             + (0.30 × AUM_Tier_Score)

Priority_Signal = 'High' if Intent_Score ≥ 85
```

**Schema contracts (`schema.yml`):**
- `not_null` on Lead_ID and Email
- `unique` on Lead_ID
- `accepted_values` on Wealth_Tier: Core, High Net Worth, Ultra High Net Worth
- Custom regex test on Email format

### 4. CRM Layer
**Tool:** Salesforce FSC

- Record-Triggered Flow fires when `Priority_Signal = 'High'`
- Custom objects: `Agentforce_Response__c`, `SLM_Audit_Grade__c`, `Human_Approval_Status__c`, `Lead_Outcome__c`
- Subscription tier objects aligned to Tethered Wealth advisory model
- FSC household and financial account model for expat client structure

### 5. Cloud AI Draft Layer
**Tool:** Agentforce (Einstein Trust Layer)

- Drafts personalised, compliance-aware outreach email on Priority_Signal trigger
- Draft stored in `Agentforce_Response__c` — staging field only
- Not visible to advisor, not dispatchable until full audit chain completes
- Einstein Trust Layer: no customer data used for model training

### 6. Local SLM Governance Layer
**Tool:** Ollama (Llama 3) — RTX 3060, 12GB VRAM

This layer is architecturally sovereign from the cloud AI layer. It cannot be bypassed by cloud API timeouts or standard user configuration.

**Audit flow:**
1. Python script pulls Agentforce draft from Salesforce via SOQL
2. Draft passed to local Llama 3 configured as strict compliance auditor
3. SLM checks for: hallucinated tax rates, unsubstantiated financial guarantees, missing fiduciary disclaimers, jurisdiction-specific language violations
4. Returns structured JSON: `{ compliance_pass: bool, flags: [...], confidence: float }`
5. Python script pushes grade to `SLM_Audit_Grade__c` via Salesforce REST API
6. Grade surfaces on advisor FlexiPage alongside draft

> Cloud AI generates at scale. Local AI governs with sovereignty. Human decides. This separation is deliberate and architecturally enforced.

### 7. Human-in-the-Loop Gate
**Mechanism:** Salesforce field lock on `Human_Approval_Status__c`

- Must be set to `'Approved'` before any email dispatches
- SLM audit grade informs the decision — it does not replace it
- Implemented as field-level enforcement, not Flow restriction (ADR-003)
- Every approval carries a timestamp and advisor ID — full audit trail

### 8. Closed-Loop Outcome Tracking
**Why it matters:** Without outcome data, Intent_Score has no feedback. With it, the system learns.

- `Lead_Outcome__c` field on Salesforce Lead object: Contacted / Responded / Converted / Disqualified
- Nightly sync: Salesforce → Snowflake `fct_lead_outcomes` via scheduled Python script
- `fct_outcome_analysis` dbt model joins Intent_Score to Lead_Outcome
- Conversion rate by score decile queryable from Day 1
- Phase 3 retraining consumes this as training dataset

---

## Phase 1 KPIs

All must be green before agency outreach begins.

| KPI | Target | Validation |
|-----|--------|-----------|
| Duplicate lead rate | 0% | MERGE + UUID uniqueness |
| dbt test pass rate | ≥ 99% | schema.yml contracts |
| Quarantine rate | < 1% | Faker quality baseline |
| Scoring coverage | 100% | fct_lead_scoring completeness |
| High-Priority rate | 8–15% | Realistic wealth distribution |
| Agentforce latency | < 30 sec | Invocation timeout monitoring |
| SLM audit latency | < 2 sec | RTX 3060 inference benchmark |
| SLM grade written | 100% of drafts | SLM_Audit_Grade__c populated before HITL render |
| HITL queue depth | 0 at day end | Approval loop must not stall |
| FinOps compliance | 0 incidents | Resource Monitor hard-cap enforced |
| Pipeline errors | < 1 per 1,000 | dbt run results logged to MODEL_AUDIT_LOG |
| Outcome field population | 100% dispatched | Written back within 48h of dispatch |

---

## Repository Structure

```
project-nimbus/
├── README.md
├── VISION.md
├── ARCHITECTURE.md
├── docs/
│   └── adr/
│       ├── ADR-001-snowflake-over-duckdb.md
│       ├── ADR-002-ollama-over-cortex.md
│       ├── ADR-003-hitl-field-lock.md
│       ├── ADR-004-outcome-loop-at-v1.md
│       └── ADR-005-system-version-tag.md
├── ingestion/
│   ├── validate_leads.py
│   └── quarantine_log.csv
├── dbt/
│   ├── models/
│   │   ├── staging/
│   │   ├── dimensions/
│   │   └── facts/
│   └── schema.yml
├── salesforce/
│   ├── flows/
│   └── objects/
├── governance/
│   └── slm_audit.py
├── salesforce_admin/
│   └── notes/
├── excel/
│   └── notes/
├── modern_data_stack/
│   └── notes/
└── daily_log.md
```

---

## Future Stack Horizon

*Not scheduled. A map of what comes after mastery.*

- **Multi-agent LLM** (CrewAI, AutoGen) — specialised agents for research, drafting, compliance in sequence
- **Client-facing React portal** — TypeScript/React surfacing financial health scores, built on Snowflake, authenticated via Salesforce
- **Streaming data** (Kafka/Redpanda) — real-time intent signals; deferred until batch scoring is demonstrably a bottleneck
- **Fine-tuned domain LLM** — trained on expat advisory content and compliance language
- **Open source extraction** — KYC document parser, expat intent scoring model, compliance HITL pattern published as standalone libraries

---

*Project Nimbus — Architecture Document*
*Started: April 20, 2026 | Joshua Boeding*
*Status: Living document — updated as the system evolves*