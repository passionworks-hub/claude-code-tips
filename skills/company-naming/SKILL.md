---
name: company-naming
description: Screens and clears a company or product name for a founder — generates candidates, checks who already occupies the name, triages trademark conflicts by class and market, runs cross-language and pronunciation checks, and says what to file now versus defer. Use when someone is naming a startup, evaluating candidate names, asking whether a name is taken or any good, checking domain or trademark availability, or deciding on a legal entity name versus a brand.
---

# Company Naming

A founder has a name, or needs one, and wants to know whether they can use it.
The job is to give them a decision they can act on — not a list of caveats and
not a legal opinion.

Two failure modes to avoid:

- **Reflexive rejection.** Every name is used by someone somewhere. Saying
  "that's taken" about a hair salon in Lisbon when the founder sells B2B
  software is noise dressed as diligence.
- **False clearance.** Saying a name is "clear" when the actual claim is
  "I searched three registers and could not reach four others."

The distinction that resolves both: **a conflict is a conflict when it is in
a related class, in a market the founder operates in.** Everything else is
context.

## The test that matters

Not "does anyone use this word." That question has no useful answer any more.

Ask instead:

1. Is anyone using it **in the same or an adjacent trademark class**?
2. **In a market the founder actually sells into**?
3. Is the user **operating and visible**, or dormant, dissolved, expired?

Three yeses is a real problem. Two is worth a professional's view. One is
usually noise.

For software and AI companies the classes are:

| Class | Covers |
|---|---|
| **9** | Downloadable and recorded software, apps, SDKs, hardware |
| **35** | Business consulting, advertising, data processing, business analysis |
| **42** | SaaS, PaaS, software development, IT consulting, R&D |

A restaurant (43), a clothing line (25), a pharmaceutical (5), or a
professional association (41/44/45) is almost never a bar to a class 9/35/42
filing. Say so plainly rather than listing it as a "finding."

## Evidence labelling

**Label every material claim.** Never let "searched and found nothing" blur
into "could not search."

| Label | Meaning |
|---|---|
| **[V]** Verified | Retrieved the primary source directly — registry RDAP, USPTO TSDR, official gazette, the company's own site |
| **[S]** Secondary | From a credible mirror or aggregator — Justia, Trademarkia, QuickCompany, Zauba, Crunchbase. Accurate but lags on status changes |
| **[I]** Inferred | Analysis or settled practice, not retrieved this session |
| **[X]** Not accessible | Could not reach the source. **This is not a clear result.** Treat the jurisdiction as unknown |

Many registers block automated access. EUIPO, TMview, WIPO Global Brand
Database, UK IPO and DPMA commonly return 403, 429, or robots blocks. IP India
is CAPTCHA-gated. The UAE has no free public register at all. When this
happens, report it as **[X]** in a visible list — never quietly omit it.

## Screening workflow

Copy this checklist and track progress:

```
Screening:
- [ ] Step 1: Occupancy — name + sector search, domains
- [ ] Step 2: Near-neighbours — phonetic and one-character variants
- [ ] Step 3: Cross-language screen
- [ ] Step 4: Pronunciation (only if the founder wants it)
- [ ] Step 5: Rank, label evidence, state must/should/defer
```

### Step 1: Occupancy — one search per candidate

Query the name plus the sector: `"<name>" company software`, `"<name>" AI`,
`"<name>" technology`. Then check the obvious domains.

Report for each hit: what the company does, where, how big, and **which class
it would fall in**. That last part is what converts a search result into a
decision.

### Step 2: Near-neighbours — this is where most misses happen

Trademark examiners test **phonetic and visual similarity**, not exact strings.
A name one character or one sound away from an operating company in the same
class is a conflict, even though an exact-match search returns nothing.

Always check: one letter added, one letter removed, one letter changed, and
the name as it would be *heard*. A name that sounds like a listed company in
the same industry is not available regardless of how empty the exact-string
search looks.

**A conflict is not always fatal.** Jerry Yang and David Filo found "Yahoo"
already registered — by a barbecue sauce and a line of steak knives — and
added an exclamation mark, because nobody else had one. Yahoo! cleared. When
a founder is attached to a blocked name, look for the modification that
distinguishes the mark before telling them to start over.

### Step 3: Cross-language screen

Screen against, at minimum: English, Spanish, Portuguese, French, German,
Italian, Arabic, Mandarin, Malay/Indonesian, Hindi, and the languages of any
specific target market.

Look for: obscenity, negative meaning, religious sensitivity, a common given
name, a place name, and near-collision with a large regional brand.

Two that recur and are easy to miss:
- **Spanish and Portuguese verb forms.** A coined name can be a live
  conjugation. Check it.
- **Religious vocabulary in Gulf markets.** Prayer-time and scriptural words
  are commercially usable but weighted; flag rather than recommend.

Calibrate against reflexive rejection. In *Gulliver's Travels* a Yahoo is a
filthy brute, and "yahoo" still means a lout in English dictionaries. It did
not matter. A dictionary meaning is a flag, not a veto — obscenity and
religious offence are vetoes, mild negative connotation is not.

### Step 4: Pronunciation, if the founder cares

Some founders explicitly rule this out. Ask before spending effort on it.

When it matters, the predictor is **open syllables and pure vowels** —
consonant-vowel structure, no clusters, no diphthongs. That is why Toyota,
Nokia, Zara and Zoho travel and why cluster-heavy English compounds do not.
*Zoho* is four letters, two open syllables, and pronounceable on first sight
in every market its company sells into.

Specific traps:
- `str-`, `sp-`, `sm-`, `-lt`, `-nd` clusters break in Spanish and Arabic
- Arabic has no /p/ and no native word-initial /o/
- Indian English merges /v/ and /w/
- The digraphs `aa`, `ai`, `ee`, `oo` are ambiguous to English readers
- The real test is **spell-from-hearing**: can someone who heard the name on a
  call type it correctly afterwards?

## Patterns that reliably fail

State these once, with the reason, rather than re-deriving them each time.

**Misspelling a common word.** The founder will lose to the correct spelling in
search, dictation and autocorrect forever, and will spell the name aloud on
every call. Google is the exception people cite, and it proves the rule:
*googol* is an obscure mathematical term nobody types, so the misspelling had
no incumbent to lose to. *Airkraft* and *Amplitide* do, because aircraft and
amplitude are words people spell correctly every day.

**English compound words.** Two ordinary words glued together make a weak,
hard-to-register mark, and they only parse for English speakers.

**Suffix trends.** `-ly`, `-ify`, `-AI`, `-base` timestamp a company the way
`.com` timestamped one in 1999. Recommend the standalone name and put the
category in the tagline.

**Initialisms.** Three letters must be spelled out — three syllables from three
characters with nothing to remember. Short domains in that space are also
expensive.

**Claim words.** *Innovations*, *Solutions*, *Ventures*, *Dynamics* assert
rather than demonstrate, and are the most crowded words on any corporate
register.

**Register-crowding by well.** Cosmic vocabulary, rocket and speed vocabulary,
and "empty vessel" invented syllables are exhausted. Obscure technical
vocabulary — mineralogy, poetics, feather anatomy, propulsion engineering,
trade-guild terms — still has room. When one well is empty, name why and move
to a less-picked one rather than generating more of the same.

## Must, should, defer

This is the section founders need most. Be explicit about it. Fees below are
indicative — confirm current amounts before quoting them as a number.

### Must — before the name is load-bearing

- **A trademark search in the home jurisdiction, in the operating classes.**
  Typically ₹5,000–15,000 in India, or a few hundred dollars elsewhere. This is
  the single decision-relevant spend. Corporate name approval is a *different
  system* from trademark and does not clear the brand.
- **Domain acquisition for the primary TLD.** Cheap, reversible, and the
  position erodes while the founder deliberates.
- **The obscenity half of the cross-language screen** (Step 3), in any market
  with staff or customers, ideally confirmed by a native speaker. Five minutes,
  and it is disqualifying when it fails.

### Should — within the first months

- **Home-jurisdiction trademark filing** in the core classes. In India this is
  ₹4,500/class with MSME or startup recognition, ₹9,000 without — and the
  certificate must be attached *at filing*, with no retroactive adjustment.
  Getting that registration first is free money.
- **Social and platform handles**, at least on the platforms that can actually
  be verified.
- Note that a home filing opens a **six-month Paris Convention window** in
  which foreign filings can claim the home date. After it closes, foreign
  filing is still possible — just from a later date.

### Defer — until a specific trigger

- **Foreign trademark filings.** Trigger: material revenue or a real conflict
  in that market. A trademark is not a licence to trade; a company can invoice
  US or EU clients from day one owning nothing abroad.
- **Foreign legal entities.** Trigger: local payroll, a physical office, or a
  customer whose procurement requires a local contracting party. Usually years
  away. Entities carry filing, accounting and tax obligations with no benefit
  until then.
- **Defensive domains and defensive class filings.** Trigger: someone actually
  encroaching.
- **Formal clearance opinions from foreign attorneys.** Expensive, and only
  worth it when the founder is about to spend real money in that market.

The honest framing: a trademark buys **the right to stop others, and the right
not to be stopped later**. Only the second matters to most early founders, and
only in markets where they have something to lose.

## Producing the recommendation

Lead with the verdict. Then the reasoning. Then what to do this week. A
sensible default shape, adapted to the specific situation:

```markdown
## Verdict
[Recommended name, and the one sentence reason it wins.]

## Ranking
1. **[Name]** — [what clears it, what the residual risk is]
2. **[Name]** — [why it places lower]
3. **[Name]** — [the specific thing that disqualifies or weakens it]

## Findings
[Per candidate: occupancy hits with class and market, near-neighbours,
language flags. Every claim labelled [V] / [S] / [I].]

## Could not check
[Jurisdictions and registers that returned [X]. Named, not omitted.]

## This week
- [ ] [The one or two must-do items, with rough cost]
```

Rules for that output:

- **Rank candidates** rather than describing each in isolation — founders
  decide by comparison.
- **Give reasons, not scores.** Numeric ratings on subjective criteria are
  false precision.
- **Separate the entity name from the brand.** Zoho Corporation Private Limited
  trades as Zoho; the descriptor is paperwork and the brand is the first word.
  A founder agonising over "Private Limited" versus "Technologies" is
  optimising the part nobody reads.
- **State the caveat once, precisely.** "This is web research, not legal
  clearance. A qualified trademark attorney or agent must clear the final name
  in each market." Once, not in every paragraph.
- **Name what requires a professional**, specifically: which question, which
  jurisdiction, roughly what it costs.

## When to push back

Founders over-invest here. Naming is a low-leverage decision that feels
high-leverage because it is the first one and it is emotionally legible.

If a founder has rejected thirty names and is asking for more, the bottleneck
is not supply. Say so kindly, and offer the alternatives: screen what is
already live, construct rather than discover (found words are occupied by
definition), or pick something serviceable and revisit later.

Renaming later works, and the biggest names did it. Yahoo! was *Jerry and
David's Guide to the World Wide Web*. Google was *BackRub*. Zoho spent its
first thirteen years as AdventNet and renamed only after the product line it
is now known for existed.

And be honest that no candidate will *feel* right on day one. Google is a
misspelled maths term. Yahoo is a dictionary insult with a punctuation mark
bolted on to dodge a barbecue sauce. Zoho is a meaningless syllable pair
derived from an office-equipment acronym. The affection comes from the
company, not the word.
