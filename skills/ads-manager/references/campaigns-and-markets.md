# Campaigns, markets, and landing pages

These are the project standards, not a snapshot of live settings. Changes follow [operating rules](operating-rules.md).

## Markets and language

| Market | Geography | Language |
|---|---|---|
| United States | California, Florida, Texas, New York City | EN |
| United Kingdom | Greater London, South East England | EN |
| Spain | Province of Málaga, Balearic Islands | EN |

Madrid is not part of the English Spain plan. A future Spanish-language campaign needs an approved Spanish landing page. New countries, regions, and languages need agreement. UK copy uses British spelling. An English campaign in Spain stays in English. Spanish ads are written in natural Spanish after the landing page is approved.

## Budget

This skill stores no standing amount or split. Use the operator's current agreement. If there is none, ask before a budget plan or a budget change. An extra campaign stays inside the agreed total. Do not restore an old split from a previous brief, including funding a brand campaign from one country. When turning a monthly budget into a daily budget, account for rounding and Google's current charging rules. A daily budget is not a hard cap on that day's spend.

## Default settings

| Setting | Standard |
|---|---|
| Type | Search. Other types are a separate decision |
| Networks | Google Search. Search partners OFF, Display OFF |
| AI Max | OFF |
| Automatically created assets, final URL expansion | OFF |
| DSA and campaign-level broad match | Do not use |
| Location targeting | PRESENCE for both targeting and exclusions |
| Language | One per campaign, the same as the landing page |
| Structure | Campaign = country or region group + language + its own budget |
| Bidding | Maximize Conversions on the primary conversion |
| tCPA | Not before 30+ conversions a month for two months in a row, and only with agreement |
| Devices | All. No device adjustments for the first 30 days |
| Rotation | Optimize |

## Names and ad groups

New names use Latin letters. Do not rename existing objects without a task.

- Campaigns: `SRCH_{COUNTRY}_{LANG}_{Theme}_{YYYYMMDD}`, for example `SRCH_UK_EN_WholeHome_20261101`.
- Ad groups: `AG{n}_{Theme}`, for example `AG2_ChinaSourcing`.
- Assets: `GLB_{type}_{theme}_{YYYYMMDD}`.

| Group | Intent | Audience |
|---|---|---|
| AG1_WholeHome | Furnishing a home | Private owners |
| AG2_ChinaSourcing | Buying through an agent in China | Designers, architects, developers, ready buyers |
| AG3_Villa | Furnishing a villa | Villa owners |
| AG0_Brand | Searches for GLOBUS | People who already know the company |

AG0_Brand may be its own small campaign if agreed. At least one RSA per ad group. Other brands are a separate case in [keywords](keywords.md).

## Landing pages

- EN: https://globus-home.com/ with anchors `#projects`, `#estimate`, `#quality`, `#process`, `#ways`, `#factory-videos`.
- RU: https://globus-home.ru/ — confirm before the first use.
- ES: no approved URL. Ask the operator. A GA4 property or a GTM container for ES does not approve a landing page.
- Do not use globus.world, or a page on it, as an ad destination, a sitelink, or a link from an ad landing page.
- The display domain matches the final URL. No shorteners and no cross-domain redirects. Check the final address, the page content, and that the anchors exist.

## Schedule

The first 30 days run all day. After that, the target window is 08:00–23:00 local, only if agreed. For the US, a source suggested one window from 08:00 Eastern to 23:00 Pacific. That is wider than 08:00–23:00 in each region, so show that before using it.

The Google Ads account time zone is Asia/Shanghai. Convert the agreed local window into that zone for the actual dates, including the day shift and daylight saving. Do not treat sample DST dates from an old brief as permanent. After writing the schedule, convert it back. If it misses the agreed time through 23:00 local, fix the plan. A schedule changes delivery and spend. Do not promise that the budget will be spent evenly.

Examples in Asia/Shanghai (UTC+8):

| Window | Account hours |
|---|---|
| US, EST/PST combined | 21:00–24:00 and 00:00–15:00 |
| US, EDT/PDT combined | 20:00–24:00 and 00:00–14:00 |
| UK, GMT | 16:00–24:00 and 00:00–07:00 |
| UK, BST | 15:00–24:00 and 00:00–06:00 |
| Spain, CET | 15:00–24:00 and 00:00–06:00 |
| Spain, CEST | 14:00–24:00 and 00:00–05:00 |

A year-round wide US window from the source is 20:00–24:00 and 00:00–15:00. Use it only when agreed, and show the local hours.

## Meta: Instagram only

The market table above is the project target, not the geography of old Meta campaigns. Account ids are in [accounts](accounts.md).

- Deliver only on Instagram. Do not include Facebook, Messenger, Audience Network, or Threads.
- Create new campaigns PAUSED and agree them under the [operating rules](operating-rules.md). Observed budgets and old click or profile-visit goals are not the standard.
- Landing pages are the same as Search. Do not use globus.world. Do not copy the Google UTM template onto Instagram. Agree Instagram labels separately. See [tracking](tracking-and-lead-quality.md).
- This ad account's time zone is America/Los_Angeles. Do not reuse a window calculated for Google Ads in Asia/Shanghai.
- In the Marketing API, `daily_budget`, `lifetime_budget`, `amount_spent`, and `min_daily_budget` are US cents. `insights.spend` is already in dollars.
