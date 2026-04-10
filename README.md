# Marketing-Analytics-Competition

# Instagram Engagement Analytics — Marketing Analytics Competition 2026

![Python](https://img.shields.io/badge/Python-Data%20Analysis-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Processing-orange)
![Statsmodels](https://img.shields.io/badge/Statsmodels-OLS%20Regression-green)
![Google Colab](https://img.shields.io/badge/Notebook-Google%20Colab-yellow)

Data-driven analysis of Instagram engagement across 47 top creators using OLS regression and NLP-based text feature extraction.

---

**Objective:** Identify the content, format, and caption characteristics that drive engagement rate among top Instagram creators, and translate findings into actionable recommendations.

## Key Findings

- **Post format is the single most actionable lever.** Album posts outperform single photos by 15.2% (coef=+0.0103, p<0.001). Videos underperform photos by 65% (coef=-0.0459, p<0.001).

- **Creator identity dominates engagement.** Adding creator fixed effects increased R-squared from 0.163 to 0.618 — 45% of engagement variation is explained by *who* the creator is, not what they post.

- **Longer captions correlate with higher engagement** within a creator's own posting history (coef=1.655e-05, p<0.001), likely reflecting more personal, story-driven content.

- **Tags hurt engagement.** Posts containing @ mentions are negatively associated with engagement (coef=-0.0076, p<0.001), consistent with audience recognition of and disengagement from sponsored or collaborative content.

- **Engagement declined platform-wide in 2023.** A year-over-year drop of 0.018 engagement rate points (p<0.001) confirms platform-level algorithm changes during this period.

---

## Key Insight Visualizations

### Engagement Rate by Day of Week
*(chart image placeholder)*

### Post Format vs. Average Engagement Rate
*(chart image placeholder)*

### Genre × Format Interaction
*(chart image placeholder)*

### Residual Plot — Heteroscedasticity
*(chart image placeholder)*

---

## Overview

This project was submitted as part of the Fordham University Gabelli School of Business Marketing Analytics Competition 2026. The analysis examined 5,975 Instagram posts from 47 top creators published between January 2022 and December 2023.

The central research question: **What are the drivers of online engagement, and how can content creators boost it?**

Four dimensions were examined: caption text features, post format, content genre, and posting day of week. Engagement rate — defined as (Likes + Comments) / Followers at Time of Posting — was selected as the primary KPI to normalize for audience size across creators ranging from 158,000 to 68 million followers.

---

## Business Problem

Instagram creators and brand managers face a common challenge: distinguishing between content choices that genuinely move engagement and those that are simply correlated with creator popularity.

Key questions addressed:

- Which post formats drive the highest engagement across creators and genres?
- Do caption characteristics — hashtags, sentiment, CTAs, length — meaningfully affect performance?
- What role does posting day play, and is it actionable?
- How did platform-wide algorithm changes affect engagement from 2022 to 2023?

---

## Analytical Approach

### Text Feature Extraction

Seven quantitative features were extracted from each post's caption using Python:

| Feature | Description |
|---|---|
| `caption_length` | Total character count |
| `hashtag_count` | Number of hashtags |
| `emoji_count` | Number of emojis |
| `has_cta` | Binary: contains CTA phrase (e.g. "comment," "tag," "link in bio") |
| `has_question` | Binary: contains a question mark |
| `sentiment` | VADER compound score (–1 to +1) |
| `has_tag` | Binary: caption contains an @ mention |

### OLS Regression Model

An OLS regression model predicted engagement rate from text features while controlling for:

- **Creator fixed effects** — 46 binary dummy variables (one per creator) to account for baseline engagement differences
- **Post format** — album and video dummies with photo as the baseline
- **Year** — 2022 vs. 2023 to capture platform-level shifts

Genre was excluded due to severe multicollinearity with creator fixed effects (condition number: 1.15e+16). Removing genre reduced the condition number to 2.26e+04 while leaving R-squared unchanged at 0.617, confirming creator fixed effects already captured genre-level variation.

### Heteroscedasticity Correction

A residual plot revealed a cone-shaped pattern, violating the OLS assumption of constant error variance. HC3 robust standard errors were applied. Nine creators shifted from insignificant to significant post-correction, confirming the original model underestimated consistency among high-follower accounts.

### Multicollinearity Diagnostics

VIF scores were calculated for all text features and control variables. All values fell below 2, well under the conventional threshold of 4.

---

## Model Results

| Variable | Coefficient | p-value | Significant? |
|---|---|---|---|
| Caption Length | 1.655e-05 | 0.004 | ✅ |
| Has Tag (@mention) | -0.0076 | 0.002 | ✅ |
| Is Album | +0.0103 | <0.001 | ✅ |
| Is Video | -0.0459 | <0.001 | ✅ |
| Is 2023 | -0.0182 | <0.001 | ✅ |
| Hashtag Count | — | n.s. | ❌ |
| Emoji Count | — | n.s. | ❌ |
| CTA Presence | — | n.s. | ❌ |
| Question Presence | — | n.s. | ❌ |
| Sentiment | — | n.s. | ❌ |

**R-squared: 0.618 | Observations: 5,975**

---

## Key Insights & Recommendations

**Post albums over photos and videos.**
Carousels significantly outperform both formats. This is the single most impactful format decision a creator can make.

**Write with authenticity.**
Longer captions correlate with higher engagement — likely because they signal personal, story-driven content rather than promotional copy.

**Avoid excessive tagging.**
@ mentions are negatively associated with engagement, suggesting audiences disengage from visibly sponsored or collaborative posts.

**Don't overthink CTAs, sentiment, or emojis.**
These showed no significant effect once creator identity was controlled for. Time is better spent on format and caption depth.

**Benchmark against yourself, not the platform.**
Engagement declined platform-wide in 2023. Creators should track performance against their own historical averages and consider cross-platform diversification.

---

## Limitations

**Creator identity dominance:** 45% of engagement variation is explained by who the creator is, not what they post. Content decisions matter less than audience trust built over time.

**Top creator sample bias:** The dataset covers 47 top creators only. Findings may not generalize to smaller or emerging accounts where content choices likely play a larger relative role.

**Correlation, not causation:** This is an observational study. Significant associations do not confirm that content choices directly cause higher engagement.

---

## Repository Structure

**Root**
- `Text_Analysis.ipynb` — Main analysis notebook (text extraction + OLS regression)
- `README.md` — Project overview and documentation

**data/**
- `Marketing_Analytics_Competition_2026_Dataset.xlsx` — Raw dataset (5,975 posts, 47 creators)

**images/**
- Visualizations used in the analysis and presentation

---

## Tools Used

Python
Pandas
Statsmodels
VADER (NLTK)
Matplotlib
Google Colab

---

## Team

Chris Remmell · Anushka Verma · Winnie Huang · Ariana Idrizaj
MS Marketing Intelligence — Fordham University, Gabelli School of Business
Marketing Analytics Competition 2026 — Milestone Achiever Award & Finalist
