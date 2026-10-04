---
name: fix-findings
description: Investigate a list of reviewer findings, fix the ones that hold up, and open PRs. Use when the user invokes /fix-findings with review findings.
argument-hint: <findings>
disable-model-invocation: true
---

A reviewer found issues that might cause problems, or changes that could improve the app. The list comes with this command or in the message just before it.

Check whether each finding is real and relevant here. Fix the ones that are, using PRs, and review each PR you open before getting back to me. Skip the rest and say why. When you're unsure, or a finding needs a product call, ask me.

Finish with each finding's outcome: the PR that fixed it, or why it was skipped.
