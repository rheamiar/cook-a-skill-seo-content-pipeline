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

Use web search to estimate keyword data from free sources:

| Signal | Free source | How to extract |
|---|---|---|
| Search volume estimate | Google Autocomplete | Search the keyword — more autocomplete variants = higher volume |
| Search volume estimate | Ubersuggest free | Search ubersuggest.io — extract volume from snippet if visible |
| Search volume + KD | Semrush Free Keyword Tool | semrush.com/analytics/keywordoverview — free tier shows volume, KD, CPC for 10 searches/day |
| Keyword difficulty estimate | Google Search results | Count exact-match domains in top 10 — more = higher difficulty |
| Long-tail discovery | Google People Also Ask | Extract all PAA questions as long-tail keyword candidates |
| Long-tail discovery | Google Related searches | Extract bottom-of-page related searches |

Label all free-source data as `[estimated]` in the output table.
Flag the overall keyword research output as `[Free mode — estimates only]`.
Recommend the user verify with Ahrefs before making publishing decisions.
