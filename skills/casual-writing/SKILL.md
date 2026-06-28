---
name: casual-writing
description: Rewrite, draft, or tune everyday writing so it sounds natural, casual, human, and context-aware, with special attention to avoiding AI slop and preserving the user's casing, spelling style, and internet shorthand. Use when the user asks for help with texts, DMs, Slack or Discord messages, short emails, comments, captions, personal notes, follow-ups, apologies, invitations, boundaries, dating messages, friendly workplace chat, or any writing that should be less formal, less corporate, less AI-like, warmer, shorter, softer, more direct, or more conversational.
---

# Casual Writing

## Overview

Make casual writing sound like a real person typed it. Preserve the user's meaning, relationship, and intent while removing stiffness, filler, over-polish, default assistant voice, and AI slop.

## Workflow

1. Infer the situation: medium, recipient, relationship, stakes, and desired outcome. Ask a question only when a wrong assumption could make the message awkward or risky.
2. Preserve the payload and surface style: names, dates, commitments, requests, boundaries, apologies, emotional intent, facts, casing, spelling style, contractions, and internet shorthand from the draft.
3. Pick a natural register: default to brief, warm, and clear. Adjust toward softer, firmer, funnier, more affectionate, more professional, or more low-key only when the user asks or the context clearly calls for it.
4. Rewrite in everyday language: use contractions, simple words, active phrasing, and sentence rhythms that fit the medium. Texts and DMs can use fragments and line breaks. Emails can stay tidy without becoming corporate.
5. Return the useful output: for simple rewrites, give the best version first. Offer 2-3 variants only when tone choice matters or the user asks for options.

## Voice Rules

- Prefer plain words: "help" over "assist", "use" over "utilize", "start" over "commence", "buy" over "purchase".
- Use contractions by default: "I'm", "you're", "can't", "don't", "we'll".
- Keep warmth specific and light. Do not add intimacy, flattery, or enthusiasm that the user did not imply.
- Avoid inflated openings: "I hope this message finds you well", "I wanted to reach out", "I am writing to inform you", "per our conversation".
- Avoid assistant-coded phrasing: "delve", "leverage", "seamless", "robust", "tapestry", "in today's fast-paced world", "it's important to note".
- Never use em dashes or en dashes as punctuation in casual rewrites. Use commas, periods, colons, parentheses, or rewrite the sentence. Keep them only in quoted/source text, user-requested style, or literal data where changing the character would be wrong.
- Preserve the user's casing and casual spelling when rewriting. If the input says "openai", keep "openai" rather than changing it to "OpenAI". If the input says "im", keep "im" rather than changing it to "I'm". Do not normalize internet writing, lowercase names, acronyms, contractions, or shorthand unless the user specifically asks for grammar/capitalization cleanup or the original text contains a clear accidental error that would confuse the recipient.
- Use exclamation points and emojis sparingly. Mirror the user's level if they already use them; otherwise default to none or one.
- Let casual writing be a little imperfect when that helps it feel real: a short fragment, a simple "also", or a direct "quick question" is often better than polished symmetry.
- Do not over-slang. Casual should mean easy and human, not forced, trendy, or trying too hard.
- Keep boundaries clear. Do not soften a no, apology, or request so much that the meaning disappears.

## Avoid AI Slop

Treat "does this sound like AI slop?" as a mandatory final check. If the answer is yes, rewrite again before responding.

- Do not produce generic, inflated, vibe-less, over-balanced, or over-explained prose.
- Do not make every message sound polished, complete, and emotionally optimized. Everyday writing can be plain, short, uneven, or understated.
- Avoid template cadence: "I completely understand", "I truly appreciate", "That being said", "At the end of the day", "I wanted to take a moment", "It means a lot".
- Avoid assistant narration in the output: "Here's a more casual version", "I made it warmer", "This keeps it friendly but direct" unless the user asked for explanation.
- Avoid fake specificity: do not add emotional texture, backstory, praise, concern, or enthusiasm that the user did not provide.
- Avoid symmetry for its own sake. Real texts do not need a neat three-part structure, perfect closure, or a softened ending.
- Prefer one sharp, usable message over several polished paragraphs.
- If the rewrite sounds like a brand, HR memo, customer support macro, or helpful chatbot, cut it down and make it sound like the sender.

## Common Moves

- Shorten first, then warm it up.
- Swap abstract nouns for verbs.
- Replace long setups with the point.
- Move the ask near the top.
- Turn corporate apologies into direct accountability.
- Keep one idea per sentence for texts.
- For workplace chat, be friendly but avoid sounding like a formal email.
- For vulnerable messages, make the tone grounded, not theatrical.
- For dating or friendship texts, preserve the user's actual energy. Do not make it clingier, cooler, or flirtier than requested.
- For conflict, remove blamey edges while keeping the user's boundary intact.

## Output Patterns

When rewriting:

- If the user wants one message, provide only the rewritten message unless a brief note is useful.
- If tone is ambiguous, provide labeled options such as "Warmer", "Shorter", or "More direct".
- If the source draft has a factual or emotional ambiguity, preserve the ambiguity rather than inventing details.
- If the user's draft is already good, make the smallest useful edit and say so briefly.

When drafting from scratch:

- Ask for missing facts only when necessary.
- Otherwise draft from the user's prompt and keep placeholders visible, like "[time]" or "[name]".
- Prefer a ready-to-send message over analysis.

## Quick Checks

Before finalizing, check:

- Would someone actually send this?
- Is the ask or point easy to find?
- Does it sound like the user's relationship with the recipient?
- Did it preserve the user's casing, spelling style, and shorthand unless cleanup was requested?
- Does it avoid AI slop, including generic warmth, filler, and assistant cadence?
- Did any detail, commitment, or boundary get weakened?
- Did the rewrite remove unnecessary polish instead of adding more?

## Examples

Formal follow-up:

Input: "I wanted to follow up regarding our previous conversation and see if you had any updates."

Output: "Hey, just checking in. Any updates on this?"

Soft no:

Input: "Decline dinner but don't make it weird."

Output: "I can't make dinner tonight, but thank you for inviting me. Hope you all have a good time."

Late reply:

Input: "Apologize for taking forever to respond and say I can send the file tomorrow."

Output: "Sorry for the slow reply. This week got away from me, but I can send the file over tomorrow."
