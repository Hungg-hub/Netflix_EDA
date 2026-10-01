# Netflix Catalog Empirical EDA & Econometric Analysis

## Overview
This repository contains an exploratory data analysis (EDA) and econometric modeling project investigating content length, catalog shifts, and series survival dynamics on Netflix. Using historical title metadata (7,787 entries: 5,377 movies and 2,410 TV shows), this project tests whether the observed contraction in modern film runtimes is statistically significant and whether it persists after controlling for genre and audience maturity ratings.

---

## Key Research Questions
1. **Movie Runtime Evolution (1960s–2020s):** Have movie durations compressed over time, and is the difference across decades statistically significant?
2. **TV Series Longevity & Attrition:** What is the survival drop-off rate across serialized television seasons?
3. **Multivariate Attribution (OLS Regression):** Does film runtime decay over time when holding genre categories and content maturity ratings constant?

---

## Core Findings

### 1. Movie Runtime Compression Across Decades
- **Descriptive Metrics:** Mean movie runtime decreased from 112.64 minutes in the 2000s to 96.76 minutes in the 2010s (a 15.88-minute contraction), continuing downward to 89.52 minutes in the 2020s.
- **Welch's Two-Sample t-Test (2000s vs. 2010s):**
  - $t = 12.9432, \, p = 8.91 \times 10^{-35}$ (Degrees of freedom $\approx 761.4$).
  - Decisively rejects $H_0$; the ~16-minute reduction is statistically significant with a moderate-to-large effect size (Cohen's $d \approx 0.60$).
- **Kruskal-Wallis Omnibus Test (2000s, 2010s, 2020s):**
  - $H = 182.0766, \, p = 2.90 \times 10^{-40}$.
  - Confirms non-parametric rank shift across modern streaming eras.

### 2. TV Series Longevity & The Season 1 Cliff
- **Season 1 Dominance:** Exactly **66.72%** (1,608 out of 2,410 shows) end after their debut season.
- **Attrition Velocity:** Only **15.85%** (382 shows) reach Season 2, marking a 76.25% drop-off in series continuation.
- **Franchise Scarcity:** Just 6.18% of shows reach Season 5 or beyond, reflecting an aggressive "test-and-abandon" commissioning strategy focused on customer acquisition via new season premieres rather than long-running IP.

### 3. Multivariate OLS Regression: Predictors of Movie Duration

An Ordinary Least Squares regression model was fitted on 4,918 movies:

$$ \text{duration} = \beta_0 + \beta_1(\text{ReleaseYear}) + \beta_2(\text{Rating}) + \sum \beta_k(\text{Genre}_k) + \epsilon $$

- **Model Fit:** $R^2 = 0.269$, Adjusted $R^2 = 0.268$, $F(11, 4906) = 164.4$, $p = 4.94 \times 10^{-324}$
- **Time Effect:** $\beta_{\text{year}} = -0.3503$ ($p < 0.001$). Holding genre and rating constant, film runtime shortens by ~0.35 minutes per year (~3.5 minutes per decade). This proves runtime compression is not an illusion caused by acquiring short documentaries or stand-up specials.

---

## Dataset
- **File:** `NetFlix.csv`
- **Total Records:** 7,787 rows $\times$ 12 columns
- **Features:** `show_id`, `type`, `title`, `director`, `cast`, `country`, `date_added`, `release_year`, `rating`, `duration`, `genres`, `description`.
- **Missing Data Handling:** Non-null values across all core analytical variables (`duration`, `type`, `release_year`, `genres`). Selective local row removal (`N = 7`) was applied only for missing ratings in the regression section to avoid discarding 38% of records due to unlisted directors.

---

## Project Structure
```text
├── data/
│   └── NetFlix.csv                                    # Raw dataset
├── notebooks/
│   └── Exploratory_Data_Analysis_Netflix.ipynb        # Complete analysis notebook
├── reports/
│   └── Exploratory_Data_Analysis_Report.pdf           # Formatted summary report
├── README.md                                          # Project documentation
