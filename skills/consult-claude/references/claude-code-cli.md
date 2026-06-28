# Claude Code CLI Guide

Checked against local Claude Code 2.1.186 and official docs on 2026-06-28.

## Default Call

```bash
cat prompt.md | claude -p --model claude-opus-4-8 --effort xhigh --output-format text --no-session-persistence --tools "" "Answer the prompt from stdin. Be concise, critical, and explicit about uncertainty."
```

## Essential Flags

- `-p` / `--print`: non-interactive response, then exit.
- `--model claude-opus-4-8`: pin Opus 4.8 instead of relying on aliases.
- `--effort xhigh`: use xhigh reasoning explicitly.
- `--output-format text`: easiest to read; use `json` only when scripting.
- `--no-session-persistence`: avoid saving one-off consult sessions.
- `--tools ""`: disable tools when Claude only needs supplied context.
- `--max-budget-usd <amount>`: cap large/uncertain calls.

## If Claude Must Inspect Files

Grant narrow read-only access:

```bash
cat prompt.md | claude -p --model claude-opus-4-8 --effort xhigh --output-format text --no-session-persistence --tools "Read,Grep,Glob" --add-dir /absolute/path/to/repo "Inspect only what is necessary; do not edit files."
```

Avoid `Edit`, broad `Bash`, and permission bypasses for consultation.

## Efficient Prompt Shape

Include: exact question, current hypothesis, constraints, relevant snippets/logs/sources, and what kind of answer is useful. Ask for objections, missing cases, uncertainty, and verification targets.

## Failure Notes

- Missing CLI: run `command -v claude`.
- Auth issue: run `claude auth status --text`.
- Version issue: run `claude --version`; Opus 4.8 needs Claude Code v2.1.154+.
- If `claude-opus-4-8` or `xhigh` is rejected, report that instead of silently downgrading.

Sources: https://code.claude.com/docs/en/cli-reference, https://code.claude.com/docs/en/model-config, https://platform.claude.com/docs/en/about-claude/models/overview
