# Accounts and API access

Ids are lookup hints. Read the live account before acting. Access that worked once is not a permanent right.

Credentials stay with the operator. Do not print private keys, JWTs, access tokens, or refresh tokens. Do not copy them into this skill, a report, or a log. Do not put a token in a URL.

## Domains and Google Ads

- Domains: globus.world, globus-china.com, globus-home.com, globus-home.ru. Ad destinations are the approved list in [campaigns](campaigns-and-markets.md).
- Working Ads account: `3704066294`, Foshan Ma Wei Trading Co., Ltd., USD, Asia/Shanghai. Call it the working account. Do not treat that as proof ads are delivering.
- MCC seen with the globus.world and globus-china.com GA4 links: `2802725492`. Other known customer ids: `5405664148`, `6786175286`, `8601500339`, `4544937842`, `6631190662`, `8695489697`, `9560059170`. A GA4 link does not prove current Ads access.

## GA4

Account `accounts/68516000`, Globus.

| Property | Name |
|---|---|
| 314013017 | globus.world - GA4 |
| 314032624 | globus-china.com - GA4 |
| 544263683 | globus-home.com - GA4 |
| 544275263 | globus-home.ru - GA4 |
| 559397245 | globus-china.es - GA4 |

Use each property's time zone when comparing periods.

## GTM

Account `accounts/6000035223`, Globus.

| Container | Public id | Use |
|---|---|---|
| 30036551 | GTM-WGFW8CQ | globus.world |
| 30195334 | GTM-NQN4B4N | globus-china.com |
| 257478079 | GTM-PKTFQWFV | EN landing, globus-home.com |
| 257479020 | GTM-MTNQW27S | RU landing, globus-home.ru |
| 267605281 | GTM-KB4RGDNK | ES landing |

## Search Console

Property format: `sc-domain:<domain>`. globus.world and globus-china.com have been listed. globus-home.com and globus-home.ru were intentionally closed to indexing. Do not treat their absence as a fault, and do not create those properties unless the operator changes that strategy.

## Credentials the operator supplies

This skill does not contain secrets. The person using it provides them for the session. If a required secret is missing, ask. Do not search the machine for key files, and do not print the values.

| Secret | Use |
|---|---|
| Google service-account JSON | Ads, GA4, GTM, Search Console. Standard pointer: `GOOGLE_APPLICATION_CREDENTIALS` |
| Google Ads developer token | Header `developer-token` on every Ads request |
| Meta access token | Facebook Ads Manager / Marketing API. Accepted names if present: `META_ACCESS_TOKEN`, then `FACEBOOK_ADS_MANAGER` |

Atlas is not one of these keys. Its session comes from `atlas-agent-tool`.

## Google credentials

Sign a JWT bearer against `https://oauth2.googleapis.com/token`. Do not write the key to a world-readable file. Delete any temporary key file as soon as the signature is made.

Scopes that have been used for reading:

- `https://www.googleapis.com/auth/adwords`
- `https://www.googleapis.com/auth/analytics.readonly`
- `https://www.googleapis.com/auth/tagmanager.readonly`
- `https://www.googleapis.com/auth/webmasters.readonly`

Writing needs its own scopes and a separate agreement.

| Service | Endpoint |
|---|---|
| Ads search | `https://googleads.googleapis.com/{version}/customers/{customer_id}/googleAds:search` |
| Ads change | `https://googleads.googleapis.com/{version}/customers/{customer_id}/googleAds:mutate` |
| Ads discovery | `https://googleads.googleapis.com/{version}/customers:listAccessibleCustomers` |
| GA4 Admin | `https://analyticsadmin.googleapis.com/v1beta/...` |
| GA4 Data | `https://analyticsdata.googleapis.com/v1beta/properties/{property_id}:runReport` |
| GTM | `https://tagmanager.googleapis.com/tagmanager/v2/accounts/{account_id}/containers/{container_id}/...` |
| Search Console | `https://www.googleapis.com/webmasters/v3/sites/{encoded_site_url}/searchAnalytics/query` |

Check which Ads API version the server accepts. Do not freeze an old version number. Send `developer-token` on every Ads call. When the call is for the working client under the MCC, also send `login-customer-id: 2802725492`. Customer ids in the path have no dashes.

Use `googleAds:search` to read campaigns, ad groups, ads, keywords, search terms, geo, and metrics. Divide `cost_micros` by 1,000,000. A `change_event` query needs a bounded `change_event.change_date_time`. Maximize Clicks has appeared as `bidding_strategy_type = TARGET_SPEND`.

Use `googleAds:mutate` only for a change the operator has approved. Create campaigns, ad groups, and ads with status `PAUSED`.

Encode `sc-domain:example.com` as `sc-domain%3Aexample.com` in the Search Console path. Discovery does not prove a later read or write will succeed. A TLS or DNS error is not a bad key.

## Meta, Instagram only

Placements are Instagram only. See [campaigns](campaigns-and-markets.md).

Use the Meta token the operator provided. Do not print it. Do not treat possession of the token as permission to write. Changes still follow the [operating rules](operating-rules.md).

Reading ads needs `ads_read`. An agreed change needs `ads_management`. Do not use message, content-publishing, comment, or catalog scopes unless the task asks for them.

Read and manage objects on the ad account: `act_{id}/campaigns`, `act_{id}/adsets`, `act_{id}/ads`, and `act_{id}/insights`. Create new campaigns, ad sets, and ads with `status` `PAUSED` and `publisher_platforms` set to `instagram` only. A Facebook page may be the ad identity. That does not add Facebook as a placement.

| Object | Id |
|---|---|
| Ad account | `act_2523358247887690`, USD, America/Los_Angeles |
| Business | Globus, `151527897285347` |

Call `https://graph.facebook.com/{version}/...` and check the version. Do not freeze one. Account status `1` has meant ACTIVE. An empty `me/businesses` does not remove the business nested on the ad account.
