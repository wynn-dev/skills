---
name: code-review
description: Review proposed code changes, pull requests, commits, diffs, or workspace changes as an engineering reviewer. Use when Codex is asked to review code, inspect a PR or branch, find actionable bugs or regressions, post inline review comments, or summarize review findings.
---

# Code Review

Act as a reviewer for a proposed code change made by another engineer. Prioritize findings the original author would likely fix if they knew about them.

If user, developer, repository, or tool-specific review instructions conflict with this skill, follow the more specific instruction.

## Workflow

1. Gather context from the prompt, repository docs, tests, nearby code, and any review-specific instructions.
2. Get the changed code:
   - Prefer `mcp__conductor__GetWorkspaceDiff` when available. Start with `stat: true`, then request specific changed files as needed.
   - If that tool is unavailable, compute the committed diff and uncommitted diff:

```bash
MERGE_BASE=$(git merge-base origin/main HEAD)
git diff "$MERGE_BASE" HEAD
git diff HEAD
```

3. Always use `$consult-codex` for an independent parallel code review before finalizing findings. Start the consult after gathering the diff and necessary context; ask for actionable bugs under this same review threshold. Keep the consult read-only, treat its output as advisory, and independently verify any candidate finding before posting it.
4. Review the combined committed and uncommitted changes. Inspect affected call sites or contracts before flagging impact; use `rg` for code search.
5. Return every qualifying finding. Do not stop at the first issue.
6. If no finding clearly meets the threshold, report no findings rather than stretching.

## Finding Threshold

Flag an issue only when all of these are true:

- It meaningfully affects correctness, performance, security, or maintainability.
- It is discrete and actionable, not a broad critique of the codebase.
- The expected fix fits the rigor already present in the repository.
- The issue was introduced by the reviewed change, not pre-existing.
- The original author would likely fix it if made aware.
- It does not depend on unstated assumptions about intent or the codebase.
- The affected code path, caller, environment, or input is identifiable, not speculative.
- It is clearly not an intentional behavior change.

Ignore trivial style unless it obscures meaning or violates documented standards. Do not flag missing tests as a finding unless the absence directly demonstrates a user-visible bug or broken contract.

## Comment Rules

Write one inline comment per distinct issue. Keep the line range as short as possible, usually one line and rarely more than 5 to 10 lines.

Each comment should:

- Explain why the issue is a bug.
- State the scenario, environment, or input required for the bug to occur.
- Match the actual severity without exaggeration.
- Be brief: one paragraph, no unnecessary line breaks.
- Avoid location details already supplied by the inline comment.
- Avoid praise, blame, filler, and phrases like "Great job" or "Thanks for".
- Avoid code blocks longer than 3 lines.

Use ```suggestion blocks only for concrete replacement code. Keep suggestions minimal and preserve the exact leading whitespace of the replaced lines, including tabs versus spaces. Do not change outer indentation unless that is the fix.

## Posting Findings

Use the review surface available in the environment:

- If `mcp__conductor__DiffComment` is available, post inline comments with that tool.
- If the Codex app inline comment directive is the available review surface, emit `::code-comment{...}` directives with tight file and line ranges.
- If no inline comment tool is available, return findings in plain text with title, explanation, file, and line.

After posting or listing inline comments, provide a concise issue list:

```markdown
### **#1 Short finding title**

Brief explanation of the bug and triggering scenario.

File: path/to/file.ext
```

Order findings by severity. When there are no findings, say that clearly and mention any meaningful test gaps or residual risk separately.
