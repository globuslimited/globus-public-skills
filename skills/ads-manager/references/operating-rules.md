# Operating rules

## Priority

Account safety, then qualified leads, then the agreed budget. Reply in the operator's language. Write ads in the language of the market and the landing page.

Company rules, a live account reading, and a statement about Google or Meta are different things. Do not present an unchecked claim as a fact. The operator's current instruction wins. A clear yes is enough; do not demand the word APPROVE.

The advertising budget is not stored in this skill. Use the amount and split the operator has agreed. Budgets observed in an account are not that limit.

## What an agent may do

Read, search, diagnose, and report without a separate approval. That includes Google, Meta, and Atlas reads through [atlas-agent-tool](../../atlas-agent-tool/SKILL.md).

Changing this skill does not permit a change in Ads, GA4, GTM, Search Console, Meta, or Atlas.

## External changes

1. Read the entities the change touches.
2. Show a table: entity, field, current value, proposed value, reason.
3. Apply the relevant items in the [checklist](policy-and-checklist.md). Name risks and unknowns.
4. Get an explicit yes for that exact plan. Do not ask again for a yes already given.
5. Do only what was agreed.
6. Read the changed entities again and report the actual result. If part of the plan remains, list it. Do not widen the plan.

An Atlas note is a dry-run in `atlas-agent-tool`. Show the preview and wait for an explicit yes before apply. Do not work around `Access denied`.

## Defaults

- Create new campaigns, ad groups, and ads, including Meta, as PAUSED. A person enables them in the interface.
- Meta delivery is Instagram only. Do not add `facebook`, `messenger`, `audience_network`, or `threads` to `publisher_platforms`. A Facebook page used as the ad identity does not allow Facebook placements. Do not copy or enable old campaigns that use other placements.
- Do not create test, sandbox, template, or "do not enable" campaigns in the working account. PAUSED does not skip content review.
- Do not on your own change statuses, budgets, countries, languages, campaign types, bids, conversion goals, or Meta placements. Do not file appeals.
- Leave account settings alone: time zone, currency, billing, access, auto-tagging, shared negative-list links, Primary roles, and conversion deletion. If a task needs an exception, show the conflict and agree both the rule change and the action.
- Deleting campaigns, groups, keywords, or assets needs an explicit yes that lists what will be deleted.
- Do not create a new ad account, and do not suggest routing around a block through another account, payment profile, or domain.

## How to answer

For a change: what you understood, what you read, the plan table, the checklist, risks, and the request for a yes. Afterward: what changed and what the second read showed.

For an audit or report: the conclusion, the data you checked, the limits, and the recommendations. Do not invent changes. If a missing fact would change the action, ask; keep reading what you can.
