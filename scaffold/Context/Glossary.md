# Glossary

Domain terms, status labels, and vault conventions for this vault.

---

## Healthcare

### Standards & data

- **HL7** - Health Level 7 messaging standard for clinical data exchange
- **LOINC** - Logical Observation Identifiers Names and Codes; standard codes for lab tests
- **ICD-10** - International Classification of Diseases, 10th rev. Diagnosis code set used on claims.
- **DSM-5-TR** - Diagnostic and Statistical Manual of Mental Disorders (Text Revision). Behavioral health diagnostic standard.
- **CPT** - Current Procedural Terminology. AMA-maintained procedure codes used for billing.
- **HCPCS** - Healthcare Common Procedure Coding System. CMS code set extending CPT (covers supplies, drugs, non-physician services).
- **EMR** - Electronic Medical Record system
- **EHR** - Electronic Health Record system
- **SFTP** - Secure File Transfer Protocol; common transport for HL7 batches

### Compliance & privacy

- **PHI** - Protected Health Information; covered by HIPAA
- **PII** - Personally Identifiable Information
- **BAA** - Business Associate Agreement; required to process PHI
- **HIPAA** - Health Insurance Portability and Accountability Act

### Billing / RCM

- **VOB** - Verification of Benefits. Pre-admission insurance check.
- **NPI** - National Provider Identifier. Unique 10-digit ID for healthcare providers.
- **EDI 837** - Electronic claim submission transaction.
- **EDI 835** - Electronic Remittance Advice (payment/adjustment from payer).
- **EDI 270 / 271** - Eligibility inquiry / response transactions.
- **AR** - Accounts Receivable
- **Encounter** - Single billable patient interaction (visit, session, group).

### Operations / clinical workflow

- **ALOS** - Average Length of Stay
- **Census** - Current count of admitted patients
- **Bed Day** - One patient occupying one bed for one day; primary BH revenue unit
- **Intake** → **Admission** → **Discharge** → **Aftercare** - Standard patient lifecycle stages
- **Treatment Plan / Master Treatment Plan** - Required clinical document outlining goals, interventions, measurable objectives
- **SOAP note** - Subjective / Objective / Assessment / Plan. Common clinical note format.
- **BIRP note** - Behavior / Intervention / Response / Plan. Common BH/SUD group-note format.
- **DAP note** - Data / Assessment / Plan. Condensed alternative to SOAP.

---

## Levels of Care (Behavioral Health / SUD / ED)

ASAM (American Society of Addiction Medicine) levels and common program types across substance use, eating disorder, behavioral health, and medication-assisted treatment settings.

- **Detox / Medical Detox** - Supervised withdrawal management. ASAM Level 3.7-WM or 4-WM depending on medical acuity.
- **Inpatient / Acute** - 24/7 hospital-based psychiatric or medical stabilization. ASAM Level 4.
- **Residential / RTC** - Residential Treatment Center. 24-hour clinically managed care. ASAM Levels 3.1, 3.3, 3.5, 3.7.
- **PHP** - Partial Hospitalization Program. Day-treatment, 5-7 days/week, 5-6 hours/day, client sleeps off-site. ASAM Level 2.5.
- **IOP** - Intensive Outpatient Program. 3-5 days/week, 3 hours/session. ASAM Level 2.1.
- **OP** - Outpatient. Standard weekly therapy/medical visits. ASAM Level 1.
- **Sober Living / SLE** - Sober Living Environment. Recovery-supportive housing, often paired with IOP/OP.
- **MAT** - Medication-Assisted Treatment. Buprenorphine, naltrexone, methadone for SUD.
- **OTP** - Opioid Treatment Program. Federally regulated methadone clinic (SAMHSA-certified).
- **ORP** - Office-based Opioid Treatment (e.g., buprenorphine prescribers outside an OTP).
- **Co-occurring / Dual Diagnosis** - Concurrent SUD and mental-health disorder treatment.

### Clinical conditions

- **SUD** - Substance Use Disorder
- **AUD** - Alcohol Use Disorder
- **OUD** - Opioid Use Disorder
- **ED** - Eating Disorder (context-dependent; not Emergency Department here)
- **AN / BN / BED / ARFID** - Anorexia Nervosa / Bulimia Nervosa / Binge Eating Disorder / Avoidant-Restrictive Food Intake Disorder
- **SMI / SPMI** - Serious Mental Illness / Severe and Persistent Mental Illness
- **MH** - Mental Health
- **BH** - Behavioral Health (umbrella: SUD + MH)

### Modalities

- **CBT** - Cognitive Behavioral Therapy
- **DBT** - Dialectical Behavior Therapy
- **EMDR** - Eye Movement Desensitization and Reprocessing
- **MI** - Motivational Interviewing
- **TF-CBT** - Trauma-Focused CBT

### Clinical roles & credentials

- **LCSW** - Licensed Clinical Social Worker
- **LMFT** - Licensed Marriage and Family Therapist
- **LPC / LMHC** - Licensed Professional Counselor / Licensed Mental Health Counselor (state-dependent name)
- **LCDC / LADC / CADC** - Licensed/Certified Chemical Dependency / Alcohol & Drug Counselor (state-dependent)
- **BHT** - Behavioral Health Technician (front-line client support, often residential)
- **RN / LVN / LPN** - Registered Nurse / Licensed Vocational/Practical Nurse
- **MD / DO** - Physician (Doctor of Medicine / Osteopathic Medicine)
- **Psychiatrist** - MD/DO specializing in mental health; can prescribe
- **Case Manager** - Coordinates services, discharge planning, external referrals
- **Peer Support Specialist** - Person with lived recovery experience, certified to support clients

### Regulatory / payer

- **SAMHSA** - Substance Abuse and Mental Health Services Administration
- **CARF / Joint Commission** - Accrediting bodies for treatment facilities
- **42 CFR Part 2** - Federal confidentiality regulation for SUD treatment records (stricter than HIPAA)
- **UR / UM** - Utilization Review / Utilization Management; insurance medical-necessity gating
- **LOC** - Level of Care
- **AMA** - Against Medical Advice (discharge type)

---

## Kipu-Specific

Product line per [kipuhealth.com](https://www.kipuhealth.com/):

- **Kipu EMR** - Behavioral Health EMR. Flagship product. Patient charting, documentation, clinical workflows, billing integration.
- **Kipu CRM** - Behavioral Health CRM. Admissions, business development, marketing, intake/referral management.
- **Kipu RCM** - Behavioral Health Revenue Cycle Management. Eligibility, verification of benefits, claims, patient payments, financial reporting.
- **Kipu GRC** - Governance, Risk, and Compliance. Accreditation tracking, policy management, staff training, task automation.
- **Kipu Intelligence Program** - AI capabilities embedded across the suite (smart phrases, AI charting assistance, analytics).
- **Kipu Avea** - Treatment outcomes / patient engagement product line.


---

## AI / Technology

- **LLM** - Large Language Model (e.g., Claude, GPT, Gemini)
- **RAG** - Retrieval-Augmented Generation. LLM pattern that fetches external context (vault notes, docs, DB rows) before generating output.
- **MCP** - Model Context Protocol. Open standard Cowork uses to connect agents to external data sources and tools (Slack, Outlook, Salesforce, custom MCP servers).
- **Agent** - LLM workflow with autonomy to plan, call tools, and act over multiple steps.
- **Skill** (Cowork) - Packaged capability the agent invokes for a domain (e.g., `obsidian-vault`, `kipu-health-standards`).
- **Connector** - User- or org-authenticated integration that gives Cowork live access to a data source.
- **Schedule** (Cowork) - Recurring agent task triggered on a cron-like cadence (requires the user's machine to be on).

---

## Business / Finance

- **ARR** - Annual Recurring Revenue
- **MRR** - Monthly Recurring Revenue
- **NRR** - Net Revenue Retention
- **EBITDA** - Earnings Before Interest, Taxes, Depreciation, and Amortization
- **NPS** - Net Promoter Score
- **OKR** - Objectives and Key Results
- **ELT** - Executive Leadership Team
- **CSM** - Customer Success Manager
- **CCO** - Chief Customer Officer
- **CTO** - Chief Technology Officer
- **CIO** - Chief Information Officer
- **CISO** - Chief Information Security Officer

---

## Status Labels

Used in YAML frontmatter on Projects, Bugs, Candidates, etc.

| Domain | Values |
|--------|--------|
| Project | `Active`, `In Progress`, `Completed`, `On Hold`, `Cancelled` |
| Candidate | `Interviewed`, `Offer Extended`, `Hired`, `Passed` |
| Bug | `Open`, `In Progress`, `Resolved`, `Closed` |

---

## Vault Folder Reference

- `Daily Notes/` - daily journal, scratchpad
- `Meeting Notes/` - dev syncs, ops reviews, customer calls
- `Projects/` - active initiatives with status and timelines
- `People/` - team members, peers, stakeholders
- `SOPs/` - standard operating procedures
- `Issues/` - bug reports, dashboards, operational issues
- `Tasks/` - running task list and archive
- `Templates/` - reusable templates for new notes
- `Context/` - reference files for Cowork (includes `Compliance.md` and `.scaffold-version.yaml` system files - don't manually edit those)

Optional (added by interview):

- `1on1s/` - per-direct-report folders for 1:1 prep and notes
- `Strategic Initiatives/` - top-level themes (OKRs, multi-quarter bets)
- `Stakeholders/` - external partners (board, investors, key customers)
- `Candidates/` - interview notes for open roles (created if you participate in hiring)
