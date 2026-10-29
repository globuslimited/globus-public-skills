# HTTP client

Read this when calling `POST /api/atlas-agent/run` instead of the local `atlas-agent` CLI. Which module to open is in the skill entry: [Projects](projects.md), [Analytics](analytics.md), or [SMM](smm.md). Dry-run, apply, and refusals are in [safety](safety-for-operators.md).

This route runs the same catalog as the CLI. The CLI auth file is not accepted. A `login` field in the body is ignored. A client token is rejected. The actor is the staff user in the session, with that user's permissions and project visibility.

## Endpoint

```http
POST https://lambda.globus.furniture/api/atlas-agent/run
Authorization: Bearer <session-jwt>
Content-Type: application/json
```

## Session

There is no session until a staff user completes WeCom login. Both login calls go to Atlas API with no Authorization header. Production host: `https://api.globus.furniture`. The tRPC body is `{ "json": <input> }`. The useful payload is `result.data.json`.

1. Ask the person for their Atlas staff login. Do not guess it.
2. Request a code:

```http
POST https://api.globus.furniture/trpc/users.sendAuthCode
Content-Type: application/json

{ "json": { "login": "ivan" } }
```

A 6-digit code is sent to that staff user's WeCom. It does not appear in the agent chat. If `json` contains `error: "User doesn't exist or banned"`, stop and say so.

3. Ask the person to read the code from WeCom and send it. Do not guess codes. `users.auth` answers `Wrong login or code` for a bad code, and repeated failures ban the staff user. After one wrong code, ask again. Do not loop.
4. Exchange the code:

```http
POST https://api.globus.furniture/trpc/users.auth
Content-Type: application/json

{ "json": { "login": "ivan", "code": "123456" } }
```

Success is `{ "session": "<jwt>", "refreshToken": "<jwt>" }` inside `result.data.json`. Send `session` as `Authorization: Bearer`. Keep both values. Login is lowercased. The code is single-use.

`session` lasts 15 minutes. `refreshToken` lasts 30 days. On `{ "error": "Forbidden" }`, refresh before starting WeCom login again:

```http
POST https://api.globus.furniture/trpc/users.refreshSessionToken
Content-Type: application/json

{ "json": { "refreshToken": "<saved refreshToken>" } }
```

The response is a new pair. Discard the previous refresh token. If refresh fails, start again at `users.sendAuthCode`.

The Atlas `session` cookie is the same JWT, but it is httpOnly and is not sent to `lambda.globus.furniture`. Copying it from the browser cookie store is only a fallback when the person is already signed in. A query parameter `session` is rejected.

Local development only: `users.devStaffSession` with `{ "json": { "login": "<staff-login>" } }` returns the same pair. Outside development that procedure does not exist.

## Request

```json
{ "action": "actions.list", "input": {} }
```

`input` may be omitted; the route sends `{}`. Success is the action JSON itself, the same object the CLI prints. There is no wrapper. Failures are `{ "error": "<public message>" }`.

Call `actions.list` first. It returns only actions this actor may run: name, description, permissions, `read` or `write` risk, whether dry-run is required, and examples. Before an unfamiliar action, call `actions.describe` with `{ "name": "<action>" }`. A name this actor cannot run is reported as unknown, not as a missing permission.

## Errors

| Status | Body | What to do |
| --- | --- | --- |
| 403 | `Forbidden` | No usable staff session. Refresh the token, or start WeCom login. |
| 403 | `Access denied: missing <permission>` | This staff user cannot run the action. Stop and name the permission. Do not switch login in the body. |
| 403 | `User doesn't exist or is banned.` | The session login is no longer an active staff user. |
| 404 | `Unknown action: <name>` | The name is not in the catalog, or this actor may not run it. Call `actions.list` and pick a listed name. |
| 400 | `Invalid request` | The body is not JSON, or `action` is missing. |
| 400 | `Invalid input: ...` | Fix the input. Dates, page size, and required fields are in `actions.describe`. |
| 400 | `Project not found or not accessible: ...` | The id is invalid or this actor cannot see the project. Do not retry with a raw database read. |
| 400 | `Chat not found or not accessible: ...` | The chat id is invalid or not on a project this actor can see. |
| 400 | `Operation not found:` / `Operation expired:` / `Operation belongs to a different actor:` / `Operation is already being applied:` / `Unsupported operation action:` | The prepared write cannot be applied. If it expired, prepare a new dry-run. |
| 500 | `Action failed` | The server hid an internal error. Retry once. If it fails again, stop and report that the action failed. |

A repeated `operations.apply` of an operation that already succeeded returns `status: "already_applied"` with the stored result. That is not an error.
