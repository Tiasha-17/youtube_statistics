# YouTube Performance and Community Health Analysis

This is another end-to-end data science portfolio project.  
I used YouTube video and sampled comment data to move beyond basic engagement ranking and answer business questions on content success, fair performance evaluation over time, and moderation prioritization.

## Project Objective
The main goal of this project is to identify what makes videos successful, how content should be compared fairly over time, and what practical actions can improve community health.

## Business Questions
1. Beginner Analysis
- Which videos rank highest by engagement score?
- Which keyword categories perform best?
- How do like-to-view ratio and average sentiment vary across top content?

2. Intermediate Analysis
- How can content effectiveness be evaluated fairly over time?
- Which publishing cohorts perform better on an age-adjusted basis?
- Is sentiment strongly related to performance?

3. Advanced Analysis
- Which videos should be prioritized for moderation review?
- Which content categories have weaker community health?
- How should moderator effort be allocated across categories?

## Dataset
- Files: `videos_stats.csv`, `comments.csv`
- Total raw video rows: `1,881`
- Unique videos after dedupe: `1,869`
- Total comment rows: `18,409`
- Keyword categories: `41`
- Date range: `2007-07-16` to `2022-08-24`
- Comment coverage: sampled comments linked to all `1,869` unique videos

## Tech Stack
- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn

## Repository Structure
```text
youtube_statistics/
|- videos_stats.csv
|- comments.csv
|- analysis.ipynb
|- README.md
|- PRESENTATION_SCRIPT.md
|- requirements.txt
|- .gitignore
```

## Analysis Workflow
1. Data loading and validation.
2. Video cleaning and duplicate-video consolidation.
3. Comment sentiment aggregation to the video level.
4. Feature engineering (`engagement_score`, engagement ratios, `engagement_per_day`, cohort percentiles).
5. Keyword-level success analysis.
6. Performance framework construction across publish-year cohorts.
7. Moderation-risk scoring and category health analysis.
8. Advanced extensions:
- moderation watchlist prioritization
- community health scoring by keyword category
- moderator effort allocation

## Core KPIs
- Total Views: `21,758,948,788`
- Total Likes: `315,763,700`
- Total Comments: `14,611,617`
- Total Engagement Score: `22,073,727,769`
- Overall Average Like-To-View Ratio: `3.36%`

### Publish-Year Trend
| Publish Year | Videos | Avg Engagement / Day | Avg Performance Score | Avg Sentiment |
|---|---:|---:|---:|---:|
| 2007 | 2 | 7,780 | 48.32 | 1.55 |
| 2008 | 1 | 1,121 | 56.21 | 1.20 |
| 2009 | 9 | 19,371 | 42.54 | 1.70 |
| 2010 | 6 | 2,511 | 42.77 | 1.63 |
| 2011 | 4 | 18,221 | 52.43 | 1.68 |
| 2012 | 12 | 1,491 | 41.51 | 1.44 |
| 2013 | 6 | 58,336 | 45.84 | 1.53 |
| 2014 | 10 | 25,112 | 43.04 | 1.48 |
| 2015 | 15 | 1,474 | 48.65 | 1.58 |
| 2016 | 34 | 9,476 | 44.68 | 1.50 |
| 2017 | 47 | 4,791 | 47.08 | 1.67 |
| 2018 | 57 | 27,718 | 47.34 | 1.62 |
| 2019 | 86 | 9,511 | 49.01 | 1.53 |
| 2020 | 158 | 9,160 | 49.37 | 1.62 |
| 2021 | 229 | 9,149 | 49.20 | 1.55 |
| 2022 | 1,193 | 1,536 | 51.01 | 1.44 |

## Answers to Business Questions

### 1) Beginner Analysis
- Highest-engagement videos include:
- `El Chombo - Dame Tu Cosita feat. Cutty Ranks (Official Video) [Ultra Music]`: `4,051,300,647`
- `Martin Garrix - Animals (Official Video)`: `1,593,623,628`
- `The Weeknd - Save Your Tears (Official Music Video)`: `922,551,152`
- Top keyword groups by success score:
- `mrbeast`: `0.826`
- `music`: `0.757`
- `tutorial`: `0.704`
- `asmr`: `0.684`
- `marvel`: `0.668`
- Highest average like-to-view ratio categories:
- `crypto`: `7.08%`
- `reaction`: `6.76%`
- `gaming`: `6.52%`
- Highest average sentiment categories:
- `lofi`: `1.83`
- `asmr`: `1.74`
- `music`: `1.74`

### 2) Intermediate Analysis
- Raw engagement is not a fair standalone metric because older viral videos dominate the rankings.
- The performance framework combines:
- cohort engagement percentile
- like-to-view percentile
- sentiment percentile
- Overall sentiment-to-performance correlations are weak:
- average sentiment vs `engagement_per_day`: `0.0157`
- negative sentiment ratio vs `engagement_per_day`: `-0.0247`
- controversy vs `engagement_per_day`: `-0.0059`
- Recent standout videos within the `2022` cohort include:
- `World’s Most Dangerous Escape Room!`
- `I Built Willy Wonka's Chocolate Factory!`
- `$10,000 Every Day You Survive Prison`
- Interpretation: newer content should be judged within its publish cohort, not against all legacy videos at once.

### 3) Advanced Analysis
- `20.92%` of videos fall into `watchlist` or `urgent_review` based on moderation priority.
- Highest-risk videos include:
- `history of the entire world, i guess`: `0.965`
- `I Ate A $70,000 Golden Pizza`: `0.951`
- `I Went Back To 1st Grade For A Day`: `0.943`
- Weakest community-health categories:
- `cnn`: `37.54`
- `news`: `49.67`
- `trolling`: `55.95`
- `history`: `58.42`
- `education`: `61.51`
- Highest moderator-effort priorities:
- `cnn`: `3.90%`
- `mrbeast`: `3.76%`
- `history`: `3.59%`
- `google`: `3.45%`
- `trolling`: `3.28%`

## Advanced Analysis

### Moderation Risk Proxy
I built a moderation layer that combines negative sentiment percentile, controversy percentile, comment volume percentile, and reach percentile into a single `moderation_priority` score.

- Highest-risk videos were flagged as `urgent_review`
- `20.92%` of all videos fell into `watchlist` or `urgent_review`
- Because comments are sampled and untimestamped, this is a moderation-risk proxy rather than a true negative-sentiment spiral detector

### Community Health Scoring
I created a `community_health_score` for each keyword category using average sentiment, negative ratio, controversy, moderation priority, and flagged-video share.

- Lowest health categories were `cnn`, `news`, `trolling`, `history`, and `education`
- This helps identify where negative audience dynamics are more likely to appear

### Moderator Resource Allocation
I converted category risk into `moderator_effort_share_pct` to estimate where response time should go first.

- `cnn`, `mrbeast`, `history`, `google`, and `trolling` received the highest priority shares
- This turns sentiment and controversy data into a staffing and triage decision aid

## Key Findings Summary
- A small set of viral legacy videos dominates raw engagement rankings.
- `mrbeast`, `music`, `tutorial`, `asmr`, and `marvel` were the strongest keyword groups.
- Like efficiency is highest in `crypto`, `reaction`, and `gaming`.
- Sentiment is only a weak predictor of age-adjusted performance in this dataset.
- Community risk is concentrated in a handful of categories rather than spread evenly across all content.
- About one-fifth of videos would merit at least watchlist-level moderation review under this scoring system.

## Business Recommendations
- Use raw engagement for first-pass ranking, not final performance evaluation.
- Compare newer videos within their publish cohorts using age-adjusted metrics.
- Use keyword success scores to guide content strategy toward stronger categories.
- Prioritize moderation coverage on low-health and high-effort categories first.
- Collect timestamped comments in future versions to support true sentiment-trend monitoring.

## How to Run
1. Clone the repository.
2. Install dependencies:
```bash
pip install -r requirements.txt
```
3. Open the notebook:
```bash
jupyter notebook analysis.ipynb
```
4. Run all cells from top to bottom.

## What I Learned
- Content analytics becomes more useful when it moves beyond raw ranking.
- Cohort and percentile methods make social-media performance comparisons more fair.
- Sentiment signals are helpful, but they are rarely strong enough to explain performance by themselves.
- Community-health framing makes a content analysis project more decision-ready.

## Next Improvements
- Add comment timestamps for true negative-sentiment spiral detection.
- Reduce keyword-score sensitivity to outlier videos.
- Turn the notebook into a lightweight dashboard.
- Test alternative weighting schemes for community health and moderator effort.
