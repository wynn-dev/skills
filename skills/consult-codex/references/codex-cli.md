# Codex CLI Guide

Checked against local Codex CLI 0.142.3, local `config.toml`, and local model cache on 2026-06-29. The local model cache shows `gpt-5.5` supports `xhigh`.

## Default Call

```bash
cat prompt.md | codex --ask-for-approval never exec --model gpt-5.5 -c 'model_reasoning_effort="xhigh"' --sandbox read-only --ephemeral --color never "Answer the prompt from stdin. Be concise, critical, and explicit about uncertainty. Do not edit files."
```

## Essential Flags

- `exec`: run Codex non-interactively, then exit.
- `--ask-for-approval never`: prevent the consult from blocking on prompts. This is a top-level Codex flag, so place it before `exec`.
- `--model gpt-5.5`: pin GPT-5.5 instead of relying on config defaults.
- `-c 'model_reasoning_effort="xhigh"'`: use xhigh reasoning explicitly.
- `--sandbox read-only`: allow inspection while preventing edits.
- `--ephemeral`: avoid persisting one-off consult sessions.
- `--color never`: keep captured output plain.
- `-o <file>`: optionally write the final assistant message to a file for cleaner parsing.

## If Codex Must Inspect Files

Grant narrow read-only access:

```bash
cat prompt.md | codex --ask-for-approval never exec --model gpt-5.5 -c 'model_reasoning_effort="xhigh"' --sandbox read-only --ephemeral --color never -C /absolute/path/to/repo "Inspect only what is necessary. Do not edit files. Be concise, critical, and explicit about uncertainty."
```

Use `--add-dir /absolute/path` only for extra directories that are truly needed. Use `--skip-git-repo-check` only when consulting outside a Git repository.

Avoid `--sandbox workspace-write`, `--sandbox danger-full-access`, and `--dangerously-bypass-approvals-and-sandbox` for consultation.

## Efficient Prompt Shape

Include: exact question, current hypothesis, constraints, relevant snippets/logs/sources, and what kind of answer is useful. Ask for objections, missing cases, uncertainty, and verification targets.

## Failure Notes

- Missing CLI: run `command -v codex`.
- Auth/config issue: run `codex doctor --summary`.
- Version issue: run `codex --version`.
- Flag details: run `codex exec --help`.
- If `gpt-5.5` or `xhigh` is rejected, report that instead of silently downgrading.
