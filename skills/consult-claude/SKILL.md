---
name: consult-claude
description: Use Claude Code CLI non-interactively as an external Opus 4.8 xhigh advisor for second opinions or collaborative research. Trigger when the user asks to consult Claude/Opus or when risky plans, code changes, debugging, architecture, writing, or research would benefit from independent critique. Synthesize and verify Claude's answer instead of forwarding it blindly.
---

# Consult Claude

Use Claude Code CLI for a focused outside opinion. Read [Claude Code CLI Guide](references/claude-code-cli.md) when command details are not fresh.

## Process

1. Choose mode: `second-opinion` for critique, `research-together` for parallel exploration.
2. Send only the necessary context: question, constraints, current hypothesis, and relevant snippets/logs/sources.
3. Do not send secrets, credentials, private keys, customer data, or broad proprietary context unless the user clearly authorized it.
4. Ask Claude for disagreement, gaps, uncertainty, and the smallest practical improvement.
5. Invoke Opus 4.8 xhigh in non-interactive mode.
6. Compare Claude's answer with local evidence and primary sources when needed.
7. Report your synthesized judgment, noting Claude only when it materially affected the result.
