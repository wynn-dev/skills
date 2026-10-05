---
name: cleanup
description: Deep cleanup pass that finds overcomplicated code, migrations that should no longer exist, and useless tests, then simplifies them in PRs. Use when the user invokes /cleanup.
argument-hint: "[paths or areas]"
disable-model-invocation: true
---

Treat this as a cleanup operation across the codebase, or the paths listed with this command. Find code that's deeper or more complicated than it needs to be, migrations and compatibility code that should no longer exist, and tests that shouldn't exist, like ones that always pass. Make the code more DRY and SOLID, but KISS comes first.

Fix what holds up, using PRs, and review each PR before getting back to me. Keep behavior the same. Before removing a migration, check that nothing can still run it. When you're unsure, or something needs a product call, ask me.

Use subagents where they help, but keep it to about 15 at a time. Hundreds at once burns through my usage limit.

Finish with the PRs, plus anything you found but left alone and why.
