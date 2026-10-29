# Conversions, tracking, and lead quality

Read the live conversion setup before acting. The roles below are the agreed scheme. A name in this file does not prove a campaign is optimizing on it.

## Roles

| Event | Role | Condition |
|---|---|---|
| EN - Project Estimate - 20261026 (`7872752384`) | Primary | Successful submit with `form_type=estimate`, one per click |
| EN - Catalog Request - 20261026 (`7872752387`) | Secondary | Successful contact submit with `form_type=catalog`, one per click |
| EN - Form Submit - 20261021 (`7860705488`) | Secondary, historical | Before the split this mixed form types. New EN events do not go here. Old conversions were not redistributed |
| Qualified Lead 20261021 | Secondary, offline import by gclid | Primary only if the operator decides. The guide is 30+ qualified leads a month |
| Website Calls 30s - 20261021 | Secondary | The operator decides whether calls enter optimization |
| WhatsApp, Telegram, and email clicks | Secondary, watch only | Do not optimize toward curious visitors |

Do not change roles or delete conversions unless that exact rule change is agreed. Also read biddable customer and campaign goals. A Primary name does not mean a given campaign bids on it.

Catalog stays a lead, and it is Secondary because the intent differs. A project estimate is Primary. That is an optimization hypothesis, not proof that catalog leads are poor. Both are worked in Atlas. Do not change bids, budgets, or campaign statuses as part of restating this rule.

EN GTM container `257478079` (GTM-PKTFQWFV), published version 15: tag 57 uses the Primary label and trigger 67 (`landing_lead_submit` and `form_type` exactly estimate). Tag 68 uses the Secondary label and trigger 50 (`form_type` exactly catalog). Other `form_type` values are not covered. Adding a type is a separate task. Publishing and reading the container are not a test that a form reached Atlas.

## How to read a period

Use one period for every system. If the operator does not name it, use the last three months, the same default as Atlas.

1. Google Ads on `3704066294`: spend, impressions, clicks, and conversions by campaign. Then the breakdown the question needs, such as search terms, geography, or day. Spend is `cost_micros` / 1,000,000, in USD.
2. Meta on `act_2523358247887690`: insights for the same period. Separate Instagram from any older Facebook, Messenger, or Audience Network delivery. Do not treat historical spend on those placements as the current plan. Spend in insights is already dollars.
3. GA4 or GTM only when the question is the form event or the tag, not the lead outcome.
4. Atlas, through `atlas-agent-tool`, for that same `start` and `end`:
   - `analytics.sources.summary` for applications and project budget by source.
   - `analytics.sources.recentApplications` when the question is the leads that arrived, newest first. `analytics.sources.projects` when the question is a filtered cohort.
   - `analytics.sources.discardReasons` when the question is why leads were discarded.
   - `analytics.clients.summary` when the question is purchase and profit. Those amounts are CNY.
   - `analytics.projects.get` for one project. `projects.snapshot` when the working picture is needed: notes, tasks, and recent messages that the actor is allowed to see. A missing section stays empty.
5. A qualified lead still means a real property, a whole project, and a budget from US$30,000. Atlas status alone does not prove that.

Google and Meta spend, a form conversion, a Sources budget (`orders.price`), and Clients revenue are four different numbers. Do not add them into one total. A gap between a form event and an Atlas project is not by itself a tracking failure: the clocks, windows, and attribution rules differ.

## Form, Atlas, and attribution

Applications and money are read with `atlas-agent-tool`, as above. Ads and GA4 show the form event.

Auto-tagging stays ON. Check it, and do not change the account setting on your own. The form stores gclid in a hidden field and sends it to Atlas.

UTM template for new Google campaigns:

`{lpurl}?utm_source=google&utm_medium=cpc&utm_campaign={campaignid}&utm_content={adgroupid}&utm_term={keyword}`

Before applying it, read the current URL parameters and tracking template so the link is not duplicated or broken.

That template is for Google only. Do not put `utm_source=google` on Instagram. Agree Instagram labels separately. An old Meta campaign aimed at clicks or profile visits does not set the project goal. Pixels on the account are not Primary.

An older source named a 90-day offline-import window after the click. Check the current window for the upload type before planning an import. The sales cycle in [company](company.md) means the optimization target is a qualified lead. Do not promise that a closed deal can be joined after the available window.

## How to judge a result

The main figure is the cost of a qualified lead from [company](company.md), not the cost of a form. A report separates applications, qualification, missing Atlas data, and cohorts that are too young. Cheap forms with no qualified enquiries are not success.

Before launch, the operator sends a test form. Check one successful submit, one firing of the right event, gclid, and that gclid reached Atlas. Reporting delay is normal. An aggregate report with too little data does not prove there were no duplicates. Do not submit a new form yourself unless that is the task.
