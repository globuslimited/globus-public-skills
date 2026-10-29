---
name: ads-manager
description: Run GLOBUS advertising end to end. Manage campaigns in Google Ads and in the Meta ad account (Facebook Ads Manager), analyze spend and conversions, and read the leads those campaigns produced in Atlas. New Meta placements are Instagram only. Use with the atlas-agent-tool skill. The operator supplies the API credentials.
---

# GLOBUS ads manager

This skill plus `atlas-agent-tool`, with the credentials the operator supplies, is the company instruction for advertising. Read only the section the task needs.

The two cabinets are Google Ads and the Meta ad account in Facebook Ads Manager. New Meta delivery is Instagram only: managing that account does not allow Facebook, Messenger, Audience Network, or Threads placements. Search Console, GA4, and GTM support measurement. They are not extra ad cabinets.

Atlas is where the lead arrives. Do not build a second CRM client. Use `atlas-agent-tool` for Sources, Clients, recent applications, and the project card. Ads and GA4 show a form event. Atlas shows the project and, for Production, Shipping, and Completed, the money. Do not add those figures together.

## Work

1. Read the live cabinets and, when the question is about leads or money, the matching Atlas period. Account ids and request shapes are in [accounts](references/accounts.md). The result order is in [tracking](references/tracking-and-lead-quality.md).
2. Judge a lead by the [company definition](references/company.md), not by a cheap form.
3. Change a campaign, keyword, ad, goal, or placement only after the [approval steps](references/operating-rules.md). Create new objects paused.

## When to use

Planning, creating, or changing campaigns in Google or Meta; audits and performance; keywords, ads, and landing pages; conversions and tracking; lead quality against Atlas.

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
