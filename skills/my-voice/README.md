# my-voice — keep your authenticity, use AI as the assistant

What we lose to AI is **authenticity**. You're in product, GTM, or sales. Sharing
what you did and what you think — in Slack, on LinkedIn — matters more than ever.
But the AI layer we use to "polish" quietly replaces our voice with its own.

This skill flips that. You write or speak your raw content. It returns the same
thing in **your** style, with minimal grammar and flow fixes — not an AI rewrite.

### How it knows your style

The first time you use it, it asks for your **top 5 best posts** — the ones you
spent real time on. It learns your voice from those, once. After that, just feed
it your draft.

### Install

A skill is just a folder. Claude Code finds skills in only two places:

- `~/.claude/skills/` — **personal**, works in all your projects
- `<your-project>/.claude/skills/` — **project-only**, shareable with a team via git

Put the `my-voice/` folder into one of them. Pick whichever way is easiest:

**Option A — by hand (no terminal needed)**

1. Open (or create) the folder `~/.claude/skills/` on your machine.
   - macOS / Linux: `~/.claude/skills/`
   - Windows: the `.claude\skills\` folder under your user directory.
2. Inside it, create a folder named `my-voice`.
3. Put all three files into `~/.claude/skills/my-voice/`:
   - `SKILL.md`  ← the filename must be exactly this
   - `my-best-posts.md`
   - `README.md`

**Option B — terminal (clone + copy)**

```bash
git clone https://github.com/passionworks-hub/claude-code-tips
cp -r claude-code-tips/skills/my-voice ~/.claude/skills/   # personal
# or, project-only:
cp -r claude-code-tips/skills/my-voice <your-project>/.claude/skills/
```

**Then:** restart Claude Code (or start a new chat) so it re-scans your skills.

### Use

```
/my-voice
```

Then paste or speak your content. First run, it'll ask for your 5 posts. Every
run after, it just cleans up your draft and shows you exactly what it changed.

Your style. Your identity. AI as the assistant — not the author.
