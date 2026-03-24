# YouTube Project Interview and Presentation Guide

## Project Goal
The goal of this analysis is to understand YouTube performance from two angles:

- content success
- community health

I wanted the project to start with basic engagement analysis, then move into fairer time-based performance evaluation, and finally into moderation prioritization.

## Why This Project Matters
For a content team, high views alone do not tell the full story. A useful analysis should help answer:

- what kind of content performs well
- whether newer content is actually doing well for its age
- which categories may need closer moderation attention

## Questions I Answered
### Beginner
- Which videos rank highest by engagement score?
- Which keyword categories perform best?
- How do like-to-view ratio and average sentiment differ across stronger content?

### Intermediate
- How can performance be compared more fairly over time?
- Which publish-year cohorts show stronger age-adjusted performance?
- Is sentiment strongly related to performance?

### Advanced
- Which videos should be flagged for moderation review?
- Which content categories have weaker community health?
- How should moderator effort be distributed?

## Dataset Snapshot
- 1,881 raw video rows
- 1,869 unique videos after deduplication
- 18,409 sampled comments
- 41 keyword categories
- Publish dates from July 16, 2007 to August 24, 2022

## My Approach
1. Load and inspect the video and comment files.
2. Clean data types and handle duplicate video IDs.
3. Aggregate sampled comment sentiment to the video level.
4. Create beginner metrics such as engagement score and like-to-view ratio.
5. Create intermediate metrics such as engagement per day, percentiles, and cohort comparisons.
6. Create advanced moderation and community-health features.
7. Use charts and summary tables to explain the results clearly.

## Metrics To Explain Clearly
- `engagement_score = views + likes + comments`
- `like_to_view_ratio = likes / views`
- `engagement_per_day = engagement_score / days_live`
- `cohort_engagement_percentile` to compare videos within the same publish year
- `performance_framework_score` to combine age-adjusted performance, like efficiency, and sentiment
- `moderation_priority` to flag high-risk videos
- `community_health_score` to compare keyword categories

## 60-Second Version
I built a YouTube analytics project using Python and Jupyter to evaluate both video performance and community health. I started with a beginner layer that ranks videos using an engagement score and identifies strong keyword categories using like-to-view ratio and average sentiment. Then I built an intermediate framework that compares content more fairly over time using engagement per day, percentiles, and cohort analysis. Finally, I added an advanced moderation layer that scores videos and categories using negative sentiment and controversy signals to help prioritize moderation effort. One important limitation is that the comments are sampled and do not include timestamps, so the moderation monitor is a risk proxy rather than a true sentiment-spiral detector.

## Key Findings To Mention
- The strongest keyword groups by success score were `mrbeast`, `music`, `tutorial`, `asmr`, and `marvel`
- Raw engagement alone is misleading because older viral videos dominate the rankings
- Age-adjusted performance and cohort percentiles give a much fairer view of newer content
- Sentiment was only a weak predictor of performance in this dataset
- The weakest community-health categories were `cnn`, `news`, `trolling`, `history`, and `education`
- The highest moderator-effort priorities were `cnn`, `mrbeast`, `history`, `google`, and `trolling`

## Recommendations
- Use raw engagement for first-pass ranking only
- Use age-adjusted and cohort-based scoring for fairer performance comparisons
- Focus content strategy on stronger keyword groups
- Prioritize moderation resources on low-health and high-risk categories
- Collect timestamped comments in future versions to support real trend detection

## Limitations To Say Honestly
- The comments are sampled rather than full comment histories
- There are no comment timestamps
- The advanced moderation layer is therefore a proxy, not a true time-series monitor
- Duplicate video rows were consolidated, which is practical but still a simplification

## If An Interviewer Asks “What Would You Improve Next?”
- add timestamped comments for true sentiment-trend analysis
- reduce keyword-score sensitivity to outliers
- move the notebook into a dashboard for easier stakeholder use
- test alternative category scoring formulas for moderation planning

## Strong Closing Line
This project shows that I can take raw social-media data, clean it, build useful analytical features, and turn it into a framework that supports both content strategy and moderation decisions.
