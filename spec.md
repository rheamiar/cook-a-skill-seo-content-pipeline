day 1: spec approved by supervisor
day 2: updated GEO rule, countinuously tested skill and edited spec

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

1. First ask: "Do you have a product spec file (.md) you'd like me to reference? If yes, paste the contents here. If not, just share the topic and I'll proceed."
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

---

### Data Collection Process

#### Step 1 — Generate seed keywords
Before fetching data, brainstorm 8–12 candidate keywords based on the topic. Consider:
- Head terms (1–2 words)
- Mid-tail (3–4 words)
- Long-tail / question variants (5+ words, "how to...", "best...", "what is...")

#### Step 2 — Fetch Google Trends data
For each seed keyword, use **web search** with these queries:
- `google trends [keyword] 2024 2025` → look for trend direction (rising / stable / declining)
- `site:trends.google.com [keyword]` → check if any direct result available

Extract from search results:
- **Trend direction**: Rising 📈 / Stable ➡️ / Declining 📉
- **Trending score**: estimate 0–100 based on search result context
- **Seasonal pattern**: year-round vs. seasonal (note peak months if found)

#### Step 3 — Fetch X (Twitter) trending data
For each seed keyword, use **web search** with:
- `site:x.com [keyword]` OR `[keyword] trending twitter 2025`
- `[keyword] discussion reddit OR twitter OR forum`

Extract:
- **Social buzz level**: High / Medium / Low
- **Discussion angle**: what people are actually talking about (pain points, questions, debates)
- **Notable hashtags** if any

#### Step 4 — Fetch Ahrefs data (API)
> ⚠️ **Requires Ahrefs API key.** Ask the user: *"Could you provide your Ahrefs API key? It will only be used during this session."*

Use Ahrefs Keywords Explorer API endpoint:

```
GET https://api.ahrefs.com/v3/keywords-explorer/overview
Headers: Authorization: Bearer {AHREFS_API_KEY}
Params:
  - keywords: [comma-separated list of seed keywords]
  - country: vn  (or user's target market: us, sg, etc.)
  - select: keyword,volume,keyword_difficulty,clicks,cpc
```

Extract for each keyword:
- **Monthly search volume** (exact number)
- **Keyword Difficulty (KD)**: 0–100 → map to Low (0–29) / Medium (30–59) / Hard (60–100)
- **CPC**: signals commercial intent

> 💡 If Ahrefs API is unavailable in this session, fall back to: ask user to paste raw data from Ahrefs UI, then parse it.

#### Step 5 — Score & select keywords
Build a combined score for each keyword:

| Signal | Weight | Scoring |
|---|---|---|
| Ahrefs Volume | 35% | log scale: <100=2, 100–1K=4, 1K–10K=7, 10K+=10 |
| Keyword Difficulty (inverse) | 30% | KD 0–29=10, 30–59=6, 60–79=3, 80+=1 |
| Google Trends score | 20% | Rising=9, Stable=6, Declining=2 |
| X/Social buzz | 15% | High=9, Medium=5, Low=2 |

**Combined Score** = weighted average → rank all keywords → pick top 1 as primary, next 5–8 as secondary.

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

**Level 1 — No API but has Ahrefs account:**
Ask the user: *"Could you go to Ahrefs > Keywords Explorer > paste the following keywords > export CSV and paste the results here?"*
Provide the list of seed keywords. Parse the pasted data and continue from Step 5 normally.

**Level 2 — No Ahrefs account at all (demo / free mode):**
Use web search to estimate keyword data from free sources:

| Signal | Free source | How to extract |
|---|---|---|
| Search volume estimate | Google Autocomplete | Search the keyword — note how many autocomplete variants appear; more variants = higher volume |
| Search volume estimate | Ubersuggest free | Search `ubersuggest.io [keyword]` — extract volume from snippet if visible |
| Search volume + KD | Semrush Free Keyword Tool | Go to `semrush.com/analytics/keywordoverview` — free tier shows volume, KD, and CPC for 10 searches/day |
| Keyword difficulty estimate | Google Search results page | Search the keyword — count how many exact-match domains appear in top 10; more = higher difficulty |
| Long-tail discovery | Google "People Also Ask" | Search the keyword — extract all PAA questions as long-tail keyword candidates |
| Long-tail discovery | Google "Related searches" | Extract bottom-of-page related searches |

Label all free-source data clearly as `[estimated]` in the output table. Note to the user that these are approximations and recommend verifying with Ahrefs before publishing decisions.

Scoring in Step 5 still applies — use estimated values and flag the overall keyword research output as `[Free mode — estimates only]`.

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
- Each H2: maximum 70 characters — long-tail keywords should be rewritten as a single natural sentence or flowing phrase in the heading (e.g. "How AI Is Used in Crypto Trading" not "AI crypto trading — how it works"); only fall back to placing the keyword in body text if it truly cannot read naturally as a heading — this should be rare; never use the format "keyword — subtitle" or "keyword - subtitle"
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

## Stage 3 — Draft Writing

### Goal
Write the full article following the outline, in a natural, human, authoritative tone.

### Writing Principles

**Structure**
- Intro: Open with a hook (stat, question, bold claim, or story). State the problem. Promise the value.
- Body: Follow the outline. Each H2 section should open with a topic sentence and close with a transition sentence that connects to the next section. Never end a section abruptly.
- H2/H3 consistency: if a section has H3 subsections, all body content must live inside those H3s — do not write floating paragraphs between the H2 heading and the first H3.
- FAQ placement: FAQ is always the last section of the article body, placed after the conclusion, never before it.
- Conclusion: Summarize key points, give a clear takeaway, include a CTA or next step.
- Word count: target 1,200–1,700 words. This is a hard cap — do not exceed 1,700 words. If running long, tighten paragraphs and cut redundant examples; do not remove entire sections. If running short, expand examples and evidence rather than adding new sections.

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
- **Never use dashes anywhere in the article body** — this includes bullet dashes (`- item`), mid-sentence dashes (`X - Y`), and em dashes (`X — Y`). All are strong AI writing signals. Use numbered lists, short paragraphs, or inline enumeration ("first... second... third...") for lists. For connective dashes in sentences, rewrite as two separate sentences or use a comma/colon instead.

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

## Stage 4 — SEO + GEO Optimization Checklist

After drafting, run through this checklist and fix any gaps.

---

### **SEO — Search Engine Optimization**
Optimize for Google and traditional search engines to rank the article.

#### Title & Meta
- [ ] Title tag: 50–60 characters, contains primary keyword near the front
- [ ] Meta description: 150–160 characters, contains primary keyword, has a hook/CTA
- [ ] URL slug: short, lowercase, hyphenated, contains primary keyword

#### Content Structure
- [ ] H1 contains primary keyword (only one H1 in the article)
- [ ] H2s use secondary keywords or question variants
- [ ] Intro paragraph contains primary keyword within first 100 words
- [ ] Conclusion contains primary keyword
- [ ] Word count: within 1,200–1,700 words (hard cap — flag if over)

#### Keyword Usage
- [ ] Primary keyword density: 1–1.5%
- [ ] No keyword stuffing (same phrase repeated unnaturally)
- [ ] LSI/semantic keywords present throughout
- [ ] At least 2–3 long-tail variants used

#### Readability
- [ ] Paragraphs: max 3–4 lines each
- [ ] Flesch Reading Ease: aim for 60+ (readable by general audience)
- [ ] Bullet points / numbered lists used where appropriate
- [ ] No walls of text

#### Internal & External Signals
- [ ] At least 2 internal link suggestions noted (placeholders if URLs unknown)
- [ ] At least 1–2 authoritative external source suggestions noted
- [ ] Image alt text recommendations included (if images are mentioned)

#### Schema / Snippet Opportunities
- [ ] FAQ section present (if relevant) → targets FAQ schema
- [ ] How-to steps present (if relevant) → targets HowTo schema
- [ ] Statistics or data points included (increases E-E-A-T signals)

---

### **GEO — Generative Engine Optimization**
Optimize for AI engines (ChatGPT, Perplexity, Google AI Overview) to cite this article as a source.

**Directness & extractability**
- [ ] Every major question in the article is answered directly and explicitly — AI engines extract clean, self-contained answers
- [ ] Key definitions are stated clearly in 1–2 sentences (not buried across paragraphs)
- [ ] Each H2 section can stand alone and make sense without reading the rest of the article

**Authority signals**
- [ ] At least 3 data points with named sources — AI engines strongly prefer citing articles with verifiable evidence
- [ ] Author expertise signals present: specific experience, credentials, or firsthand knowledge mentioned
- [ ] Article takes a clear stance or conclusion — vague "it depends" articles are rarely cited by AI

**Structure for AI parsing**
- [ ] H2/H3 headings are written as clear topic labels, not clever/vague titles — AI uses headings to understand what each section is about
- [ ] Summary or TL;DR either in intro or conclusion — gives AI a clean snippet to cite
- [ ] No fluff paragraphs that don't add information — AI engines skip low-signal content

**Entity & topic coverage**
- [ ] Key entities (people, tools, brands, concepts) are named explicitly, not referred to vaguely
- [ ] Topic is covered comprehensively enough that AI sees this as a complete source, not a partial one
- [ ] Semantic keywords and related concepts are present — AI engines map topic coverage, not just keyword density

---

## Stage 5 — AI-Pattern Detection & Humanization

### Goal
Identify and eliminate writing patterns that signal AI generation. Replace with natural, human phrasing.

### Known AI-Pattern Library

**Structural Red Flags**
- Starting every section with "In today's [world/landscape/era]..."
- Ending every section with a summary sentence that restates the heading
- Perfect parallel structure across all bullet points (same length, same syntax)
- Transitioning with "Furthermore," / "Moreover," / "Additionally," / "In conclusion,"
- Using exactly 3 bullet points for every list
- Using dashes anywhere in the article body: bullet dashes (`- item`), mid-sentence dashes (`X - Y`), or em dashes (`X — Y`) — all are AI formatting/writing signals; rewrite as separate sentences, use commas/colons, or use numbered lists instead

**Phrase-Level Red Flags**
Scan the draft and flag any of the following. Replace each flagged phrase with human alternatives:

| AI Pattern | Human Alternative Examples |
|---|---|
| "It's important to note that..." | Just state the thing directly |
| "In the realm of..." | "In [specific field]..." or just cut it |
| "When it comes to..." | Cut it — start with the subject |
| "Delve into" | "Explore," "look at," "break down" |
| "Leverage" (used abstractly) | "Use," "apply," "take advantage of" |
| "Navigate the complexities of..." | Be specific about what's complex |
| "In today's fast-paced world..." | Cut entirely, start with real content |
| "It goes without saying..." | If it goes without saying, don't say it |
| "Comprehensive guide / deep dive" | Describe what you actually cover |
| "Game-changer / revolutionary / transformative" | Describe the actual impact |
| "Unlock the potential of..." | Say what the potential actually is |
| "Empower [people] to..." | "Help [people] do [specific thing]" |
| "As we explore in this article..." | Cut — don't narrate your own article |
| "Suffice it to say..." | Cut |
| "At the end of the day..." | Cut or replace with specific conclusion |
| **"[X] represents a..."** | Rewrite: "[X] is..." or lead with the implication directly |
| **"[X] represents the future of..."** | Say what will actually change, with specifics |
| **"[X] represents a significant shift..."** | "Since [year], [X] has changed how [people do Y]" |
| **And-chain: "A and B and C and D"** | Break into 2 sentences, or use a short list |
| **"not only... but also..."** | Usually cut "not only" — just state both things |
| **"both... and..." (overused connector)** | Restructure into separate clauses |

**Conclusion-Specific Red Flags**
Conclusions are where AI patterns cluster most heavily. Scan the conclusion separately for:

| AI Conclusion Pattern | Fix |
|---|---|
| Starts with "In conclusion," / "To summarize," / "In summary," | Cut the opener — start with the actual takeaway |
| Restates every H2 heading as bullet points | Replace with 1–2 sentences of synthesis, not recap |
| Ends with "we hope this article has helped you..." | Cut entirely — end with action or insight |
| "[Topic] represents an exciting opportunity..." | Say what the reader should do with that opportunity |
| Vague closing: "The future of [X] is bright" | Replace with a specific prediction or concrete next step |
| Motivational fluff: "Now is the time to embrace [X]" | Give a specific first action to take |

**Rhythm Red Flags**
- Sentences that are all approximately the same length → vary them
- Every paragraph has exactly the same number of sentences → break the pattern
- No contractions anywhere → add contractions where natural (you're, it's, that's)
- No rhetorical questions → add 1–2 where appropriate
- No personal/direct asides → add occasional "Here's the thing:" or "Think about it this way:"

**Flow & Transition Red Flags**
- Two or more consecutive paragraphs that start with the same word or structure → rewrite openers
- Paragraphs that end abruptly with no bridge to the next → add a 1-sentence transition
- H2 sections that feel like separate articles with no connection to each other → add closing transition sentences
- Body reads like a list of facts rather than a narrative → add causal connectors ("because", "which means", "the result is")
- Zero transition phrases in the entire article → flag and add at least 5

**Structural Red Flags (additional)**
- Content written as floating paragraphs between an H2 and its H3 subsections → move all content inside the H3s
- FAQ section placed before the conclusion → move FAQ to after conclusion
- Headings that use `— ` or ` - ` as a separator between keyword and subtitle → rewrite as single natural sentence or use `:` sparingly
- Tool or project name mentioned without official URL on first mention → add URL in parentheses
- H3 section makes a claim with no example, data, or link → flag as "evidence needed"

### Humanization Instructions
1. Read through the draft and highlight every AI pattern found.
2. Rewrite flagged sections using alternatives from the table above.
3. Add at least 2–3 "human moments": a surprising stat, a counterintuitive point, a concrete micro-example, or a direct question to the reader.
4. Read the final version aloud (mentally) — if it sounds like a robot, rewrite.

---

## Stage 6 — Scoring & Evaluation Report

After completing all stages, produce a structured evaluation of the final article.

### Output Format

```
╔══════════════════════════════════════════════╗
║         SEO CONTENT EVALUATION REPORT        ║
╚══════════════════════════════════════════════╝

ARTICLE: [Title]
KEYWORD: [Primary keyword]
WORD COUNT: [X words]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SCORES (each out of 10)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. SEO OPTIMIZATION          [X/10]
   - Keyword placement:      [✓/✗ notes]
   - Title & meta:           [✓/✗ notes]  
   - Structure (H tags):     [✓/✗ notes]
   - Keyword density:        [X% — target 1–1.5%]
   - Internal/external links:[✓/✗ notes]

2. HUMAN-STYLE WRITING       [X/10]
   - AI patterns detected:   [count] — [list them]
   - Sentence variety:       [Good/Needs work]
   - Tone naturalness:       [Good/Needs work]
   - Contractions used:      [Yes/No]
   - Personal voice present: [Yes/No]

3. CONTENT QUALITY           [X/10]
   - Accuracy & depth:       [notes]
   - Unique angle/insight:   [notes]
   - Examples & specifics:   [notes]
   - E-E-A-T signals:        [notes]

4. CONTENT FLOW              [X/10]
   - Intro hook strength:      [Strong/Weak — notes]
   - Logical progression:      [notes]
   - Paragraph transitions:    [count transitions present vs. needed]
   - Section transitions:      [Smooth/Choppy — closing sentence present at each H2?]
   - Conclusion clarity:       [notes]
   - FAQ placement:            [✓ after conclusion / ✗ misplaced]
   - H2/H3 structure:          [✓ consistent / ✗ floating content between H2 and H3]
   - Prose vs bullet balance:  [bullet count: X — appropriate/overused]
   - Citation format:          [✓ using "according to" / ✗ using dash format]
   - Evidence per H3:          [X/X sections have concrete example or data]
   - Tool URLs present:        [✓/✗ — first-mention URLs added for all tools]
   - Heading length compliance:[H1: X chars ✓/✗ | H2s within 70 chars: X/X]
   - Heading dash-free:        [✓ clean / ✗ X headings still use dash separators]

5. KEYWORD DISTRIBUTION      [X/10]
   - Primary keyword:        [appears X times — distribution: even/front-loaded/sparse]
   - Secondary keywords:     [coverage: X/X keywords used]
   - LSI/semantic coverage:  [Good/Needs more variety]
   - Over-optimization risk: [Low/Medium/High]

6. GEO OPTIMIZATION          [X/10]
   - Direct answers present: [✓/✗ — AI can extract clean answers]
   - Key definitions clear:  [✓/✗ notes]
   - Authority signals:      [data points cited: X/3 minimum]
   - Heading clarity:        [Good/Needs work — headings as topic labels]
   - Entity coverage:        [Good/Needs work]
   - AI-extractable summary: [✓/✗ — TL;DR or clear conclusion present]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
OVERALL SCORE: [X/60]  →  [X%]
GRADE: [A / B / C / D]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

GRADE SCALE:
A (90–100%): Publish-ready — optimized for both search engines and AI engines
B (75–89%):  Minor revisions recommended
C (60–74%):  Significant improvements needed
D (<60%):    Major rewrite needed

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SUMMARY ASSESSMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

STRENGTHS:
- [Point 1]
- [Point 2]

WEAKNESSES / PRIORITY FIXES:
- [Issue 1 — what to fix and how]
- [Issue 2 — what to fix and how]

QUICK WINS (fixes that take <5 min):
- [Action item]
- [Action item]
```

---

## Usage Notes

- **Entering mid-pipeline**: If user provides an existing article, start at Stage 4 (checklist), then Stage 5 (humanization), then produce Stage 6 (report).
- **Partial runs**: If user only asks for keyword research, run Stage 1–2 only. If they ask to "check" or "score" an article, run Stage 4–6.
- **Language**: Default to the language of the user's topic/request. Do not switch languages mid-pipeline.
- **Tone calibration**: Ask the user for brand voice guidance before Stage 3 if not already clear from context (e.g., formal vs. conversational, B2B vs. consumer).

---

## Quick Reference — AI Phrases to Always Avoid

```
GENERIC OPENERS & FILLERS:
"Delve into" / "In the realm of" / "Navigate the complexities"
"It's important to note" / "It goes without saying"
"In today's fast-paced world" / "In today's digital landscape"
"When it comes to..." / "As we explore in this article"
"At the end of the day" / "Suffice it to say"

INFLATED ADJECTIVES:
"Leverage" (abstract) / "Empower" / "Unlock the potential"
"Game-changer" / "Revolutionary" / "Transformative" / "Comprehensive"

CLUNKY TRANSITIONS:
"Furthermore" / "Moreover" / "Additionally" / "In conclusion,"
"Not only... but also..." / "Both... and..." (overused)

REPRESENTS PATTERN (conclusion red flag):
"[X] represents a..." → rewrite as "[X] is..."
"[X] represents the future of..." → state the specific change
"[X] represents a significant shift..." → "Since [year], [X] has changed how..."

AND-CHAINS (structural red flag):
"A and B and C and D" → break into 2 sentences or a list

DASHES — ALL FORMS (formatting + writing red flag):
"- item" bullet lists → replace with numbered lists or prose
"X - Y" or "X — Y" mid-sentence dashes → rewrite as 2 sentences or use a comma/colon

CONCLUSION KILLERS:
"In conclusion," / "To summarize," / "In summary,"
"We hope this article has helped you..."
"The future of [X] is bright"
"Now is the time to embrace [X]"
```
