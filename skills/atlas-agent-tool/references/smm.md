# SMM

SMM posts and their metrics. All three methods require `smm.canSeeContents`.

These methods do not answer whether advertising produced projects and money. That question belongs to [Analytics](analytics.md).

Other inputs are in `actions.describe`.

## smm.posts.search

Search posts. The useful filters are the publish window (`publishedFrom`, `publishedTo`), `platforms`, `channelIds`, `tagIds`, `query`, `state` (`DRAFT`, `QUEUE`, `PUBLISHED`, `ERROR`), and `linkStatus` (`linked`, `unlinked`, `invalid`, `any`). `limit` is at most 100.

## smm.posts.getPerformance

One post and its current platform metrics. Input is `{ "postId": "<id>" }`.

## smm.analytics.summarize

A summary for a publish-date window. `publishedFrom` and `publishedTo` are required. `includeRows` and `limitRows` (at most 100) add the post rows.
