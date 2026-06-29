---
name: consult-codex
description: Use Codex CLI non-interactively as an external GPT-5.5 xhigh advisor for second opinions or collaborative research. Trigger when the user asks to consult Codex/GPT-5.5 or when risky plans, code changes, debugging, architecture, writing, or research would benefit from an independent Codex critique. Synthesize and verify Codex's answer instead of forwarding it blindly.
---

# Consult Codex

Use Codex CLI for a focused outside opinion from GPT-5.5 xhigh. Read [Codex CLI Guide](references/codex-cli.md) when command details are not fresh.

## Process

1. Choose mode: `second-opinion` for critique, `research-together` for parallel exploration.
2. Send only the necessary context: question, constraints, current hypothesis, and relevant snippets/logs/sources.
3. Do not send secrets, credentials, private keys, customer data, or broad proprietary context unless the user clearly authorized it.
4. Ask Codex for disagreement, gaps, uncertainty, verification targets, and the smallest practical improvement.
5. Invoke GPT-5.5 xhigh in non-interactive mode.
6. Keep the consult read-only unless the user explicitly wants a separate implementation pass.
7. Compare Codex's answer with local evidence and primary sources when needed.
8. Report your synthesized judgment, noting the consult only when it materially affected the result.
