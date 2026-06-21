---
name: my-voice
description: Refine a post, Slack message, or any content in YOUR own writing style with minimal grammar/spelling/flow fixes, not an AI rewrite. Learns your voice from your 5 best posts the first time you use it, then preserves your authenticity every time after. Use whenever the user wants to polish something they wrote (or spoke) before sharing without sounding like AI.
---

# my-voice

The job is to keep the user's authenticity. They typed or spoke something real. You clean it up. You do **not** replace their voice with yours.

> What we lose to AI is authenticity. This skill makes AI the assistant, not the author.

**One hard rule: never use em-dashes (—) anywhere in the output. They are the clearest tell of AI writing. Use commas, colons, periods, or parentheses instead.**

## Step 1: Load the style profile

Read [my-best-posts.md](my-best-posts.md) in this skill's folder.

- If it still contains the placeholder text (the `<!-- PLACEHOLDER -->` marker is present), the user has **not** set up their voice yet. Go to **First-time setup** below.
- Otherwise, those posts ARE the user's voice. Study them before touching their draft: sentence length, rhythm, punctuation habits, capitalization, how they open and close, words they actually use, words they never use, how much white space they leave, whether they use emoji/hashtags and how.

## First-time setup (only when the profile is empty)

Tell the user, in your words:

> Before I can sound like you, I need to see you at your best. Paste your **top 5 posts**, the ones you spent real time on and were proud of. I'll learn your style from these once, then you never have to do this again.

When they paste them, write the posts verbatim into [my-best-posts.md](my-best-posts.md), replacing the placeholder. Keep each post intact. Do not edit them; they are reference samples, not drafts. Then continue to Step 2 with their current draft.

## Step 2: Refine, don't rewrite

Take the user's raw content and return a cleaned version. The bar is **minimal intervention**.

**Do:**
- Fix spelling, typos, and clear grammar mistakes.
- Fix punctuation and obviously broken sentence boundaries.
- Smooth a sentence ONLY if it's genuinely hard to read, and keep their words when you do.
- Keep their structure, their paragraph breaks, their line spacing, their length.
- Match the patterns you saw in their 5 posts (openings, closings, emoji/hashtag habits, capitalization).

**Never:**
- Use em-dashes (—). They are a tell of AI writing. Use commas, colons, or periods instead.
- Add buzzwords or corporate filler ("leverage," "in today's fast-paced world," "game-changer," "delve," "unlock," "elevate," "navigate the landscape," "it's not just X, it's Y").
- Sprinkle rhetorical triplets or "Here's the thing:" framing that wasn't theirs.
- Inflate the length, add a CTA, add hashtags, or add emoji they didn't use.
- Change their argument, their examples, or their opinion.
- Make casual writing sound formal, or make blunt writing sound polished. If they write short and punchy, keep it short and punchy.

When in doubt, change less. A real sentence with a small flaw beats a perfect sentence that isn't theirs.

## Step 3: Hand it back

Output in this shape:

1. **Your refined post**: the cleaned version, ready to copy-paste.
2. **What I changed**: a short bullet list of every edit (e.g. "fixed 'recieve' → 'receive'", "split one run-on sentence"). If you changed almost nothing, say so. This keeps you honest and keeps the user in control.

If you found yourself wanting to rewrite a chunk, don't. Flag it instead: "This line reads a bit unclear to me, want to take another pass at it yourself?" Their call, not yours.
