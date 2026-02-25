# AI Showcase — SEO Content Pipeline

This folder documents key moments from building the SEO Content Pipeline skill across 3 days. Each screenshot shows either a human insight that shaped the skill, or an AI problem-solving moment that improved it.

---

## Screenshot 1 — The initial idea: defining the full pipeline in one prompt

**File:** `01-initial-brainstorm.png`

**What to capture:** The very first prompt of the conversation (Day 1) where you defined the entire skill scope from scratch.

**Why it matters:** In a single prompt, you defined all 4 core components that became the final skill: keyword research, outline, AI-pattern detection, and scoring report. The pipeline structure that exists today — 6 stages from research to scoring — maps directly to this first message. Nothing was added by accident; the scope was set by you from the start.

**Human insight:** You defined the full product vision before any code or spec was written.

---

## Screenshot 2 — Brainstorm: The 3-source keyword idea

**File:** `02-brainstorm-3-sources.png`

**What to capture:** The moment you proposed combining Google Trends + X/Twitter buzz + Ahrefs as 3 data sources for keyword research — and the conversation where AI explained the API limitations and helped figure out how to make it work anyway.

**Why it matters:** This was the core insight that separates this skill from a generic SEO prompt. Most SEO tools only use search volume and difficulty. Adding social buzz as a signal captures what people are actually debating — not just what they're searching. The keyword angle recommendation that comes out of Stage 1 (e.g. "the fear of missing out vs. fear of being scammed" for AI crypto) comes directly from this design decision.

**Human insight:** You came up with the 3-source idea. AI helped figure out the implementation.

---

## Screenshot 2 — Designing the keyword scoring formula

**File:** `03-keyword-scoring-formula.png`

**What to capture:** The conversation where the weighted scoring formula was built — Volume 35% / KD 30% / Trends 20% / Social buzz 15% — including the reasoning behind each weight and the log scale for volume.

**Why it matters:** This was the hardest technical problem in Stage 1. A keyword with 50,000 searches/month shouldn't score linearly higher than one with 5,000 — the log scale prevents volume from dominating every decision. The weights reflect a specific opinionated stance: difficulty matters almost as much as volume, and social signal is a real tiebreaker.

**AI problem-solving:** Translating the 3-source idea into a concrete, defensible formula.

---

## Screenshot 3 — Akemi feedback → spec.md as primary input

**File:** `04-akemi-feedback-spec-input.png`

**What to capture:** The supervisor feedback from Akemi saying "input must accept a product spec .md file, not just topic text" — and the conversation where this was implemented, turning the skill from a generic SEO tool into a product-specific pipeline.

**Why it matters:** This was the most important product decision in the whole build. Before this fix, the skill was just a well-structured SEO prompt. After it, the skill reads your product context and customizes every stage: keywords chosen for product positioning, outline reflecting real use cases, draft using product-specific language. The spec-ai-crypto.md example shows exactly how this plays out.

**Human insight:** Akemi's feedback + your decision to implement it immediately.

---

## Screenshot 4 — Discovering the volume hallucination bug

**File:** `05-volume-hallucination-bug.png`

**What to capture:** The screenshot you shared showing Claude generating `[est. 8,000–14,000/month]` volume numbers despite having no real data — and the conversation diagnosing why it happened and how the fix was designed.

**Why it matters:** This is a real LLM reliability problem, not a theoretical one. Claude's instinct is to complete tasks and fill in gaps — which means it will generate plausible-looking numbers when it doesn't have real data. The fix wasn't just adding a "don't estimate" rule (which Claude ignores) but restructuring Stage 1 into Turn 1 / Turn 2 so Claude physically cannot score before asking the user to verify volume.

**Human insight:** You caught the bug by testing with real data, not by reviewing the instruction file.

---

## Screenshot 5 — Restructuring Stage 1 into Turn 1 / Turn 2

**File:** `06-turn1-turn2-restructure.png`

**What to capture:** The conversation where multiple STOP instructions failed and the solution was to change the flow structure instead — splitting Stage 1 into two turns with different outputs.

**Why it matters:** This shows real LLM engineering thinking. Adding rules to tell Claude to stop doesn't work reliably — Claude's completion instinct overrides it. The only reliable fix is making it structurally impossible to skip the step: Turn 1 outputs a candidate list with no scores, which forces a user reply before Turn 2 can run scoring. The design insight is "don't fight the instinct, change the structure."

**AI problem-solving + Human judgment:** Multiple failed attempts + the pivot to structural solution.

---

## Screenshot 6 — Deciding to document the dash limitation honestly

**File:** `07-dash-limitation-decision.png`

**What to capture:** The conversation where you decided to stop trying to fix the em dash compliance issue with more rules, and instead document it as a known limitation in skill-card.md, spec.md, and README.

**Why it matters:** This is a product maturity moment. The temptation is to keep adding rules until the problem is solved — but that path leads to a 1,000-line instruction file that's harder to read and still doesn't work. Choosing to be honest about a limitation rather than papering over it is a real judgment call, and it makes the skill more trustworthy, not less.

**Human judgment:** Your call to stop fighting and document instead.

---

## How to use this folder

1. Take screenshots of each conversation moment described above
2. Name them exactly as listed (e.g. `01-brainstorm-3-sources.png`)
3. Upload to this `ai-showcase/` folder on GitHub
4. Done — the README links everything together with context

**Total screenshots needed:** 7
**Estimated time to collect:** 15–20 minutes
