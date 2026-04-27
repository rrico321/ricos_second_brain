# Approved Connectors

Status as of 2026-04-27. Update via PR when status changes.

## Approved (use freely)

- **Fathom** - meeting transcripts. Recently became a Cowork connector. Major unlock.
- **Microsoft 365** - SharePoint, OneDrive, Outlook
- **GitHub** - for engineering roles
- **Atlassian** - Jira, Confluence
- **NetSuite** - financial data, treat outputs as Confidential
- **Pendo** - product analytics
- **SmartSheet** - operational tracking
- **Vendr** - vendor management
- **Slack** - DMs, channels. Note: client channels often contain PHI - subject to BAA gap.

## Pending Security Approval

- **Zoom** - meeting recordings
- **n8n** - automation orchestration
- **Lucidchart** - diagramming
- **Docusign** - contract signing
- **Calendly** - scheduling

## Under Investigation

- **Custom MCP Server** - Rico evaluating for Salesforce / Gong / company-specific needs
- **Salesforce hosted MCPs** - Salesforce now publishes their own MCPs; faster than building custom

## Personal-only (not for Kipu data)

- Personal Gmail / iCloud / personal Slack workspaces - OK for personal data only

## Hard No (until BAA)

- Any connector that exposes PHI without BAA in place

## How to request a new connector

1. Open an issue in this repo describing the connector and use case
2. Loop in IT / Security
3. If approved, update this file via PR
