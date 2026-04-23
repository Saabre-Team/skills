# Connectors — Brakson Skills

This file documents the optional MCP connectors referenced by skills in this library.
When a connector is not installed, the skill works in "standalone mode" using pasted data and web search.

---

## How connectors work

Skills reference connectors with the `~~connector-name` syntax.
If that connector is not active in your session, Claude ignores those lines automatically.

---

## Available connectors (install as needed)

| Connector | Skills that use it | What it unlocks |
|---|---|---|
| `~~product analytics` | metrics-review, analyze, synthesize-research | Pull usage data and funnel metrics directly |
| `~~user feedback` | synthesize-research, research-synthesis, ticket-triage | Pull support tickets, NPS, and feature requests |
| `~~knowledge base` | customer-research, kb-article, draft-response | Search internal docs and prior tickets |
| `~~meeting transcription` | synthesize-research, call-summary, sprint-planning | Pull interview recordings and meeting summaries |
| `~~crm` | account-research, call-prep, pipeline-review, forecast | Pull account data and deal history |
| `~~email` | draft-outreach, call-summary, daily-briefing | Read and send emails |
| `~~calendar` | daily-briefing, call-prep, sprint-planning | Access upcoming meetings |
| `~~analytics` | seo-audit, performance-report, campaign-plan | Pull GA4, Search Console, or ad platform data |

---

## Installing connectors in Claude Cowork

1. Open Claude Cowork
2. Click **Plugins** in the sidebar
3. Search for the connector you want (e.g. "Google Analytics", "HubSpot")
4. Click **Install** — no configuration required for most connectors

---

## Running without connectors

All skills in this library work without any connector.
You can always paste your data directly into the chat — CSV exports, copy-pasted tables, or text summaries all work fine.

---

*Last updated: April 2026 — Brakson Skills v1*
