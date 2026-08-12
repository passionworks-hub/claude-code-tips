---
name: authoring-context-files
description: Applies Anthropic's official, live-fetched best practices for authoring Claude Code context files, both SKILL.md skill files and CLAUDE.md / AGENTS.md project-memory files. Use whenever creating a new skill, writing or editing any SKILL.md, running /init or drafting a CLAUDE.md, adding rules under .claude/rules/, or reviewing/improving an existing skill or CLAUDE.md for quality — in this repo or any other. Fetches the current guidance (not a cached copy) on naming, description quality, conciseness, progressive disclosure, size limits, and structure, then reports back exactly which best practices were applied and why.
---

# Authoring context files

Two artifact types, one shared discipline: both SKILL.md and CLAUDE.md are
context Claude reads at the start of (or during) a session, competing for
space with everything else Claude needs to know. The single biggest failure
mode for both is the same — writing too much, explaining things Claude
already knows, and burying the one instruction that actually matters under
paragraphs that don't.

This skill fetches Anthropic's **current, live** guidance rather than
carrying its own cached copy — those docs get revised, and a stale local
snapshot would silently drift from what's actually true (exact character
limits, reserved words, checklist items). Don't rely on your own training-
data memory of these docs either; fetch them.

## Step 1: Identify which artifact you're authoring

- **A skill** (new or existing `SKILL.md`, anywhere) → fetch the Skills doc.
- **A CLAUDE.md, CLAUDE.local.md, AGENTS.md, or a file under `.claude/rules/`**
  → fetch the CLAUDE.md doc.
- **Both** (e.g. setting up a repo's Claude Code config from scratch) → fetch
  both.

## Step 2: Fetch the live guidance

Use WebFetch with the URL and prompt below for the artifact type from Step 1.
Use the prompt text exactly as given — it's tuned to pull the specific,
checklist-relevant facts (limits, reserved words, structural rules) rather
than a vague summary.

**Skills** — `https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices`

> Extract the complete current guidance for authoring SKILL.md files: the
> YAML frontmatter validation rules (name and description constraints,
> including any reserved words or length limits), naming conventions, how to
> write an effective description, the progressive disclosure patterns,
> degrees-of-freedom guidance, content rules (time-sensitive info,
> terminology, examples), anti-patterns, guidance for skills with executable
> scripts, and reproduce the "Checklist for effective Skills" section in
> full.

**CLAUDE.md** — `https://code.claude.com/docs/en/memory`

> Extract the complete current guidance on CLAUDE.md files: what belongs in
> CLAUDE.md vs. auto memory vs. skills, the scope table (managed/user/
> project/local), how to write effective instructions (size limits,
> structure, specificity, consistency), imports and AGENTS.md handling,
> `.claude/rules/` path-scoped rules, and common troubleshooting/failure
> modes.

**If the fetch fails** (offline, page moved, tool unavailable): say so
explicitly to the user, proceed using the shared principles in Step 3 plus
your best general knowledge, and flag in your final report that the
checklist wasn't freshly verified against the source — don't silently fall
back without saying so.

## Step 3: Shared principles (apply regardless of artifact type, stable enough not to need a live fetch)

- **Assume Claude is already smart.** Cut any sentence that explains a
  concept a competent engineer/Claude already knows. Every paragraph must
  earn its token cost.
- **Match specificity to what's actually true.** "Use 2-space indentation"
  beats "format code properly." Vague instructions get inconsistently
  followed; concrete, verifiable ones don't.
- **Don't document what Claude can derive from the codebase.** Directory
  layouts, dependency lists, things visible from `ls`/`package.json` don't
  belong in either file — they go stale and Claude can look.
- **No time-sensitive claims** ("before/after date X, use Y") — write only
  current state; isolate any legacy pattern in a clearly labeled aside.
- **One consistent term per concept**, used everywhere in the file.
- **Shorter is more reliable, not just cheaper.** Treat size limits as a
  forcing function to cut, not a target to fill — the exact numbers come
  from Step 2's fetch, not from memory, since they're the kind of detail
  that changes.

## Step 4: Draft, then check against the fetched checklist

Write (or revise) the file, then walk the checklist you just fetched, item
by item. Fix anything that fails before considering the draft done. Don't
skip this even for a small edit — a one-line addition can still push a file
over its size limit or introduce inconsistent terminology.

## Step 5: Report what you applied

This is the part that's easy to skip and shouldn't be. After drafting or
editing, tell the user — in a few bullets, not a wall of text — which
specific best practices shaped the result. Concrete beats generic:

- Bad: "I followed best practices."
- Good: "Tightened the description to name explicit trigger phrases (was
  missing 'when to use'). Moved the API reference table to
  `reference/api.md` since the body was approaching 500 lines. Reworded two
  instructions from vague ('handle errors well') to verifiable ('retry
  network errors up to 3 times, others fail immediately')."

If you deliberately chose not to apply something the checklist calls for
(e.g. skipped writing evaluations for a purely stylistic skill), say so and
say why — that's a decision, not an omission, and the user should see it as
one.

## Note on overlap with other skills

Some environments already have `superpowers:writing-skills` (skill authoring
workflow with test-driven iteration) or `claude-md-management:*` (CLAUDE.md
audit/revise) installed as plugins. Those are heavier, process-oriented
skills — good for actively co-developing a skill through evals, or auditing
an existing CLAUDE.md across a whole repo. This skill is the lighter,
always-available baseline: it applies the current official checklist and
reports on it, not a full eval loop. If both are available and the task
warrants deeper iteration (a skill going into real production use, not a
one-off), prefer the heavier one and let this one serve as the fast,
always-current check underneath it.
