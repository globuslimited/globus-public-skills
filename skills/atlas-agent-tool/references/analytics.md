# Analytics

Whether advertising produced projects and money. This is the Sources screen and the Clients screen, not SMM post metrics. Post metrics are in [SMM](smm.md).

Always pass `start` and `end` as ISO date-times. `end` before `start` is `Invalid input: end is before start`. When the person does not name a period, use the last 3 months, matching the Atlas Analytics screens.

Sources count projects by created date and first-touch UTM. Clients are only Production, Shipping, and Completed.

`analytics.sources.*` requires `utms.canSeeUTMList`. `analytics.clients.*` requires both `statistics.canSeeModule` and `purchases.canSeePurchases`.

Optional filters (`country`, `manager`, `source`, `medium`, `group`, `campaign`, `content`, status) are in `actions.describe`. Two of them change the question:

- `group` is one of `seo`, `cpc`, `ai`, `smm`, `video`, `referral`, `other`.
- `attributionMode: "marketingRoi"` keeps known advertising sources and drops direct or unmapped traffic. The default `discovery` includes every attributed project.

Paged methods return `rows`, `total`, `page`, and `pageSize`. `pageSize` max is 100. Request the next page while `page * pageSize < total`. Do not treat one page as the whole period. Period totals come from a summary method, or from reading every page.

Read the numbers this way:

- Sources `budget` is `orders.price`, the project budget, not purchase revenue. `analytics.sources.summary` includes `currencyNote`: `budget is orders.price, not purchase revenue`. Say that.
- Clients `purchaseTotal` and `netProfit` are CNY, the same values the Clients screen returns.
- Do not add a Sources budget to a Clients revenue figure, and do not call the budget revenue.
- Rows never include contact names, emails, phones, or messengers.
- A project this actor cannot see is `Project not found or not accessible`, not an empty card.

A usual read is summary, then the project list or the newest applications, then discard reasons, then Clients, then one project.

## analytics.sources.summary

Channel counts and budget for the period. Budget totals are `orders.price`.

## analytics.sources.projects

Projects in that cohort: status, client id, budget, country, managers, source, medium, campaign, content, and discard reason. Same filters as the summary, plus paging.

## analytics.sources.recentApplications

The same cohort, newest `created_at` first. Sort is fixed. Use this when the question is the latest applications, not a campaign comparison. Rows add campaign labels for google/cpc, term, landing URL, Google click id, post link, and marketing note.

## analytics.sources.discardReasons

Why Discarded projects in the cohort were discarded. Same period and source filters as the summary. Not paged.

## analytics.clients.summary

Purchase totals and net profit for Production, Shipping, and Completed projects. Requires both client permissions. Does not take `page` or `pageSize`.

## analytics.clients.projects

The projects behind that Clients summary. `purchaseTotal` and `netProfit` are CNY. Budget on the row is still `orders.price`.

## analytics.projects.get

One visible project: who it is, where it came from, and what it returned. Input is `{ "projectId": "<id>" }`. The action itself has no extra permission.

- `project` is the identity and is returned when the project is visible.
- `attribution` is the first touch. It is present only with `utms.canSeeUTMList`.
- `commercial` is purchase, profit, and budget in CNY. It is present only with both client permissions and only when the project is in the Clients cohort.
- `unavailable` names a missing block: `missing_permission` (with `permission`) or `outside_client_cohort`.

No block means no numbers. Do not treat a missing block as zero.
