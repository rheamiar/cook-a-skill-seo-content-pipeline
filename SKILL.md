---
name: seo-content-pipeline
description: >
  Full end-to-end SEO content creation pipeline. Primary input is a product spec .md file
  that describes the product, target user, use cases, and differentiators — this is what makes
  output specific rather than generic. Also accepts a plain topic if no spec exists.
  Use this skill whenever the user wants to: write an SEO article, research keywords,
  create a content outline, optimize a blog post, score or audit SEO content quality,
  check if writing sounds AI-generated, improve human-style writing, or run any part of the
  SEO content workflow (keyword research → outline → draft → optimize → score).
  Trigger even if the user only mentions one step — e.g. "write me an article about X"
  or "check my SEO" or "make this sound less AI" — because the full pipeline adds value.
---

# SEO Content Pipeline

A complete, opinionated workflow for producing high-quality SEO content that ranks — and actually reads like a human wrote it. Covers every stage from keyword research to final scoring.

---

## Overview of Stages

```
[1] KEYWORD RESEARCH
      ↓
[2] CONTENT BRIEF & OUTLINE
      ↓
[3] DRAFT — human-style writing
      ↓
[4] SEO + GEO OPTIMIZATION (on-page checklist)
      ↓
[5] AI-PATTERN DETECTION & HUMANIZATION
      ↓
[6] SCORING & EVALUATION REPORT (SEO + GEO)
```

---

## ⚠️ HARD RULES — APPLY TO EVERY WORD OF OUTPUT

These rules override everything else. Violating any of these is an automatic failure at Stage 6 scoring.

**RULE 1 — NO DASHES IN ARTICLE BODY (zero tolerance)**
The article body must contain zero dash characters used as connectors or separators. This means:
- No em dash: `—` between words or clauses (e.g. "AI tools — when used correctly" is FORBIDDEN)
- No hyphen as connector: `X - Y` mid-sentence (e.g. "the result - a faster execution" is FORBIDDEN)
- No `— Source` citation format at end of sentences

To fix: rewrite as two separate sentences, use a comma, use a colon, or restructure the clause entirely.
The ONLY acceptable use of a hyphen is inside a compound word (e.g. "well-known", "long-term", "on-chain") — not as a sentence connector.

**Mandatory scan before outputting draft:** Before showing any draft to the user, search the entire article body for every occurrence of ` — ` and ` - ` (with spaces around them). If any are found outside compound words, rewrite those sentences immediately. Do not output the draft until zero violations remain.

**RULE 2 — WORD COUNT HARD CAP**
Article body must be 1,200–1,700 words. Do not exceed 1,700 under any circumstance.

**RULE 3 — DEFAULT OUTPUT IS PLAIN TEXT**
Never create a file (.docx, .pdf, etc.) unless the user explicitly asks for one.

**RULE 4 — WAIT FOR USER INPUT**
Never auto-start a stage or run research while waiting for a user decision.

---

You may enter at any stage. If the user gives you a topic from scratch, run all 6 stages in sequence. If they hand you an existing draft, start at Stage 4 or 5 as appropriate.

**Before running any stage, always collect these inputs first. Do not proceed until you have them.**

Collect inputs conversationally — ask ONE question at a time, wait for the answer, then ask the next. Do not list all questions at once.

Question sequence — strict one-at-a-time, always wait for user reply before proceeding:

1. First ask: "Do you have a product spec file (.md) you'd like me to reference? If yes, paste the contents here. A good spec should include: topic/product description, target audience, content goal, editorial thesis, tone guidelines, and **content type** (News 800–1,000 words / Opinion & Analysis 1,000–1,300 words / Long-form Guide & Explainer 1,200–1,700 words). If you don't have a spec, just share the topic and content type and I'll proceed."
   → STOP. Wait for the user's reply. Do not ask the next question yet.

2. After receiving answer to question 1, ask: "What is your target market or country? (e.g. Vietnam, US, Singapore — this affects keyword research)"
   → STOP. Wait for the user's reply. Do not ask the next question yet.

3. After receiving answer to question 2, ask: "Do you have an Ahrefs API key? If yes, share it and I'll pull live keyword data. If not, which would you prefer — (A) share the real key now, or (B) proceed with free tools (Google autocomplete, People Also Ask, Semrush estimates) and I'll label everything as [estimated]?"
   → STOP. Wait for the user to explicitly choose Option A or Option B before doing anything else. Do not start Stage 1 or run any research while waiting.

4. Only after the user has answered all 3 questions AND confirmed the Ahrefs option should you begin Stage 1.

IMPORTANT: Never auto-start the pipeline while waiting for a user decision. Never produce a .docx or any file output unless the user explicitly requests it — default output is plain text in the chat.

If the user says they want to run only a specific stage (e.g. "just score my article"), skip the questions that are not relevant to that stage.

---

## Input

### Primary input — Product spec .md (preferred)
A spec .md file describing the product or feature to write content for. This is what separates this skill from a generic SEO prompt — the pipeline reads the spec and customizes every stage around the actual product: keywords are chosen based on product positioning, the outline reflects real use cases, the draft uses product-specific language and examples.

The spec .md should contain (ask the user if missing):
- What the product/feature is and what it does
- Target user and their pain points
- Key use cases and differentiators
- Tone of voice or brand guidelines (if any)
- **Content type** — determines word count target:
  - News / Announcement: 800–1,000 words
  - Opinion / Analysis: 1,000–1,300 words
  - Long-form Guide / Explainer: 1,200–1,700 words (default if not specified)

**If a spec .md is provided:** extract the above information before running Stage 1. Reference it throughout all stages to keep output product-specific.

**If no spec .md is provided:** ask the user before proceeding — *"Do you have a product spec file (.md) I can reference? This helps me tailor keywords, outline, and draft specifically to your product rather than writing generically. If not, just give me the topic and I'll proceed."* If they confirm no spec exists, proceed with topic text only and note that output will be more generic.

### Secondary input — Plain topic text
Accepted as fallback when no spec .md exists. The pipeline runs normally but outputs will be less product-specific.

---

## Stage 1 — Keyword Research

### Goal
Identify 1 primary keyword + 5–10 secondary/LSI keywords, enriched with **real data** from 3 sources:
- 🔴 **Google Trends** — trending score & momentum (via web search)
- 🐦 **X (Twitter)** — social buzz & discussion volume (via web search)
- 🔵 **Ahrefs** — search volume & keyword difficulty (via Ahrefs API)

Stage 1 runs in **2 turns** when in free mode. Do not compress into 1 turn.

---

### Turn 1 — Collect candidates and ask for volume verification

#### Step 1 — Generate seed keywords
Brainstorm 8–12 candidate keywords based on the topic:
- Head terms (1–2 words)
- Mid-tail (3–4 words)
- Long-tail / question variants (5+ words, "how to...", "best...", "what is...")

#### Step 2 — Fetch Google Trends data
For each seed keyword, use web search:
- `google trends [keyword] 2024 2025` → trend direction (rising / stable / declining)
- Extract: trend direction, trending score 0–100, seasonal pattern

#### Step 3 — Fetch X (Twitter) trending data
For each seed keyword, use web search:
- `site:x.com [keyword]` OR `[keyword] discussion reddit OR twitter OR forum`
- Extract: buzz level (High/Medium/Low), discussion angle, notable debates

#### Step 4 — Fetch Ahrefs data
**If user provided Ahrefs API key:** call the API and extract volume, KD, CPC → skip Turn 1 output below, proceed directly to Turn 2 scoring.

**If user is in Level 1 (has Ahrefs account, no API key):** ask user to export CSV from Ahrefs Keywords Explorer and paste here → wait for data → proceed to Turn 2 scoring.

**If user is in Level 2 (no Ahrefs account):** after completing Steps 1–3, output Turn 1 result below and STOP.

#### Turn 1 Output (Level 2 only) — output this, then stop

```
KEYWORD CANDIDATES
Topic: [topic] | Target market: [country]

[list all candidate keywords with Trend and Buzz data only — no volume, no scores]

┌─────────────────────────────────┬────────────┬──────────┐
│ Keyword                         │ Trend      │ Buzz     │
├─────────────────────────────────┼────────────┼──────────┤
│ [keyword 1]                     │ Rising 📈  │ High     │
│ [keyword 2]                     │ Stable ➡️  │ Medium   │
│ ...                             │            │          │
└─────────────────────────────────┴────────────┴──────────┘

Before I score these, would you like to verify search volume and difficulty?
You can check for free on:
- Semrush: semrush.com/analytics/keywordoverview (10 searches/day)
- Keywordtool.io: keywordtool.io

Option A — paste volume + KD data here and I'll score with full formula
Option B — reply "skip" and I'll score based on Trends + social buzz only
```

→ STOP. Wait for user reply. Do not score, do not output final results.

---

### Turn 2 — Score and output final results

Run after user replies to Turn 1 (or immediately if Ahrefs data is available).

#### Step 5 — Score & select keywords

- If Ahrefs data available → use full formula (Volume 35%, KD 30%, Trends 20%, Buzz 15%)
- If user provided manual volume data → same formula
- If user skipped → adjusted weights (KD 40%, Trends 35%, Buzz 25%), flag as [Free mode — volume unverified]

Pick top 1 as primary (target score 8+/10), next 5–8 as secondary.

→ See full formula and weight details: **`references/keyword-scoring.md`**

---

### Output Format

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
KEYWORD RESEARCH RESULTS
Topic: [topic] | Target market: [country]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PRIMARY KEYWORD (Score: X/10)
  Keyword:        [keyword]
  Volume:         [X searches/month — source: Ahrefs]
  Difficulty:     [KD score] → [Low/Medium/Hard]
  Google Trends:  [Rising📈 / Stable➡️ / Declining📉] — score: X/100
  X/Social buzz:  [High/Medium/Low] — "[notable discussion angle]"
  Search Intent:  [Informational/Navigational/Transactional/Commercial]
  CPC:            $[X] (signals [low/medium/high] commercial value)

SECONDARY KEYWORDS:
┌─────────────────────────┬────────┬──────┬────────────┬──────────┬───────┐
│ Keyword                 │ Volume │  KD  │ Trend      │ Buzz     │ Score │
├─────────────────────────┼────────┼──────┼────────────┼──────────┼───────┤
│ [keyword 1]             │  X,XXX │  XX  │ Rising📈   │ High     │  X.X  │
│ [keyword 2]             │  X,XXX │  XX  │ Stable➡️   │ Medium   │  X.X  │
│ [keyword 3]             │    XXX │  XX  │ Declining📉│ Low      │  X.X  │
│ ...                     │        │      │            │          │       │
└─────────────────────────┴────────┴──────┴────────────┴──────────┴───────┘

CONTENT ANGLE RECOMMENDATION:
[1–2 sentences on the unique angle based on what's trending on X
and the gap between search volume vs. social discussion]

KEY INSIGHT FROM SOCIAL DATA:
"[What people are actually debating/asking about this topic on X/forums]"
→ Use this as the hook in your intro and FAQ section.
```

---

### Fallback Mode

Two fallback levels when Ahrefs API is unavailable.

**Important:** In free mode (Level 2), Claude must NOT estimate or generate volume numbers. Free mode is for finding keyword candidates only — volume data must come from the user or be explicitly skipped.

→ See full formula and weight details: **`references/keyword-scoring.md`**

---

## Stage 2 — Content Brief & Outline

### Goal
Build a **logically sequenced outline** that:
1. Follows a narrative arc matching the reader's mental journey (problem → understanding → solution → validation)
2. Maps every long-tail keyword to a specific section
3. Expands naturally with real community reactions & social discussions from Stage 1 data

---

### Step 1 — Determine the Logical Flow Pattern

Before writing the outline, identify which flow pattern fits the topic:

| Pattern | When to use | Arc |
|---|---|---|
| **Problem → Solution** | How-to, guides, fixes | Problem → Why it happens → Solution steps → Validation |
| **What → Why → How** | Educational, explainers | Definition → Importance → Application → Examples |
| **Comparison** | Best X, X vs Y | Context → Criteria → Options → Recommendation |
| **Journey** | Beginner guides, complete guides | Starting point → Stages → End state → Next steps |
| **Argument** | Opinion, trend analysis | Claim → Evidence → Counter-argument → Conclusion |

Pick the pattern that best matches the primary keyword's search intent, then build the outline around that arc.

---

### Step 2 — Map Long-Tail Keywords to Sections

Take all long-tail keywords from Stage 1 (5+ word phrases, question variants) and assign each to a section:

- Each long-tail keyword should **anchor one H2 or H3**
- The heading can be the keyword itself (slightly reworded naturally) or a question form
- A section without a long-tail keyword anchor = filler risk → consider cutting or merging

**Mapping table to build before writing the outline:**
```
Long-tail keyword               → Assigned section        → Heading type
[keyword 1]                     → H2 Section 2            → Question ("How to...")
[keyword 2]                     → H3 under Section 3      → Statement
[keyword 3]                     → FAQ entry               → Question
...
```

---

### Step 3 — Collect Social Reactions for Section Expansion

Using data from Stage 1 (X/social buzz findings), identify sections where community voice can add depth:

For each major H2 section, check:
- Is there a **common misconception** people debate on X/forums about this subtopic? → Add a "Common myth" H3
- Is there a **strong opinion or backlash** about this aspect? → Add a "What people are saying" H3
- Is there a **real user question** that appears repeatedly in comments/threads? → Convert to FAQ entry
- Is there **notable social proof** (viral post, trending discussion) supporting a point? → Cite as supporting evidence in that section

> 💡 Social reaction sections serve dual purpose: they add E-E-A-T signals (real-world evidence) and they match conversational search queries that long-tail voice search picks up.

---

### Step 4 — Build the Outline

Assemble the final outline using the flow pattern from Step 1, keyword map from Step 2, and social expansions from Step 3.

**Rules:**
- H1: contains primary keyword, maximum 60 characters — no dashes, no "keyword — subtitle" format; write as a single natural sentence
- Each H2: maximum 70 characters — long-tail keywords should be rewritten as a single natural sentence or flowing phrase in the heading (e.g. "How AI Is Used in Crypto Trading" not "AI crypto trading — how it works"); only fall back to placing the keyword in body text if it truly cannot read naturally as a heading — this should be rare; never use the format "keyword — subtitle" or "keyword - subtitle"; if the heading is a question, always use natural interrogative word order — "What Are Prediction Markets?" not "What Prediction Markets Are?", "How Do Prediction Markets Work?" not "How Prediction Markets Work?" — structure: question word + auxiliary verb + subject
- Each H3: either a long-tail keyword heading, a social reaction expansion, or a concrete sub-point
- H2/H3 consistency: if an H2 section has H3 subsections, do NOT write standalone body content directly under the H2 before the H3s — move all content into the H3s instead; each H2 should serve as a container label, not a content block
- Section order: Body sections → Conclusion → FAQ (FAQ is always the final section before the end of the article, never before the conclusion)
- Intro: Hook → Problem → Promise (3-part structure, no keyword stuffing here)
- FAQ section: minimum 3 questions, sourced from long-tail question keywords + recurring social questions

---

### Output Format

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CONTENT BRIEF
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Target Keyword:      [primary keyword]
Flow Pattern:        [chosen pattern — e.g. Problem → Solution]
Search Intent:       [type]
Recommended Length:  [X words — must be within 1,200–1,700 words hard cap]
Target Audience:     [who is reading, what they know, what they need]
Content Goal:        [rank / educate / convert / build trust]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
LONG-TAIL KEYWORD MAP
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[long-tail keyword 1]  →  H2: [section title]
[long-tail keyword 2]  →  H3: [subsection title]
[long-tail keyword 3]  →  FAQ: [question form]
[long-tail keyword 4]  →  H3: [subsection title]
...

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SOCIAL EXPANSION POINTS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[Section X] ← add: "[community misconception/debate found on X/forums]"
[Section Y] ← add: "[recurring user question from social threads]"
[Section Z] ← add: "[notable social proof or trending angle]"

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
OUTLINE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

H1: [Title — primary keyword + compelling angle]
    Alt title option: [variation]

── INTRO ──────────────────────────────────
  Hook: [1 sentence — stat / question / bold claim]
  Problem: [what the reader is struggling with]
  Promise: [what this article will give them]

── BODY ───────────────────────────────────

H2: [Section 1 — anchored to long-tail keyword 1]        🔑 [keyword]
  Context: [what this section covers in 1 sentence]
  H3: [Subsection A]
  H3: [Subsection B]
  H3: 💬 Community angle: [social reaction / debate]      ← social expansion

H2: [Section 2 — anchored to long-tail keyword 2]        🔑 [keyword]
  Context: [what this section covers in 1 sentence]
  H3: [Subsection A]
  H3: [Subsection B]

H2: [Section 3 — anchored to long-tail keyword 3]        🔑 [keyword]
  Context: [what this section covers in 1 sentence]
  H3: [Subsection A]
  H3: 💬 Community angle: [recurring question from forums]  ← social expansion

[... continue for all mapped keywords ...]

── FAQ ────────────────────────────────────
H2: Frequently Asked Questions

  H3: [Question from long-tail keyword]?                  🔑 [keyword]
  H3: [Question from social discussion]?                  💬 social source
  H3: [Question from long-tail keyword]?                  🔑 [keyword]

── CONCLUSION ─────────────────────────────
  Summary: [key points in 2–3 bullets]
  Takeaway: [the one thing they should remember]
  CTA: [what to do next]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
KEYWORD COVERAGE CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Primary keyword:    H1 ✓ | Intro ✓ | H2 ✓ | Conclusion ✓
Long-tail keyword 1: [assigned section] ✓
Long-tail keyword 2: [assigned section] ✓
Long-tail keyword 3: [assigned section — FAQ] ✓
Unplaced keywords:  [list any not yet mapped → decide: add section or cut]
```

---

### ✋ Content Brief Approval — STOP before Stage 3

After outputting the outline above, STOP. Do not proceed to Stage 3 until the user explicitly approves.

Ask the user:
"Here's your content brief and outline. Before I start writing, please review:
- Does the outline structure look right?
- Any sections to add, remove, or reorder?
- Any angle or tone adjustments?

Reply 'approved' or share your edits and I'll update the outline before writing."

→ STOP. Wait for explicit approval or edits. Do not start writing the draft until user confirms.

---

## Stage 3 — Draft Writing

### Stage 3a — Write the Draft

### Goal
Write the full article following the outline, in a natural, human, authoritative tone.

### Writing Principles

**Structure**
- Intro: Open with a hook (stat, question, bold claim, or story). State the problem. Promise the value.
- Body: Follow the outline. Each H2 section should open with a topic sentence and close with a transition sentence that connects to the next section. Never end a section abruptly.
- H2/H3 consistency: if a section has H3 subsections, all body content must live inside those H3s — do not write floating paragraphs between the H2 heading and the first H3.
- FAQ placement: FAQ is always the last section of the article body, placed after the conclusion, never before it.
- Conclusion: Summarize key points, give a clear takeaway, include a CTA or next step.
- Word count: follow the content type specified in the spec — News 800–1,000 words / Opinion & Analysis 1,000–1,300 words / Long-form Guide & Explainer 1,200–1,700 words. Default to Long-form if not specified. This is a hard cap — do not exceed the upper limit. If running long, tighten paragraphs and cut redundant examples; do not remove entire sections. If running short, expand examples and evidence rather than adding new sections.

**Transitions & Flow**
Every paragraph must connect to the next. Use transitional phrases and sentence bridges to avoid the "list of facts" feeling:
- Between sentences: "This matters because...", "The result is...", "That said...", "Here is where it gets interesting:", "The catch is..."
- Between paragraphs: Start the new paragraph with a word or phrase that picks up from the previous one — echo a key term, use a contrasting opener ("But that edge has a limit."), or use a bridging question ("So what does that mean in practice?")
- Between H2 sections: End each H2 block with 1 sentence that signals the transition — e.g. "That explains the upside. The downside is less discussed."
- Never start two consecutive paragraphs with the same word or sentence structure.

**Heading Formatting Rules**
- Never use dashes (`-` or `—`) in headings to separate a keyword from a subtitle. Long-tail keywords should always be rewritten into headings as a single natural sentence or flowing phrase. Only move a keyword to body text if it truly cannot be made readable as a heading — this should be rare, not the default.
- If a colon is needed in a heading, limit to one per article — overuse of colons in headings is an AI signal.
- H1 maximum: 60 characters. H2 maximum: 70 characters. H3 maximum: 65 characters.
- Headings must read as natural English phrases or questions, not keyword strings.

**Bullet Point Rules**
Bullets are allowed but must be used selectively:
- USE bullets for: genuinely parallel items of equal weight (a list of tools, a list of steps, a checklist) where each item is short and self-contained
- DO NOT use bullets for: ideas that have a logical sequence, content that can flow as prose with transitions, or any list where items have different levels of complexity
- When in doubt: write it as prose with connectors ("first... second... third..." or "one option is... another is...") — prose with transitions always reads more naturally than a bullet list
- Maximum 2 bullet lists per article — if you are reaching for a third, convert it to prose

**Citation Format**
Never use `— Source` or `- Source` at the end of a sentence. Always cite inline using one of these formats:
- "According to [Source], [stat]."
- "[Stat] ([Source], [Year])."
- "[Stat], according to [Source]'s [Year] report."
When referencing tools, platforms, or projects, include the official URL in parentheses on first mention — e.g. Token Metrics (tokenmetrics.com) — so readers do not accidentally find scam/clone sites.

**Evidence & Examples Requirements**
Every H3 section that makes a specific claim must include at least one of:
- A concrete real-world example with a named event, date, or company
- A data point with a named source
- A link to a credible reference (official site, research paper, news article)
Sections that only contain assertions without evidence will be flagged in Stage 5 and penalized in Stage 6 scoring.

**Tone & Voice**
- Write like a knowledgeable person explaining to a smart friend — not a textbook, not a press release.
- Use "you" to address the reader directly.
- Vary sentence length: mix short punchy sentences with longer explanatory ones.
- Use concrete examples, analogies, and specific numbers where possible.
- Avoid hedging phrases and filler words (see Stage 5 for full AI-pattern list).
- **No dashes in article body** — See Hard Rules, Rule 1 for full detail and fix instructions.

**Data, Statistics & Source Requirements**

Every article must contain a minimum of **3 data points or statistics** distributed across the body. A draft with no numbers and no sources = fails at scoring stage.

Rules for data usage:
- **Prioritize recent data**: prefer sources from the last 2 years. If older data is all that exists, note the year explicitly.
- **Source every stat inline**: format as `[stat] — [Source, Year]` e.g. *"53% of mobile users abandon a page that takes over 3 seconds to load — Google/SOASTA, 2023"*
- **Find real stats via web search before drafting**: run searches like `topic statistics 2024`, `topic data report 2025`, `topic survey results` to collect actual numbers before writing.
- **Credible source tiers** (use in order of preference):
  1. Original research: Nielsen, McKinsey, HubSpot, Statista, Pew Research, government agencies, academic papers
  2. Industry publications: Moz, Ahrefs Blog, Semrush Blog, Search Engine Journal, sector-specific outlets
  3. Major news outlets: Reuters, Bloomberg, BBC, AP — for recent events/trends only
  4. Avoid: personal blogs, unverified forums, sources without clear methodology

**Where to place data points:**
- **Intro**: 1 striking stat as the hook or within the first 2 paragraphs — builds credibility immediately
- **Each H2 section**: at least 1 data point grounding the claim made in that section
- **Social expansion H3s**: real engagement figures, survey percentages, or poll data from community discussions
- **FAQ**: where a question has a definitive data-backed answer, lead with the number
- **Conclusion**: 1 forward-looking stat or trend figure to close with authority

**If real data cannot be found via search:**
- Do NOT invent statistics or write vague phrases like "studies show" or "research suggests" without a source
- Instead insert a visible placeholder: `[DATA NEEDED: search "suggested query" to find a stat here]`
- Flag all placeholders so the user knows exactly what to fill in before publishing

**Keyword Integration**
- Primary keyword: appears in first 100 words, in at least one H2, and in conclusion.
- Secondary keywords: woven in naturally — never forced.
- Keyword density: aim for 1–1.5% for primary keyword. Never stuff.

---

### Stage 3b — Mandatory Self-Review (before outputting draft)

After completing the draft, run this entire checklist silently. Fix all violations before showing anything to the user. Output only one draft — the final clean version after all checks pass.

---

**1. Dash scan (Hard Rule 1):**
- Search for every ` — ` and ` - ` in the article body
- For each found: is it inside a compound word (well-known, on-chain)? If not → rewrite the sentence
- Zero violations allowed before proceeding

**2. Word count check (Hard Rule 2):**
- Check word count against content type target from spec (News: 800–1,000 / Opinion: 1,000–1,300 / Long-form: 1,200–1,700)
- If under minimum → expand examples and evidence in existing sections
- If over maximum → tighten paragraphs, cut redundant examples

**3. Citation format check:**
- Search for any `— [Source]` or `- [Source]` at end of sentences → rewrite as `according to [Source]`

**4. Flow check:**
- Does every H2 section end with a transition sentence? If not → add one
- Do any two consecutive paragraphs start with the same word? If yes → rewrite one opener

**5. Evidence check:**
- Does every H3 section have at least one concrete example, data point, or link? If not → flag as `[EVIDENCE NEEDED: add example here]`

---

**6. SEO check:**
- [ ] Primary keyword in first 100 words, at least one H2, and conclusion
- [ ] Primary keyword density: 1–1.5% — not stuffed, not sparse
- [ ] At least 2–3 long-tail variants used naturally
- [ ] H1 max 60 chars, H2 max 70 chars, H3 max 65 chars
- [ ] Paragraphs max 3–4 lines — no walls of text
- [ ] At least 2 internal link placeholders noted
- [ ] At least 1–2 external authoritative sources noted
- [ ] FAQ section present → targets FAQ schema
- [ ] At least 3 data points with named sources

**7. GEO check:**
- [ ] Every major question answered directly and explicitly in 1–2 sentences
- [ ] Key definitions stated clearly — not buried across paragraphs
- [ ] Article takes a clear stance — no vague "it depends" conclusions
- [ ] H2/H3 headings are clear topic labels, not clever/vague titles
- [ ] TL;DR or clear summary present in intro or conclusion
- [ ] Key entities (tools, brands, concepts) named explicitly with URLs on first mention

---

**8. AI-pattern scan:**

Scan the full draft against the pattern library → **`references/ai-pattern-library.md`**

Then run burstiness check:
- Sentence length: if 3+ consecutive sentences are similar length (all 15-20 words or all 8-12 words) → insert a very short sentence (3-6 words) or a very long one (30+ words) to break the pattern
- Fragment intentional: add 2-3 deliberate short fragments at paragraph openers or after a strong point — "That's the problem." / "Not quite." / "Here's why."
- Sentence starters: if 3+ sentences start with the same word (The / This / It / AI) → rewrite at least one opener; occasionally start with "And", "But", "So"
- Numbers: replace round numbers with specific ones where source allows — "around 30%" → "27%" — specific numbers read as more credible and less AI
- Lexical unpredictability: in each H2 section, replace at least one predictable word choice with a less obvious alternative — "important" → "worth noting", "shows" → "points to", "many people" → "a lot of traders"

Add at least 2–3 human moments: a surprising stat, a counterintuitive point, a concrete micro-example, or a direct question to the reader.

---

Only after all 8 checks pass → output the single final draft.

---

## Stage 4 — Scoring & Evaluation Report

After completing Stage 3, produce a structured evaluation of the final article.

### Output Format

Grade across 6 dimensions (10 points each, 60 total): SEO Optimization, Human-Style Writing, Content Quality, Content Flow, Keyword Distribution, GEO Optimization. Output includes overall score, letter grade (A/B/C/D), strengths, priority fixes, and quick wins.

→ See full scoring rubric with all sub-criteria and output template: **`references/scoring-rubric.md`**

### ✋ Output Format — ask after scoring report

After delivering the scoring report, ask the user:
"Would you like me to export the full article as a file?
- Option A — plain text in chat (default, already done)
- Option B — export as .docx file"

→ STOP. Wait for user reply. Only create a file if user explicitly chooses Option B.

---

## Usage Notes

- **Entering mid-pipeline**: If user provides an existing article, run Stage 3b checklist (SEO + GEO + AI-pattern), then produce Stage 4 scoring report.
- **Partial runs**: If user only asks for keyword research, run Stage 1–2 only. If they ask to "check" or "score" an article, run Stage 3b checklist then Stage 4.
- **Language**: Default to the language of the user's topic/request. Do not switch languages mid-pipeline.
- **Tone calibration**: Ask the user for brand voice guidance before Stage 3 if not already clear from context (e.g., formal vs. conversational, B2B vs. consumer).

---

## Quick Reference

→ Full AI pattern library with fix instructions:
**`references/ai-pattern-library.md`**

→ Full scoring rubric with all sub-criteria:
**`references/scoring-rubric.md`**

→ Keyword scoring formula and fallback modes:
**`references/keyword-scoring.md`**
