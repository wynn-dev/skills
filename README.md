# Skills

A public collection of personal agent skills I use day to day. They follow the [skills.sh](https://www.skills.sh/) convention (`skills/<name>/SKILL.md`), so they work with Claude Code, Codex, Cursor, and other supported agents.

## Skills

| Command | What it does |
| --- | --- |
| `/fix-findings <findings>` | Checks each reviewer finding, fixes the valid ones in PRs, and asks when something needs a product call. |
| `/review-merge [PRs]` | Reviews the PRs from the current conversation (or the ones listed), then merges them. |

Both are slash-command only in Claude Code and Codex, so the agent won't trigger them on its own.

## Install

Install everything:

```bash
npx skills add wynn-dev/skills
```

Install globally (available in every project):

```bash
npx skills add wynn-dev/skills -g
```

Install a single skill:

```bash
npx skills add wynn-dev/skills --skill fix-findings
```

List the skills in this repo without installing:

```bash
npx skills add wynn-dev/skills --list
```

Update installed skills:

```bash
npx skills update
```
