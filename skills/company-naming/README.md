# company-naming: screen a startup name to a decision, not a pile of caveats

Ask an AI whether a company name is available and you get one of two useless
answers. Either "that's taken" (a hair salon in Lisbon uses it, and you sell
B2B software), or "looks clear!" (it searched three registers and couldn't
reach four others, and didn't say so).

This skill fixes both. It applies the test that actually decides the
question: **a conflict is a conflict when it's in a related trademark class,
in a market you actually sell into, by a company that's actually operating.**
A restaurant in class 43 is not a bar to your class 42 SaaS filing, and the
skill says so plainly instead of listing it as a "finding."

What it does:

- **Occupancy screening** — who's using the name, in which class, in which market
- **Near-neighbour checks** — examiners test phonetic and visual similarity, so
  exact-string searches miss most real conflicts
- **Cross-language screening** — including the two that keep catching people:
  Spanish/Portuguese verb conjugations, and religious vocabulary in Gulf markets
- **Pronunciation** — open syllables and pure vowels are why Zoho and Nokia
  travel and cluster-heavy English compounds don't
- **Must / should / defer** — the section founders actually need: what to spend
  money on this week, what to file in the first months, and what to leave alone
  until a specific trigger fires

Every material claim gets an evidence label: `[V]` verified from the primary
source, `[S]` secondary aggregator, `[I]` inferred, `[X]` couldn't reach it.
That last one is the important one. Registers like EUIPO, TMview, WIPO and UK
IPO routinely block automated access, and IP India is CAPTCHA-gated. "Couldn't
check" gets reported as its own visible list rather than quietly dropped into
the clear pile.

It also knows when to tell you to stop. If you've rejected thirty names, the
bottleneck isn't supply. Google was BackRub. Yahoo! was *Jerry and David's
Guide to the World Wide Web*, and the exclamation mark exists only because
"Yahoo" was already trademarked by a barbecue sauce. Zoho spent thirteen years
as AdventNet. No name feels right on day one; the affection comes from the
company, not the word.

### Install

A skill is just a folder. Claude Code finds skills in only two places:

- `~/.claude/skills/`: **personal**, works in all your projects
- `<your-project>/.claude/skills/`: **project-only**, shareable with a team via git

**Option A: by hand (no terminal needed)**

1. Open (or create) the folder `~/.claude/skills/` on your machine.
   - macOS / Linux: `~/.claude/skills/`
   - Windows: the `.claude\skills\` folder under your user directory.
2. Inside it, create a folder named `company-naming`.
3. Put `SKILL.md` into `~/.claude/skills/company-naming/` (the filename must
   be exactly this).

**Option B: terminal (clone + copy)**

```bash
git clone https://github.com/passionworks-hub/claude-code-tips
cp -r claude-code-tips/skills/company-naming ~/.claude/skills/   # personal
# or, project-only:
cp -r claude-code-tips/skills/company-naming <your-project>/.claude/skills/
```

**Then:** restart Claude Code (or start a new chat) so it re-scans your skills.

### Use

Just describe the naming problem — Claude picks this up automatically:

- "I'm naming an AI infra startup, here are five candidates, which one?"
- "Is `Nimbus` taken?"
- "Do I need to trademark in the US before I can invoice US clients?"
- "Should I register a Delaware entity for this?"

You'll get a ranked verdict, the reasoning, the jurisdictions that couldn't be
checked, and a short list of what to do this week.

**This is web research, not legal clearance.** A qualified trademark attorney
or agent has to clear the final name in each market. The skill's job is to tell
you which question to take to them, in which jurisdiction, and roughly what it
should cost.
