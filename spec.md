# Spec — SEO Content Pipeline

## Problem

Content writers spend 4–5 hours producing a single SEO article — and still have no reliable way to know if it will rank. The three most common failure modes:

- Google ignores the article entirely (wrong keywords, weak on-page signals)
- AI engines (ChatGPT, Perplexity, Google AI Overview) cite competitors instead
- The article ranks briefly then drops because it reads like AI-generated content

The root cause is not effort — it is process. Keyword research, outlining, drafting, optimizing, and scoring are all done separately, in different tools, with no consistent standard between them. Quality depends on whoever wrote the article that day.

---

## User

**Primary:** Content writers (solo or team) who produce SEO articles regularly and want a repeatable, structured process that does not rely on memory or checklist discipline.

**What they know:** Basic SEO concepts, how to use Ahrefs or Semrush, what a meta description is.

**What they struggle with:** Translating keyword data into a well-structured article, avoiding AI-sounding output, knowing whether an article is actually ready to publish.

---

## Input

| Input | Required | Description |
|---|---|---|
| Product spec `.md` | Recommended | Describes the product/topic, target audience, tone, content goal. Makes output specific rather than generic. |
| Topic (plain text) | Fallback | Used when no spec file exists. Output will be more generic. |
| Target market / country | Required | Affects keyword research (e.g. Vietnam vs US has different volume and competition data) |
| Ahrefs API key | Optional | Enables live keyword data. Without it, skill uses free tools and labels data as [estimated] |

**Example input:**
- Topic: AI in crypto trading
- Target market: US
- Spec file: [paste contents of spec file]
- Ahrefs API key: [key]

---

## Output

A full pipeline report delivered as plain text in chat (no file unless requested), containing:

1. Keyword Research Table — primary keyword with score 8–10/10, secondary keywords ranked by combined score
2. Content Brief + Outline — flow pattern, long-tail keyword map, social expansion points, full H1/H2/H3 structure
3. Full Article Draft — 1,200–1,700 words, human-style, minimum 3 sourced data points, zero AI filler patterns
4. SEO + GEO Checklist — pass/fail per item with notes
5. AI-Pattern Detection Report — patterns found, fixes applied
6. Scoring Report — 6 dimensions x 10 points = 60 total, letter grade, strengths, priority fixes, quick wins

---

## Workflow

**0. Collect inputs** — ask 3 questions one at a time (spec file, target market, Ahrefs key)

**1. Keyword Research**
- Generate 8–12 seed keywords across head, mid-tail, and long-tail
- Fetch Google Trends + X/Twitter buzz via web search
- Fetch volume + KD via Ahrefs API (or free fallback: Semrush, Google PAA)
- Score and rank all keywords with weighted formula

**2. Content Brief & Outline**
- Select logical flow pattern based on search intent
- Map each long-tail keyword to a specific H2 or H3
- Identify social expansion points from Stage 1 data
- Build full outline with keyword coverage check

**3. Draft Writing**
- Write 1,200–1,700 words following the outline
- Integrate keywords naturally, no stuffing
- Cite minimum 3 data points with named sources
- No dashes as connectors, no AI filler phrases

**4. SEO + GEO Optimization**
- Run 20-item SEO checklist (title, meta, structure, keyword density, schema)
- Run 10-item GEO checklist (direct answers, authority signals, entity coverage)
- Flag all items that fail with notes

**5. AI-Pattern Detection**
- Scan for dash usage, AI phrases, rhythm issues, conclusion clichés
- Rewrite all flagged sections with human alternatives

**6. Scoring Report**
- Grade across 6 dimensions (10 points each, 60 total)
- Output letter grade + strengths + priority fixes + quick wins

---

## Edge Cases

| Situation | Skill behavior |
|---|---|
| No spec file provided | Ask user. If confirmed none, proceed with topic only and note output will be generic |
| Claude outputs em dashes or hyphens in article | This is an LLM limitation — Claude may slip despite instructions. Manual review before publishing is recommended. |
| No Ahrefs API key | Offer Level 1 (paste CSV from Ahrefs UI) or Level 2 (free tools: Google PAA, Semrush free, Ubersuggest) |
| User only wants one stage | Skip irrelevant input questions, run only the requested stage |
| Article runs over 1,700 words | Tighten paragraphs and cut redundant examples — do not remove entire sections |
| Real data not found for a stat | Insert placeholder [DATA NEEDED: search "query" here] — never invent statistics |
| User requests a file output | Produce plain text by default. Only create a file if explicitly asked |

---

## Scope — MVP (2 days)

**In scope:**
- All 6 stages running end-to-end in Claude Project
- Ahrefs API integration with 2-level fallback
- AI-pattern detection library (phrases, rhythm, conclusion clichés)
- SEO + GEO dual optimization checklist
- Scoring report with letter grade and actionable fixes

**Out of scope for MVP:**
- Competitor content gap analysis
- Vietnamese language SEO rules
- CMS integration (WordPress/Ghost)
- Google Search Console data as input
- Internal linking suggestions from existing content library
