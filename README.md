# AI-Powered Candidate Ranking System using Sentence-BERT

## Project Overview

Recruiters often spend significant time manually reviewing hundreds of candidate profiles to identify suitable applicants for specific job roles. This process is time-consuming, inconsistent, and prone to human bias.

This project presents an **AI-powered candidate ranking system** that automatically identifies and ranks candidates based on their relevance to predefined job keywords using **semantic similarity techniques powered by Sentence-BERT (SBERT)**.

The system improves recruiter efficiency by:

✔ Ranking candidates based on relevance  
✔ Dynamically improving results using recruiter feedback  
✔ Filtering irrelevant candidates  
✔ Determining adaptive selection cutoffs  
✔ Reducing bias through automated ranking logic  

---

# Business Problem

Traditional candidate screening methods rely on:

- Manual keyword search
- Human judgment
- Static filtering rules

These approaches:

- Miss relevant candidates due to wording differences  
- Require significant manual effort  
- Introduce bias into decision-making  

The goal of this project was to **build an intelligent ranking system** that:

- Understands job relevance semantically  
- Learns from recruiter feedback  
- Produces scalable, fair, and consistent rankings  

---

# Dataset Overview

The dataset contains **104 candidate records** collected from sourcing platforms.

### Features

| Column | Description |
|-------|-------------|
| id | Unique candidate identifier |
| job_title | Candidate job title |
| location | Candidate location |
| connection | Number of professional connections |

### Target (Conceptual)

| Column | Description |
|-------|-------------|
| fit | Expected relevance score |

---

# Tools & Technologies

- Python
- Sentence-BERT (SBERT)
- Scikit-learn
- Pandas
- NumPy
- Matplotlib
- Cosine Similarity
- Natural Language Processing (NLP)

---

# Project Workflow — Step-by-Step

This project follows a structured data science pipeline.

---

## Step 1 — Data Cleaning & Preprocessing

Raw data contained inconsistencies such as:

- Mixed text formatting  
- Special characters  
- Duplicate records  
- Non-standard connection values  

### Cleaning Actions

- Converted text to lowercase  
- Removed punctuation  
- Normalized whitespace  
- Converted `"500+" → 500`  
- Removed duplicate records  
- Standardized job titles  

### Why This Matters

Clean data ensures:

- Reliable similarity calculations  
- Consistent ranking logic  
- Reduced noise in modeling  

---

## Step 2 — Feature Engineering

A new feature was created:

### contains_hr

This identifies whether job titles contain:
Human Resources


This allowed prioritization of HR-related candidates.

---

## Step 3 — Embedding Generation

Job titles were converted into **numerical vectors** using:

**Sentence-BERT (SBERT)**

SBERT generates semantic embeddings that capture **meaning**, not just keywords.

### Why SBERT Was Selected

Traditional methods like TF-IDF:

❌ Match only exact words  

SBERT:

✔ Understands sentence meaning  
✔ Handles synonyms  
✔ Improves ranking accuracy  

---

## Step 4 — Similarity Calculation

Cosine similarity was used to compare:

- Candidate embeddings  
- Target keyword embedding  

Output:

**Similarity Score**

This represents candidate relevance.

---

## Step 5 — Initial Candidate Ranking

A weighted scoring formula was used:

Initial Fit Score =
0.85 × Similarity Score
+
0.15 × Connection Score


### Why Connections Were Included

Professional connections were used as a proxy for:

- Industry engagement  
- Professional network strength  

---

## Step 6 — Dynamic Ranking Using Recruiter Feedback

To simulate real-world hiring workflows:

Recruiters can **"star" candidates**.

The system then:

1. Extracts embedding of starred candidates  
2. Computes similarity to other candidates  
3. Updates ranking scores  

### Final Ranking Formula

Final Score =
0.6 × Initial Fit
+
0.4 × Star Similarity


### Result

Candidates similar to starred profiles:

⬆ Move higher in rankings  
⬇ Less relevant candidates move lower  

This introduces **adaptive learning**.

---

## Step 7 — Filtering Irrelevant Candidates

Two filtering strategies were applied.

### 1. Similarity Threshold

Candidates with:
initial_fit < 0.25


were removed.

### 2. Keyword Retention

HR-related candidates were retained even if:

- Similarity was slightly lower

### Filtering Rule
Keep candidate if:

initial_fit > threshold
OR
contains_hr = True


---

## Step 8 — Determining Adaptive Cutoff

Instead of fixed thresholds:

A dynamic percentile method was used.
Cutoff = 75th percentile of scores


### Benefits

✔ Works across different job roles  
✔ Prevents arbitrary filtering  
✔ Improves scalability  

---

## Step 9 — Bias Reduction Techniques

Bias-aware design was incorporated.

The system intentionally excluded:

- Gender  
- Age  
- Nationality  
- Personal identifiers  

Ranking relied only on:

✔ Professional attributes  
✔ Semantic similarity  
✔ Numeric scoring  

---

# Model Comparison

Multiple ranking strategies were tested to validate performance.

Comparisons included:

- Initial ranking vs updated ranking  
- Single-star vs multi-star ranking  
- Filtered vs unfiltered outputs  

Observation:

✔ Ranking quality improved after feedback  
✔ Irrelevant candidates reduced  
✔ Ranking distribution became more meaningful  

---

# Key Results

The system successfully:

✔ Ranked candidates based on semantic relevance  
✔ Improved rankings dynamically using recruiter feedback  
✔ Filtered weak matches  
✔ Determined adaptive cutoffs  
✔ Reduced ranking bias  

---

# Output Files

Generated outputs:
final_ranked_sbert_candidates.csv
multi_star_ranked_candidates.csv


These contain:

- Ranked candidates  
- Updated scores  
- Final selections  

---

# Example Use Cases

This system can be applied to:

✔ Talent acquisition platforms  
✔ Resume screening systems  
✔ Job recommendation engines  
✔ Recruitment automation tools  

---

# Future Improvements

Possible extensions include:

- Integration with real-time applicant tracking systems  
- Adding resume text parsing  
- Incorporating explainable AI methods  
- Training role-specific models  
- Deploying as an API or web service  

---

# My Contribution (For Recruiters & Hiring Managers)

In this project, I independently:

✔ Designed the end-to-end ranking pipeline  
✔ Performed data cleaning and feature engineering  
✔ Implemented Sentence-BERT embeddings  
✔ Built similarity-based ranking logic  
✔ Developed dynamic feedback-based ranking updates  
✔ Designed filtering and cutoff strategies  
✔ Ensured bias-aware ranking design  
✔ Generated final ranked outputs  

This project demonstrates my ability to:

- Build real-world NLP systems  
- Apply machine learning to business workflows  
- Design scalable ranking systems  
- Translate business problems into technical solutions  

---

# Key Skills Demonstrated

- Natural Language Processing (NLP)
- Machine Learning
- Semantic Similarity
- Feature Engineering
- Model Evaluation
- Ranking Systems
- Python Development
- Data Cleaning
- Bias-Aware Modeling
- Business Problem Solving

---

# Conclusion

This project demonstrates the development of a **scalable, intelligent candidate ranking system** capable of improving recruiter productivity and reducing bias in hiring workflows.

By combining **semantic embeddings**, **dynamic feedback learning**, and **adaptive filtering**, this solution showcases how AI can meaningfully enhance real-world talent acquisition systems.

This work highlights my ability to:

✔ Build production-style machine learning pipelines  
✔ Solve business-driven data problems  
✔ Deliver interpretable and scalable solutions  

I welcome feedback and discussion on this work.

