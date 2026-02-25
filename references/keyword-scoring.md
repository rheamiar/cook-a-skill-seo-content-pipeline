# Keyword Scoring Formula & Fallback Modes

Reference file for Stage 1 — Keyword Research.

## Scoring Formula

| Signal | Weight | Scoring |
|---|---|---|
| Ahrefs Volume | 35% | log scale: <100=2, 100–1K=4, 1K–10K=7, 10K+=10 |
| Keyword Difficulty (inverse) | 30% | KD 0–29=10, 30–59=6, 60–79=3, 80+=1 |
| Google Trends score | 20% | Rising=9, Stable=6, Declining=2 |
| X/Social buzz | 15% | High=9, Medium=5, Low=2 |

**Combined Score** = weighted average across all 4 signals.
Rank all candidate keywords → pick top 1 as primary (target score 8+/10), next 5–8 as secondary.

---

## Fallback Mode

### Level 1 — Has Ahrefs account but no API key

Ask the user: "Could you go to Ahrefs > Keywords Explorer, paste the following keywords, export CSV and paste the results here?"

Provide the list of seed keywords generated in Step 1. Parse the pasted CSV data and continue from the scoring formula above normally.

### Level 2 — No Ahrefs account (free mode)

In free mode, Claude cannot reliably obtain search volume or KD data. Do NOT estimate or generate volume numbers — this leads to hallucinated data.

**What Claude can do in free mode:**

Use web search to find keyword candidates only:

| Goal | Source | How to use |
|---|---|---|
| Long-tail discovery | Google People Also Ask | Search the keyword — extract all PAA questions as long-tail candidates |
| Long-tail discovery | Google Related searches | Extract bottom-of-page related searches |
| Keyword variants | Google Autocomplete | Search the keyword — note autocomplete suggestions as variant candidates |

**What Claude cannot do in free mode:**
- Estimate search volume — do not generate volume numbers without a real data source
- Estimate keyword difficulty — do not score KD without tool data

**After generating keyword candidates, ask the user:**

Question 1: "I've identified [X] keyword candidates. Would you like to verify search volume and difficulty before I continue? I recommend checking on one of these free tools:
- Ahrefs (Standard plan) — Keywords Explorer
- Semrush free — semrush.com/analytics/keywordoverview (10 searches/day)
- Keywordtool.io free — keywordtool.io

If yes, paste the volume and KD data here and I'll score the keywords properly.
If you'd like to skip verification and proceed without volume data, I'll score based on Trends and social buzz only (Volume weight will be excluded from scoring)."

→ STOP. Wait for user reply.

Question 2 (only if user wants to skip): "Understood — I'll proceed without volume data. Note that keyword scores will be based on Google Trends and social buzz signals only, and may not reflect actual search demand. Shall I continue?"

→ STOP. Wait for explicit confirmation before proceeding.

**If user provides manual volume data:** use it in the scoring formula normally.

**If user skips verification:** remove Volume from scoring formula, redistribute weights as follows:
- Keyword Difficulty (inverse): 40%
- Google Trends score: 35%
- X/Social buzz: 25%

Flag output as `[Free mode — volume unverified, scores based on Trends + social buzz only]`.
