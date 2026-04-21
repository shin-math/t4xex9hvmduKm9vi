# Candidate Ranking System Using Sentence-BERT
## Problem Statement

Talent sourcing companies face significant challenges in identifying suitable candidates for specific job roles. The traditional manual screening process requires recruiters to review large numbers of profiles, making it time-consuming, inconsistent, and prone to bias.

The objective of this project is to design an **automated candidate ranking system** that identifies and ranks candidates based on their relevance to predefined role-specific keywords.

For this project, the keyword search focus is:

**"Aspiring Human Resources"**

**"Seeking Human Resources"**

The system must:

- Rank candidates based on job relevance
- Improve ranking dynamically using recruiter feedback
- Filter irrelevant candidates
- Determine a generalizable cut-off threshold
- Reduce human bias through automation
## Dataset Overview

The dataset contains **104 candidate records** collected from sourcing platforms.

Features
| Column       | Description                        |
| ------------ | ---------------------------------- |
| `id`         | Unique candidate identifier        |
| `job_title`  | Candidate job title                |
| `location`   | Candidate location                 |
| `connection` | Number of professional connections |

Target
| Column | Description                                            |
| ------ | ------------------------------------------------------ |
| `fit`  | Expected candidate relevance score (used conceptually) |

## Exploratory Data Analysis (EDA)

Exploratory Data Analysis was conducted to understand candidate distribution patterns and prepare the dataset for modeling.

## Key Observations
**Connections Distribution**
- Many candidates had **500+ professional connections**
- Over **40 candidates** belonged to this category
- High connections were considered an indicator of professional reach

**Visualizations used:**

- Histogram of connection distribution
- Boxplot to detect outliers

**HR Keyword Presence**

A new feature was created:

contains_hr

This detects whether job titles contain the phrase:

human resources

Result:

- 61 candidates contained HR-related keywords
- HR candidates were prioritized during filtering

Visualization:

- Bar plot showing HR vs Non-HR candidates

**Data Cleaning Steps**

The following preprocessing steps were applied:

- Converted text to lowercase
- Removed punctuation and special characters
- Normalized whitespace
- Converted "500+" connections to numeric value (500)
- Removed duplicate records while ignoring id
- Standardized job titles and locations

These steps ensured consistent and reliable data processing.

## Modeling Approach

The ranking system was developed using **semantic similarity techniques** powered by:

**Sentence-BERT (SBERT)**

Sentence-BERT is a deep learning model designed to generate meaningful sentence-level embeddings that capture semantic meaning.

**Why Sentence-BERT Was Used**

Traditional keyword-based approaches such as TF-IDF rely on exact word matching. These methods fail when synonyms or alternative phrasing are used.

Sentence-BERT improves performance by:

- Understanding sentence meaning
- Recognizing similar phrases
- Handling variations in wording
- Producing higher-quality rankings

TF-IDF was considered as a baseline conceptually, while Sentence-BERT was used as the primary ranking model.

## System Workflow

The project follows a structured workflow:

**Step 1 — Data Cleaning**

Job titles and locations were cleaned to remove noise and ensure consistency.

Connections were normalized:

"500+" → 500

Duplicate rows were removed to prevent ranking bias.

**Step 2 — Embedding Generation**

Job titles were converted into numeric vectors using Sentence-BERT.

Keywords were also converted into embeddings:

"Aspiring Human Resources Seeking Human Resources"

This allowed semantic comparison between candidates and target roles.

**Step 3 — Similarity Calculation**

Cosine similarity was calculated between:

- Candidate job title embeddings
- Keyword embedding

This generated:

Similarity Score

which represents candidate relevance.

**Step 4 — Initial Ranking**

A weighted scoring formula was used:

Initial Fit Score =
0.85 × Similarity +
0.15 × Connection Score

This balances:

- relevance
- professional strength

Candidates were ranked based on this score.

## How the Solution Works and Improves Ranking with Starring
**Objective**

Improve ranking quality using recruiter feedback.

**Method**

When a recruiter **stars a candidate**, the system:

- Extracts embedding of starred candidate
- Computes similarity between all candidates and starred candidate
- Updates ranking scores

Formula used:

Final Score =
0.6 × Initial Fit +
0.4 × Star Similarity

**Evidence of Ranking Improvement**

Ranking lists were compared:

- Before starring
- After starring

Observation:

- Candidates similar to the starred profile moved higher
- Less relevant candidates moved lower
- Ranking distribution became more refined

This demonstrates:

- adaptive learning
- improved candidate prioritization

## Filtering Irrelevant Candidates
**Objective**

Remove candidates that should not appear in the ranking list.

**Method**

Two filtering techniques were applied.

**Similarity Threshold Filtering**

Candidates below threshold:

initial_fit < 0.25

were removed.

This eliminates weak matches.

**HR Keyword Filtering**

Candidates containing:

human resources

were retained even if similarity was slightly lower.

Filtering rule:

Keep candidate if:

initial_fit > threshold
OR
contains_hr = True

**Result**

Irrelevant candidates were filtered effectively, improving ranking accuracy and reducing noise.

## Determining a General Cut-Off Point
**Objective**

Find a cut-off that works across different roles.

**Method**

A **percentile-based dynamic cutoff** was used.

Formula:

Cutoff = 75th percentile of initial_fit scores

Candidates above this threshold were selected.

**Why This Works**

Percentile-based cutoffs adapt automatically to different score distributions.

Benefits:

- Works across multiple job roles
- Avoids fixed arbitrary thresholds
- Preserves high-potential candidates
- Improves scalability

Visualization included:

- Score distribution plot
- Vertical cutoff marker

## Preventing Human Bias
**Objective**

Reduce subjectivity in hiring decisions.

**Implemented Methods**

**Remove Sensitive Information**

The system does NOT use:

- Gender
- Nationality
- Age
- Personal identifiers

Only professional attributes were used.

**Automated Ranking**

All candidate ranking decisions were based on:

- semantic similarity
- numeric scoring

No manual judgment influenced rankings.

**Multi-Star Feedback System**

Instead of relying on a single recruiter:

Multiple starred candidates were used.

Formula:

Multi-Star Score =
Average similarity to multiple starred candidates

**Additional Future Bias-Reduction Ideas**

To further improve fairness:

- Perform periodic fairness audits
- Use anonymized candidate identifiers
- Train models on diverse datasets
- Apply explainable AI techniques
- Monitor demographic balance (if data available)
## Final Results

The system successfully:

- Ranked candidates based on semantic relevance
- Improved ranking dynamically using recruiter feedback
- Filtered irrelevant candidates effectively
- Determined adaptive cutoffs
- Reduced bias through automated decision-making

## Key Insights
- HR-related candidates consistently ranked highest
- Semantic similarity improved relevance detection
- Percentile cutoffs enhanced adaptability
- Multi-star ranking improved fairness
- Connection strength improved ranking quality
## Output Files

Generated outputs:

final_ranked_sbert_candidates.csv

multi_star_ranked_candidates.csv

These contain ranked candidate results.

## Final Outcome

This project demonstrates a **robust AI-powered candidate ranking system** capable of:

- semantic understanding
- adaptive ranking
- intelligent filtering
- scalable threshold selection
- bias-aware automation

The system significantly improves recruiter efficiency and provides a foundation for building advanced talent matching platforms.
