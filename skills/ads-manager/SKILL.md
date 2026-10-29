---
name: ads-manager
description: Plan, audit, and change GLOBUS advertising in Google Ads, GA4, GTM, Search Console, and Instagram-only Meta. Use for campaigns, keywords, ads, landing pages, conversion tracking, and lead quality. Judge Atlas projects and money with the atlas-agent-tool skill, not with a separate CRM client.
---

# GLOBUS ads manager

Company rules and advertising standards for GLOBUS. Read the section the task needs. Do not load every reference up front.

Lead quality, project budgets, purchase totals, discard reasons, and project cards come from the `atlas-agent-tool` skill in this same repository. Do not reimplement Atlas login or the action catalog here. Ads and GA4 events show a form submission. Atlas shows the created project and, for Production, Shipping, and Completed, the money. Do not add those rows together.

## When to use

Audits and plans; keywords, ads, and assets; traffic and lead quality; conversions, GA4, GTM, and organic search; the Meta account. New Meta delivery is Instagram only.

## References

| Section | What it holds | Open it for |
|---|---|---|
| [Company](references/company.md) | Offer, buyers, qualification | Strategy and lead quality |
| [Claims](references/positioning-and-claims.md) | Tone and allowed promises | Copy, assets, landing pages |
| [Operating rules](references/operating-rules.md) | Approval, limits, report shape | Before any external change |
| [Campaigns](references/campaigns-and-markets.md) | Markets, settings, landing pages, Instagram | Creating or auditing campaigns |
| [Keywords](references/keywords.md) | Match types, seeds, negatives | Search terms |
| [Ads](references/ads-and-assets.md) | RSA, extensions, images | Creative |
| [Tracking](references/tracking-and-lead-quality.md) | Conversion roles, UTM, gclid | Measurement |
| [Accounts](references/accounts.md) | Account ids and how to call the APIs | Reading Google or Meta |
| [Checklist](references/policy-and-checklist.md) | Internal limits and self-check | Before a change is approved |

These files are the shared public skill. A chat does not rewrite them. A confirmed durable rule change is reported so a maintainer can update this repository. Do not store tokens, private keys, or staff logins here. Live account settings are read from the services, not assumed from an old audit.
