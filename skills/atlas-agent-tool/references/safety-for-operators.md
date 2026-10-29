# Safety for operators and bots

## Writes

- Every write goes through dry-run before apply. Today that write is `projects.addNote`.
- Do not apply in the same step as the dry-run.
- Show target, preview, warnings, and `operationId` before asking for confirmation. Silence is not confirmation.
- A prepared operation expires after 24 hours. Prepare it again. Do not extend it.
- Applying the same operation again returns `already_applied` and does not create a second note.

## Permissions

If an action is unavailable or a permission check fails, stop and explain. Do not bypass it with a raw edit or a different action.

- `actions.list` and `actions.describe` show only actions this actor may run. Describing a hidden name responds as an unknown action.
- `projects.addNote` requires `projects.canAddNotes` and a project the actor can see.
- `analytics.sources.summary`, `analytics.sources.projects`, `analytics.sources.recentApplications`, and `analytics.sources.discardReasons` require `utms.canSeeUTMList`.
- `analytics.clients.summary` and `analytics.clients.projects` require both `statistics.canSeeModule` and `purchases.canSeePurchases`.
- `analytics.projects.get` returns a visible project card. The attribution block stays empty without `utms.canSeeUTMList`. The commercial block stays empty until the actor has both client permissions and the project is in the Clients cohort. `unavailable` names the reason.
- Lead sections follow the same rule: a missing section permission makes that section `null` and lists the permission. Do not invent the missing text.
- SMM post actions require `smm.canSeeContents`.

The catalog is shared by the HTTP route and the `atlas-agent` CLI. It does not register tools on Atlas Manager or SMM bots. Website bots use the current Atlas session user from the conversation. Do not use a local CLI auth file in the website runtime.

## Refusals

Refuse or pause when:

- the action is not in `actions.list`;
- the person asks for a raw database edit, generic CRUD, price changes, permission changes, or deletion;
- the change would be a bulk edit;
- several projects match and the target is ambiguous;
- a permission check fails, including `Access denied`;
- dry-run has not been shown and explicitly confirmed;
- the answer would need a contact name, email, phone, or messenger the catalog removed;
- the person asks to treat a Sources budget (`orders.price`) as revenue.

## Local CLI

Read this only when the `atlas-agent` binary is on this machine. HTTP callers use [the HTTP client](http-client.md) instead. `atlas-agent login` does not create the Bearer session that route requires.

- `atlas-agent login --login <staff-login>` checks that the staff user exists in MongoDB and saves the login locally. No WeCom code is sent.
- The CLI trusts the operator who already has `MONGODB_CONNECTION_STRING`. Treat the config file and env as secrets.
- `atlas-agent whoami` reports the saved login and whether the user still resolves from MongoDB.
- `atlas-agent logout` removes the saved auth file and is safe to repeat.
- If local auth is missing or the user no longer exists, stop and ask the operator to run `atlas-agent login`.
- `atlas-agent projects add-note` refuses to run without `--dry-run`. Apply with `atlas-agent operations apply` after the preview is confirmed.
- Any other registered action is `atlas-agent run <action> --json input.json`.
