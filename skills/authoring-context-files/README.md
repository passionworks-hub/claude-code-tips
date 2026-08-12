# authoring-context-files: write skills and CLAUDE.md against the current rules, not stale memory

SKILL.md and CLAUDE.md files compete for context space with everything else
Claude needs to know. The single biggest failure mode for both is the same:
writing too much, explaining things Claude already knows, and burying the
one instruction that actually matters under paragraphs that don't.

This skill doesn't carry its own cached checklist. Instead it live-fetches
Anthropic's current guidance (exact character limits, reserved words,
structural rules) at the moment you need it, since those docs get revised
and a stale local copy would silently drift from what's actually true.

Use it whenever you're creating a new skill, writing or editing any
`SKILL.md`, running `/init`, drafting a `CLAUDE.md`/`AGENTS.md`, adding rules
under `.claude/rules/`, or reviewing an existing one for quality.

### Install

A skill is just a folder. Claude Code finds skills in only two places:

- `~/.claude/skills/`: **personal**, works in all your projects
- `<your-project>/.claude/skills/`: **project-only**, shareable with a team via git

Put the `authoring-context-files/` folder into one of them. Pick whichever
way is easiest:

**Option A: by hand (no terminal needed)**

1. Open (or create) the folder `~/.claude/skills/` on your machine.
   - macOS / Linux: `~/.claude/skills/`
   - Windows: the `.claude\skills\` folder under your user directory.
2. Inside it, create a folder named `authoring-context-files`.
3. Put `SKILL.md` into `~/.claude/skills/authoring-context-files/` (the
   filename must be exactly this).

**Option B: terminal (clone + copy)**

```bash
git clone https://github.com/passionworks-hub/claude-code-tips
cp -r claude-code-tips/skills/authoring-context-files ~/.claude/skills/   # personal
# or, project-only:
cp -r claude-code-tips/skills/authoring-context-files <your-project>/.claude/skills/
```

**Then:** restart Claude Code (or start a new chat) so it re-scans your skills.

### Use

Just create or edit a `SKILL.md` or `CLAUDE.md` — Claude picks this up
automatically. It fetches the live Anthropic docs for the artifact type
you're working on, applies the shared authoring principles, drafts against
the checklist, and reports back exactly which best practices shaped the
result.

Note: if this environment also has `superpowers:writing-skills` or
`claude-md-management:*` installed, those are heavier eval-driven workflows
better suited to production skills. This one is the lighter, always-current
baseline check.
