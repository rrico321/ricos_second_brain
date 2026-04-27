# COMPLIANCE.md - Org-Wide Guardrails

These rules apply to every user of this scaffold. The `CLAUDE.md` template references `Settings/Compliance.md` (a copy of this file in your vault) as a layered guardrail so the agent reads org rules before user-specific instructions.

## HIPAA and PHI

**Hard rule: no PHI in Claude until Anthropic Business Associate Agreement is signed.**

Protected Health Information (PHI) includes but is not limited to:
- Patient names, dates of birth, addresses, phone numbers, email addresses
- Medical record numbers, account numbers, health plan beneficiary numbers
- Diagnoses, treatments, prescriptions, lab results
- Any image, screenshot, or document containing the above

Until the BAA is signed, Cowork must NOT:
- Ingest PHI from any connector (Slack, Outlook, Salesforce, Zendesk, Gong, etc.)
- Store PHI in the vault
- Generate output containing PHI
- Process PHI through any LLM call

If Cowork detects content that may contain PHI:
- Refuse to ingest, store, or process it
- Tell the user clearly: "This appears to contain PHI. Per Kipu policy, I cannot process this until the Anthropic BAA is signed."
- Do not paraphrase or summarize PHI into a non-PHI form. Refusal is the only correct response.

PHI workflows that need AI processing must route through AWS Bedrock, which has a BAA via AWS.

## Data classification

| Class | Examples | Cowork posture |
|-------|----------|----------------|
| Public | Marketing copy, public docs | Free use |
| Internal | Project plans, SOPs, meeting notes without PHI | Free use within Kipu vault |
| Confidential | Salary, financials, vendor contracts, customer lists | Use with caution. Do not paste into shared channels. Do not include in connector outputs. |
| Restricted (PHI) | See above | Hard refuse until BAA signed |

## Connector posture

For Kipu work vaults:
- Prefer connectors routed through MCP servers with OAuth gating over personal connectors
- The Slack connector touches client channels with PHI - assume PHI exposure and act accordingly
- The NetSuite connector touches financial data - treat as Confidential
- Personal connectors (logged into the user's individual account) are OK for personal-tier data only

Approved connectors: see `docs/connectors-approved.md` in the repo.

## Output rules

- Always proofread anything Cowork drafts before sending. The user is the gatekeeper.
- Cowork is "thinking out loud" - the user decides what leaves the vault.
- Never auto-send emails. Always create drafts in `Drafts/` or in the email client for user review.

## When in doubt

- Ask the user before processing
- Refuse rather than risk
- Surface the concern explicitly
- Do not paraphrase sensitive content into a "safer" form. The original sensitivity remains.

## Versioning

This file is updated when policy changes. Once Anthropic BAA is signed, the PHI hard-rule will be replaced with a more nuanced policy reflecting BAA scope.

Last updated: 2026-04-27.
