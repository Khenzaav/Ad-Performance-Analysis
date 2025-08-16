# Ad-Performance Analysis

**Author:** Fathima Khenza A  

---

## Abstract  
This project explores how users interact with ads and how ads perform across different demographics and placements.  
Using a dataset containing age, gender, income, location, ad type, topic, placement, clicks, CTR, and conversion rate,  
I analyzed which factors influence engagement and conversions.  

Clustering techniques grouped users by demographics and ads by features, while statistical tests (Mann–Whitney, Chi-square) were used to validate differences.  
The results highlight patterns in user behavior and ad performance, showing which combinations of user groups and ad features work best.  

---

## Introduction  
Ads reach people every day, but not everyone reacts the same way.  
Some ads get clicked more than others — why is that?  

This project studies how demographic factors (age, gender, income, location) and ad features (type, topic, placement) influence ad performance.  
I grouped users and ads using clustering and applied statistical tests to check which differences actually matter.  

**Goal:**  
To understand how people respond to ads and identify which demographic + ad feature combinations perform best.  

---

## Objectives  
- Explore how demographics (age, gender, income, location) influence CTR and conversion rate.  
- Analyze how ad characteristics (type, topic, placement) affect performance.  
- Identify user behavior patterns using clustering.  
- Validate differences with statistical tests (Mann–Whitney, Chi-square).  
- Understand interaction effects between demographics and ad engagement.  

---

## Dataset Description  
**Name:** Online Advertisement Click-Through Rates  
**Published:** 22 April 2024  
**Version:** 1  
**DOI:** 10.17632/wrvjmdtjd9.1  
**Contributors:** Jagadish Tawade, Nitiraj Kulkarni  
**Source:** [Mendeley Data](https://data.mendeley.com/datasets/wrvjmdtjd9/1)  

The dataset includes:  
- **Demographics:** Age, Gender, Income, Location  
- **Ad Features:** Type, Topic, Placement  
- **Behavior Metrics:** Clicks, CTR, Conversion Rate  
- **Contextual Factors:** Day of week, Device type  

This makes it valuable for analyzing user engagement and optimizing ad targeting strategies.  

---

## Methodology  

### Tools Used  
- **SQL** → Data cleaning & preprocessing  
- **Python (Jupyter Notebook)** → Analysis, visualization & modeling  

### Steps  

#### 1. Data Cleaning  
- Removed missing and duplicate values.  
- Fixed inconsistencies in SQL.  
- Encoded categorical variables.  
- Prepared dataset for analysis.  

#### 2. Exploratory Data Analysis (EDA)  
- Visualized demographic and ad feature distributions.  
- Checked correlations between CTR, conversion rate, and other variables.  

#### 3. Unsupervised Clustering  
- Clustered **users** by demographics (age, gender, income, location).  
- Clustered **ads** by type, topic, and placement.  
- Compared CTR and conversion rates across clusters.  

#### 4. Statistical Testing  
- **Shapiro–Wilk Test** → Checked normality of numeric variables.  
- **Mann–Whitney Test** → Compared non-normal numeric variables between two groups.  
- **Chi-Square Test** → Tested associations between categorical features and CTR/conversion.  

---

## Clustering Results  

### 1. User Clustering (K-Prototypes & KMeans)  
- **Cluster 0** → Younger, mid/high-income females, rural/non-rural mix → Balanced CTR.  
- **Cluster 1** → Middle-aged females, low/mid-income, suburban/urban → Moderate CTR.  
- **Cluster 2** → Younger/mid-aged males, mixed income, urban/rural → Mixed CTR (low/high).  
- **Cluster 3** → Rural males, low/mid-income, non-urban → Moderate CTR.  
- **Cluster 4** → Very young, mid-income, urban, mixed gender → **Highest CTR**.  

**Key Insight:** Young, urban, mid-income users show the strongest ad responsiveness.  

---

### 2. Ad Clustering (KMeans on Ad Features)  
- **Cluster 0 (Social Media ads)**  
  - CTR ≈ 0.0502, Conversion ≈ 20.46% (**highest**)  
  - Mix of ad types & topics  
  - **Best-performing cluster**  

- **Cluster 1 (Search Engine + Website ads)**  
  - CTR ≈ 0.0499, Conversion ≈ 20.08%  
  - Balanced ad types/topics but weaker than social media  

**Key Insight:** **Placement** matters more than ad type/topic.  
Social media ads consistently outperform search engine & website ads.  

---

### 3. Cross Insights (User × Ad Clusters)  
- **High CTR & Conversion:**  
  - User Cluster 4 + Ad Cluster 0  
  - Young, urban users respond best to social media ads.  

- **Moderate CTR:**  
  - User Cluster 1 + Ad Cluster 1  
  - Middle-aged/rural users engage more with search engine/website ads.  

**Practical Implication:**  
- Social media → Target young, urban audiences.  
- Search engine/website → Target older, rural/suburban audiences.  

---

## Outlier Detection & Treatment  
- Outliers detected in CTR & Conversion using IQR per demographic/ad group.  
- Example: Adults had 70 conversion rate outliers, Teens had 17.  
- **Treatment:** Winsorization (capping values at IQR bounds).  
- Result: Reduced bias from extreme values while keeping all observations.  

---

## Statistical Tests  

### 1. Mann–Whitney U Test  
- Compares two independent groups on a non-normal numeric variable.  
- **Example:**  
  *“Users exposed to Ad Type A showed significantly higher CTR compared to Ad Type B (U = 1234, p < 0.05).”*  

### 2. Chi-Square Test (Single Feature vs Target)  
- Tests independence between one categorical feature and the outcome.  
- **Example:**  
  *“Ad placement is significantly associated with conversion rate (χ² = 45.2, p < 0.01).”*  

### 3. Chi-Square Test (Multiple Features vs Target)  
- Tests joint association of two features with outcome.  
- **Example:**  
  *“The combination of age group and ad topic significantly affects CTR level (χ² = 62.3, p < 0.05).”*  

---

## Inferences from EDA  

### 1. Univariate Distributions  
- **CTR:** Mostly 0–10%, peak at 4–6%. Right-skewed.  
- **Conversion Rate:** Mostly 0–4%, peak at 1–2%. Rare compared to clicks.  
- **Impressions:** Unevenly distributed; few ads dominate exposure.  

### 2. Bivariate Analysis  
- **CTR vs Conversion:** High CTR ≠ always high conversions.  
- **Correlation Heatmap:** Weak-moderate CTR ↔ Conversion link.  
- **Clicks vs CTR:** CTR rises initially, then stabilizes.  
- **Clicks vs Conversion:** No consistent rise → diminishing returns.  

### 3. Key Takeaways  
- Few ads drive most success; most are modest performers.  
- High CTR does not guarantee conversions → ad quality matters.  
- Conversions are rarer than clicks → optimize for conversions.  
- Clicks beyond a point show diminishing impact.  

---

## Conclusion  
This project studied ad performance using clustering and non-parametric statistical tests.  
Since the data was not normally distributed, Mann–Whitney and Chi-square were applied.  

For clustering, I initially tried **K-means** but switched to **K-prototypes**, which better handled mixed data types.  
This led to clearer user segments and more accurate ad grouping.  

**Overall:**  
- Young, urban, mid-income users respond best to **social media ads**.  
- Middle-aged/rural users engage more via **search engine & website ads**.  
- High CTR ≠ high conversions → targeting and ad quality are critical.  

This project demonstrates how the right methodology (cleaning, clustering, and statistical testing) uncovers actionable insights for ad targeting and optimization.  

---
