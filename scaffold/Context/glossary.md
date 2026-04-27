# Glossary

Domain terms, status labels, and vault conventions for this vault.

---

## Healthcare / Lab Integration

- **HL7** - Health Level 7 messaging standard for clinical data exchange
- **HL7 v2.x** - Pipe-delimited message format used for lab orders, results, and ADT events
- **OBX** - Observation/Result segment in an HL7 message
- **OBR** - Observation Request segment
- **ORC** - Common Order segment
- **PID** - Patient Identification segment
- **MSH** - Message Header segment
- **LOINC** - Logical Observation Identifiers Names and Codes; standard codes for lab tests
- **EMR** - Electronic Medical Record system
- **EHR** - Electronic Health Record system
- **SFTP** - Secure File Transfer Protocol; common transport for HL7 batches
- **PHI** - Protected Health Information; covered by HIPAA
- **PII** - Personally Identifiable Information
- **BAA** - Business Associate Agreement; required to process PHI
- **HIPAA** - Health Insurance Portability and Accountability Act

---

## Kipu-Specific

- **L-number** - Internal identifier for a lab interface (e.g., L-4821)
- **Falloff** - When an interface stops sending or receiving expected message volume
- **POSSIBLE_FALLOFF** - At-risk interface flagged for monitoring
- **LIVE** - Interface in production
- **BUILDING** - Interface in development
- **TESTING** - Interface in QA / E2E validation
- **Kipu Core** - Main EMR product
- **KipuLabs** - Lab interface product
- **Elevate** - Customer-facing AI brief tool

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
- `Candidates/` - interview notes for open roles
- `SOPs/` - standard operating procedures
- `Bugs & Issues/` - bug reports, dashboards, operational issues
- `Tasks/` - running task list and archive
- `Templates/` - reusable templates for new notes
- `Context/` - reference files for Cowork
- `Settings/` - system files (don't manually edit)

Optional (added by interview):

- `Decisions/` - decision journal
- `1on1s/` - per-direct-report folders for 1:1 prep and notes
- `Strategic Initiatives/` - top-level themes (OKRs, multi-quarter bets)
- `Stakeholders/` - external partners (board, investors, key customers)
