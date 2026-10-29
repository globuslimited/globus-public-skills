# Projects

The project a manager works: search, the card, the working picture on the project page, and an internal note.

A hidden or invalid project id is `Project not found or not accessible`. If several search hits could be the one the person means, stop and ask. Do not pick the first match silently.

Paged methods take `page` from 1 and `pageSize` from 1 to 100, default 20. The response has `rows` and `total`. Request the next page while `page * pageSize < total`.

Contacts are removed throughout this module. Do not fill in a name, email, phone, or messenger from somewhere else.

## projects.search

Search projects this actor can see by project id, name, or client id.

`query` is required. `limit` is 1–20 and defaults to 10.

## projects.get

Load the normalized card: name, status, managers, country, city, client id, description, and dates. This is not the advertising outcome. For source and money, use `analytics.projects.get` in [Analytics](analytics.md).

## projects.snapshot

Open the same first screen the manager sees: the card, latest notes, open tasks, recent completed tasks, related IM chats with a short last message, recent emails, and recent project-room messages. The limits are hard. This is not the full history. The action itself has no extra permission.

A section the actor cannot read is `null`. `unavailable` names the permission and contains no counts or text. Do not fill that gap with zeros or invented notes.

Start here when judging a lead, then page the section that was cut off.

Quotations, favorites, documents, purchases, and QC are not in this picture.

## projects.notes.list

Page manager notes, newest first. Requires `projects.canSeeNotes`. A leave request keeps description and source. Name and contact are omitted.

## projects.tasks.list

Page tasks. Requires `tasks.canSeeTasks`. `status` is `open` (current), `done` (completed), or `all`. Open tasks are soonest due first. Done tasks are most recently completed first.

## projects.chats.list

Page IM chats related to the project: platform, chat id, and a short last message. Requires `im.canSeeChats`. Phone, Telegram id, a WhatsApp id like `number@c.us`, and a chat name that is itself a number are omitted.

## projects.chats.messages

Page one of those chats, newest first. Pass the chat id from `projects.chats.list`. Requires `im.canSeeChats`. A bad chat id is `Chat not found or not accessible`. Each row has time, direction, text, and attachment type plus caption. Sender phone numbers are omitted. Message text is kept.

## projects.emails.list

Page emails, newest first. Requires `mailer.canSeeMessages`. Rows have subject, time, direction, and a text snippet. Sender and recipient addresses are omitted.

## projects.room.messages

Page the project room on the Chats tab, not IM. Newest first. Requires `projects.canSeeProjects`. A staff author is the login. A client author has no name and no contact. Message text is kept.

## projects.addNote

Prepare an append-only internal note. This method does not write the note.

Input is `projectId`, `text`, optional `reason`, and optional `source` (default `atlas-agent`). It requires `projects.canAddNotes` and a project this actor can see.

The response is `operationId`, `target`, `preview`, `warnings`, and `expiresAt`. The prepared operation lasts 24 hours.

1. Show the person the target, note text, warnings, and `operationId`.
2. Wait for an explicit confirmation that this note should be created. Silence is not confirmation.
3. Only then call `operations.apply` with `{ "operationId": "<id>" }`.

Do not call `operations.apply` in the same step. Applying the same operation again does not create a second note: the status is `already_applied`. An expired operation cannot be extended. Call `projects.addNote` again and show the new preview. Another actor's operation cannot be applied.
