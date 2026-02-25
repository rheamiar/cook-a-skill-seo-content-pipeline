# SEO Content Pipeline

> A skill that runs a full end-to-end SEO + GEO content pipeline — from keyword research to publish-ready article with scoring report.

---

cook-a-skill-seo-content-pipeline/
├── SKILL.md              (584 dòng — giảm từ 787)
├── README.md
├── spec.md
├── skill-card.md
└── references/
    ├── ai-pattern-library.md
    ├── scoring-rubric.md
    └── keyword-scoring.md

---

## The Problem This Solves

Writing SEO content manually is slow, inconsistent, and easy to get wrong. Most writers either over-optimize (keyword stuffing, robotic tone) or under-optimize (great writing, zero rankings). This skill closes that gap by running a structured, repeatable pipeline that handles both sides: content that ranks and content that reads like a human wrote it.

**Before this skill:** keyword research in one tab, outline in another, draft in a third, SEO checklist somewhere else, scoring never. Total time: 3–5 hours per article, inconsistent quality.

**After this skill:** one input (topic + optional spec file), one pipeline, one structured output with SEO score, GEO score, and actionable fixes. Time: under 60 minutes.

---

## What It Does

Runs 6 stages in sequence, each building on the previous:

| Stage | What happens |
|---|---|
| 1. Keyword Research | Finds primary + secondary keywords using Google Trends, X/Twitter buzz, and Ahrefs data. Scores each keyword on volume, difficulty, trend, and social buzz. |
| 2. Outline | Builds a logic-driven structure mapped to long-tail keywords. Expands sections with real community reactions from social data. |
| 3. Draft | Writes the full article in human style — varied sentence rhythm, transitions, no AI filler phrases, minimum 3 sourced data points. |
| 4. SEO + GEO Checklist | Runs on-page SEO audit (title, meta, keyword density, schema) plus GEO audit (AI-extractable answers, authority signals, entity coverage). |
| 5. AI-Pattern Detection | Scans for and rewrites AI writing patterns — dash overuse, "represents" constructions, conclusion clichés, rhythm issues. |
| 6. Scoring Report | Grades the article across 6 dimensions (60 points total) with strengths, priority fixes, and quick wins. |

---

## Inputs

**Primary:** Product spec `.md` file describing the product, target audience, tone, and content goal. This is what makes output specific rather than generic.

**Also required:** Target market/country and Ahrefs API key (or fallback to free tools: Semrush, Google autocomplete, People Also Ask).

---

## Hard Rules Built Into the Skill

- Zero dashes used as connectors in article body
- Word count: 1,200–1,700 words hard cap
- Minimum 3 data points with named sources
- FAQ always placed after conclusion, never before
- No file output unless explicitly requested
- Citation format: `according to [Source]`, never `— Source`

---

## Tools Used

Claude (claude.ai Projects) · Ahrefs API · Semrush Free Keyword Tool · Google Trends · X/Twitter web search

---

## Limitations

- Ahrefs API required for accurate volume and KD data — free mode uses estimates only
- Social data from X/Twitter is estimated via web search, not live API
- Skill does not auto-publish or connect to CMS
- Best results on informational and commercial investigation content — not optimized for product pages or landing pages

---

*Built by Vee · LAB3 AI Competition 2026 · Supervisor: Akemi (Product & Business)*
