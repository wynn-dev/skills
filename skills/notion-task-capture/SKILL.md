---
name: notion-task-capture
description: Capture actionable tasks, todos, follow-ups, and action items from the current or recent conversation context into Notion's `task tracker` database with `Draft` status using the `notion` CLI, checking for similar existing tasks before creating new ones and adding task body descriptions when useful. Use when the user asks to add, save, log, capture, or sync relevant tasks from prior context to Notion, update a Notion task database from chat, or turn recent agent/user work into Notion action items.
---

# Notion Task Capture

Capture only concrete future actions from the current thread's prior context and create or update them in Notion's `task tracker` database with `Draft` status using the `notion` CLI.

If user, developer, or workspace instructions conflict with this skill, follow the more specific instruction. Mutating Notion is live external state, so inspect before writing and ask only when the destination or intended task set is genuinely ambiguous.

## Workflow

1. Review the available prior context. Extract tasks from explicit TODOs, commitments, follow-ups, requested future work, unresolved blockers, or clearly implied next steps needed for a stated goal. Skip completed work, vague ideas, notes, decisions with no future action, and filler tasks. If no actionable task exists, say so and do not create anything.
2. Normalize each task:
   - Write a short imperative title, ideally under 120 characters.
   - Include a concise context note such as `From Codex thread on YYYY-MM-DD: ...`.
   - Set due dates only when explicit. Resolve relative dates against the current date and timezone from system context.
   - Set `Status=Draft` for every created task.
   - Set priority, owner, project, and tags only when they are explicit or map cleanly to existing Notion properties.
   - Plan a short page-body description when the title and database properties are not enough to preserve context, acceptance criteria, links, blockers, or the reason the task exists.
   - Avoid storing unnecessary private details.
3. Check Notion CLI access before mutating:

```bash
notion auth status
```

4. Locate the destination:
   - Use the Notion database named `task tracker` as the destination.
   - Search for it directly:

```bash
notion db list
notion search "task tracker" --type database
```

   - If multiple `task tracker` databases are plausible, ask the user which one to use.
   - If `task tracker` cannot be found or resolves only to a regular page, ask for the database URL/id. Do not append plain todo blocks because they cannot reliably set `Status=Draft`.
5. Inspect the database schema before writing:

```bash
notion db view <database-id-or-url>
```

Map only to properties that actually exist. Require a `Status` property with a `Draft` option. Common mappings are title property (`Name`, `Task`, or `Title`), `Status`, `Due`/`Date`, `Priority`, `Tags`, `Project`, and `Source`/`Context`/`Notes`.

6. Check for duplicate or similar existing tasks before adding a new task:
   - Query the `task tracker` database with 2 to 3 distinctive title phrases or keywords. Run separate queries when needed; multiple `-F` flags combine with AND.
   - Also query by project, tag, source, or context properties when those exist and help narrow the candidates.
   - Prefer active/open candidates. If the schema has terminal statuses such as `Done`, `Archived`, or `Canceled`, exclude or de-prioritize those when assessing similarity.

```bash
notion db query <database-id-or-url> -F '<title-property>~=Draft launch plan' --format json
notion db query <database-id-or-url> -F '<title-property>~=launch' --format json
```

Compare candidates by underlying action, project/context, owner, due date, and desired outcome:

- If an active task is clearly the same or substantially overlapping, update that existing task only when useful, such as appending missing context or linking the new source. Do not create a duplicate.
- If a candidate is related but meaningfully different, create a new `Draft` task and mention the related task in the body description or context property.
- If the match is uncertain and creating a duplicate would be noisy, ask the user to choose between updating the similar task and creating a new one.

7. Create tasks. Use exact property names and values from the schema, omitting properties that do not exist:

```bash
notion db add <database-id-or-url> "Name=Draft launch plan" "Status=Draft" "Due=2026-07-10" "Context=From Codex thread on 2026-07-07: user asked for launch prep next steps"
```

After creating a task, write a page-body description when it would make the task easier to act on. Keep it brief and structured. Include only useful context such as source thread/date, goal, relevant details, acceptance criteria, links, blockers, or related existing tasks:

```bash
notion page set-markdown <created-task-page-id> --append --text "Source: Codex thread on 2026-07-07\n\nContext: User asked for launch prep next steps.\n\nAcceptance criteria:\n- Draft launch plan is ready for review"
```

If the database has a short `Description`, `Context`, or `Notes` property, use it for a concise summary; use the page body for longer or multi-line details.

8. Verify and report. Keep track of created or updated Notion IDs/URLs from command output. Final response should list what was added to `task tracker` as `Draft`, what was updated because a similar task already existed, what was skipped as duplicate, and any tasks that could not be captured.

## Error Handling

- If `notion auth status` fails, tell the user to authenticate with `notion auth login --with-token` or set `NOTION_TOKEN`.
- If a write fails because of a schema mismatch, inspect the schema and retry once with valid property names and option values.
- If the `Status` property or `Draft` option is missing, stop and report the mismatch rather than creating tasks in a different status.
- If Notion returns a sharing or permissions error, explain that the integration likely needs access to the parent page or database.
- Do not create a new database or workspace-root page unless the user explicitly asks for that.
