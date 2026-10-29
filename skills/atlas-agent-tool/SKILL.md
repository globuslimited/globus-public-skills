---
name: atlas-agent-tool
description: Operate the atlas-agent CLI or POST /api/atlas-agent/run through action discovery, inspection, dry-run, and apply. Use for bot/operator workflows, not package implementation. For GLOBUS advertising results and incoming leads, pair it with the ads-manager skill.
---

# Atlas Agent Tool

Use this skill to read and change Atlas data through the action catalog. One request runs one action. Do not open Atlas in a browser to fetch something a method already returns. Do not invent methods or fields. Call `actions.describe` before an unfamiliar method.

This skill is not the source of truth for package layout or implementation. The live contract is `actions.list` and `actions.describe`.

The catalog is the same over HTTP and the local `atlas-agent` CLI. It is not an Atlas Manager tool and not an SMM bot tool.

GLOBUS advertising decisions — which campaign to change, what a qualified lead is, and how to read Google and Meta next to these numbers — live in the `ads-manager` skill. This skill supplies the Atlas read: Sources, recent applications, discard reasons, Clients, and the project card.

## Modules

Open the reference for the Atlas module you are in. Each file describes that module's methods.

- **Projects** — find a project, open the manager's working picture, and prepare an internal note. Methods: `references/projects.md`.
- **Analytics** — judge whether advertising produced projects and money, on the Sources and Clients screens. Methods: `references/analytics.md`.
- **SMM** — search posts and read post metrics. This does not answer the advertising question. Methods: `references/smm.md`.

`operations.apply` is not its own module. It commits a prepared write. Today the only write is `projects.addNote`, and that method is documented with Projects.

## Calling a method

- **HTTP session, body, and errors**: `references/http-client.md`
- **Local CLI**, only when the `atlas-agent` binary is on this machine: the CLI section of `references/safety-for-operators.md`
- **Writes, permissions, and refusals**: `references/safety-for-operators.md`

`actions.list` with `{}` returns the methods this actor may run. `actions.describe` with `{ "name": "<method>" }` returns that method's input and output.
