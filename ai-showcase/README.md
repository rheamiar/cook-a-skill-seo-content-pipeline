# AI Showcase — SEO Content Pipeline

This folder documents key moments from building the SEO Content Pipeline skill across 3 days. Each screenshot shows either a human insight that shaped the skill, or an AI problem-solving moment that improved it.

---

## Screenshot 1 — The initial idea: defining the full pipeline in one prompt

**File:** `01-initial-brainstorm.png`

**What to capture:** The very first prompt of the conversation (Day 1) where I defined the entire skill scope from scratch.

---

## Screenshot 2 — Brainstorm: The 3-source keyword idea

**File:** `02-brainstorm-3-sources.png`

**What to capture:** The moment I proposed combining Google Trends + X/Twitter buzz + Ahrefs as 3 data sources for keyword research — and the conversation where AI explained the API limitations and helped figure out how to make it work anyway.

---

## Screenshot 2 — Designing the keyword scoring formula

**File:** `03-keyword-scoring-formula.png`

**What to capture:** The conversation where the weighted scoring formula was built — Volume 35% / KD 30% / Trends 20% / Social buzz 15% — including the reasoning behind each weight and the log scale for volume.

---

## Screenshot 3 — Akemi feedback → spec.md as primary input

**File:** `04-akemi-feedback-spec-input.png`

**What to capture:** The supervisor feedback from Akemi saying "input must accept a product spec .md file, not just topic text" — and the conversation where this was implemented, turning the skill from a generic SEO tool into a product-specific pipeline.

---

## Screenshot 4 — Discovering the volume hallucination bug

**File:** `05-volume-hallucination-bug.png`

**What to capture:** The screenshot I shared showing Claude generating `[est. 8,000–14,000/month]` volume numbers despite having no real data — and the conversation diagnosing why it happened and how the fix was designed.

---

## Screenshot 5 — Restructuring Stage 1 into Turn 1 / Turn 2

**File:** `06-turn1-turn2-restructure.png`

**What to capture:** The conversation where multiple STOP instructions failed and the solution was to change the flow structure instead — splitting Stage 1 into two turns with different outputs.

---

## Screenshot 6 — Deciding to document the dash limitation honestly

**File:** `07-dash-limitation-decision.png`

**What to capture:** The conversation where I decided to stop trying to fix the em dash compliance issue with more rules, and instead document it as a known limitation in skill-card.md, spec.md, and README.

---
