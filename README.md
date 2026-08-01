# A/B Testing — New Page vs Old Page Conversion Analysis

Statistically testing whether a newly designed landing page generates significantly higher conversion rates than the existing page — using Chi-Square hypothesis testing on 290,000+ user records.

---

## Brief Summary

An A/B testing project on 2,94,478 user records — involving data cleaning, misassignment correction, duplicate removal, conversion rate comparison, and Chi-Square statistical testing — to answer: "Does the new landing page significantly improve conversion rates over the old page?"

---

## Overview

This project implements a complete A/B testing pipeline on a real-world e-commerce dataset. Users were split into two groups — control (shown old page) and treatment (shown new page) — and conversion rates were compared between the two groups. A Chi-Square test was used to determine whether the observed difference is statistically significant or just due to random chance.

---

## Problem Statement

A company built a new landing page hoping it would increase user conversions. Before rolling it out to all users, they ran an A/B test — splitting users into a control group (old page) and a treatment group (new page). The goal is to determine:

"Is there a statistically significant difference in conversion rates between the new page and the old page?"

Hypothesis:

H0 (Null)	There is no difference in conversion rate between the new page and the old page → p_treatment = p_control
H1 (Alternative)	There is a difference in conversion rate between the new page and the old page → p_treatment ≠ p_control

Significance Level (α)	0.05
Decision Rule	p-value < α → Reject H0 · p-value ≥ α → Fail to Reject H0

---

Columns:

|Column | Type |	Description |	
|-------|------|--------------|
|user_id |	int64 |	Unique identifier for each user |
|timestamp |	datetime | Date and time the user visited the page |	
|group | string |	Experiment arm the user was assigned to |
|landing_page |	string | Page version the user actually saw |	
|converted	| int64 |	Whether the user converted |

---

## Tools & Technologies

| Tool |	Purpose |
|------|----------|
|Python (Jupyter Notebook) |	Data cleaning, analysis & statistical testing |
|Pandas / NumPy |	Data manipulation & conversion rate calculation |
|Matplotlib / Seaborn |	Visualizations (bar charts, countplots) |
|SciPy (chi2_contingency)	| Chi-Square statistical significance test |

---

## Methods

1. Inspection	Checked shape (2,94,478 × 5), data types, value counts for group and landing_page.
2. Data Type Correction	Converted timestamp column from string to proper datetime format.
3. Misassignment Fix	Identified users where group and page didn't match (e.g., control shown new_page or treatment shown old_page) — removed all mismatched rows using a match mask.
4. Duplicate Removal	Found duplicate user_id entries — kept first occurrence per user, dropped rest.
5. Conversion Rate Calculation	Computed conversion rate (%) separately for control and treatment groups.
6. Chi-Square Test	Built a contingency table (group × converted) and ran chi2_contingency() from SciPy to test statistical significance.
7. Decision	Compared p-value against α = 0.05 to accept or reject H0.

---

## Key Insights

Observed Counts (after cleaning):

| Group |	Not Converted (0) |	Converted (1) |
|-------|-------------------|---------------|
|Control |	1,27,785 |	17,489 |
|Treatment |	1,28,046 |	17,264 |

---

## Conversion Rates:

| Group |	Conversion Rate |
|-------|-----------------|
| Control (Old Page) |	~12.04% |
| Treatment (New Page) |	~11.88% |

---

## Statistical Test Results:

| Metric |	Value |
|--------|--------|
| Chi-Square Statistic |	1.7036 |
| P-Value |	0.1918 |
| Significance Level (α) | 	0.05 |
| Decision	 | Fail to Reject H0 |
| Conclusion	| No significant difference between old page and new page conversion |

---

## Key Takeaways:

 1	The p-value (0.1918) is greater than α (0.05) — the difference in conversion rates is NOT statistically significant.
 2	The new page conversion rate (~11.88%) is slightly lower than the old page (~12.04%) — the new page did not improve conversions.
 3	Data quality issues found — misassigned users (wrong group/page combinations) and duplicate user IDs were cleaned before testing.
 4	After cleaning, 2,86,690 valid unique users remained for the final test.
 5	The Chi-Square test is the correct test here — it evaluates independence between two categorical variables (group × converted).
 
---

## Results & Conclusion

The Chi-Square test returns a p-value of 0.1918, which is well above the significance threshold of 0.05. This means we fail to reject the Null Hypothesis — there is no statistically significant difference in conversion rates between the new page (11.88%) and the old page (12.04%). The company should not roll out the new page based on this data, as it does not demonstrably improve user conversions. Further testing with a larger sample size or a longer test duration may be warranted before making a final decision.

---

## Author & Contact

| Field |	Info |
|-------|------|
|Name	| KRISHNA |
|LinkedIn |	https://www.linkedin.com/in/krishna-krishna-26a106231/ |
|GitHub	| https://github.com/ |

⭐ If you found this project helpful, consider giving it a star!
