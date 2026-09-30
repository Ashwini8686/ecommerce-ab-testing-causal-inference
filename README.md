E-Commerce A/B Testing & Causal Inference

## Project Overview

This project analyzes an A/B test conducted for an e-commerce landing page.

The experiment compares an existing landing page (Control) with a newly
designed landing page (Treatment) to determine whether the new design is
associated with an improvement in customer conversion.

The analysis follows a complete data science experimentation workflow:

**Data Understanding → Experiment Audit → Data Cleaning → EDA → A/B Testing
→ Confidence Interval → Relative Lift → Segment Analysis
→ Treatment Effect Heterogeneity → Logistic Regression
→ Business Interpretation**

The project combines descriptive analysis, statistical inference, and
regression-based analysis to evaluate the observed Treatment effect.

## Business Problem

An e-commerce company introduced a new landing page and wants to determine
whether it performs better than the existing landing page.

Users in the experiment were assigned to two groups:

- **Control:** Existing landing page
- **Treatment:** New landing page

The primary outcome is whether a user converted.

The central business question is:

> Does the new landing page produce a statistically significant and practically
> meaningful improvement in customer conversion compared with the existing
> landing page?

The analysis also investigates whether the Treatment effect differs across
different user segments such as gender, location, and device type.

## Business Objective

The objectives of this analysis are to:

1. Compare conversion rates between the Control and Treatment groups.
2. Determine whether the observed difference is statistically significant.
3. Estimate the uncertainty around the Treatment effect using a 95% confidence
   interval.
4. Measure the relative lift produced by the Treatment landing page.
5. Examine conversion differences across gender, location, and device segments.
6. Test whether the Treatment effect varies systematically across these
   segments using interaction terms.
7. Estimate the Treatment effect after adjusting for other observed user
   characteristics using logistic regression.
8. Translate the statistical findings into a business-oriented interpretation.
9. Identify limitations that should be considered before applying the findings
   to production decisions.

## Dataset

The dataset contains **294,478 user records** and **12 variables** describing
experiment assignment, user characteristics, session behavior, and conversion
outcomes.

### Dataset Features

| Feature | Description |
|---|---|
| `user_id` | Unique identifier for each user |
| `timestamp` | Timestamp associated with the user activity |
| `group` | Experiment group: Control or Treatment |
| `landing_page` | Landing page version shown to the user |
| `converted` | Binary conversion outcome |
| `age` | User age |
| `gender` | User gender category |
| `location` | User location |
| `session_duration` | Duration of the user's session |
| `pages_visited` | Number of pages visited during the session |
| `device_type` | Device used by the user |
| `purchase_amount` | Purchase amount associated with the user |

### Experiment Groups

- **Control:** Existing landing page
- **Treatment:** New landing page

The `converted` variable is the primary outcome used to evaluate the
experiment.

The dataset was audited for missing values, duplicate users, group balance,
and consistency between experiment group and landing page before conducting
the statistical analysis.


## Experiment Design

The experiment consists of two groups:

- **Control:** Users exposed to the existing landing page.
- **Treatment:** Users exposed to the new landing page.

The primary outcome is the `converted` variable.

Conversion rate is calculated as:

$$
Conversion\ Rate =
\frac{Number\ of\ Converted\ Users}
{Total\ Users}
$$

The Treatment effect is evaluated by comparing the conversion rate of the
Treatment group with the conversion rate of the Control group.

---

## Methodology

The project follows a structured experimentation workflow:

1. Dataset understanding and experiment audit
2. Data cleaning and validation
3. Univariate exploratory data analysis
4. Bivariate exploratory data analysis
5. Two-proportion A/B hypothesis test
6. 95% confidence interval
7. Relative lift calculation
8. Segment-level analysis
9. Treatment effect heterogeneity using interaction terms
10. Adjusted logistic regression
11. Business interpretation
12. Limitations and considerations

---

## Key Results

| Metric | Result |
|---|---:|
| Control Conversion Rate | **11.87%** |
| Treatment Conversion Rate | **17.95%** |
| Absolute Difference | **+6.08 percentage points** |
| Relative Lift | **+51.18%** |
| Z-statistic | **46.28** |
| 95% CI for Difference | **+5.82 to +6.33 percentage points** |
| Adjusted Odds Ratio | **1.624** |
| 95% CI for Adjusted Odds Ratio | **1.591–1.658** |

The Treatment group had a higher observed conversion rate than the Control
group.

---

## Statistical Analysis

### Hypothesis Test

A two-sided two-proportion z-test was used to compare the conversion rates
between the Treatment and Control groups.

**Null Hypothesis**

$$
H_0: p_T = p_C
$$

**Alternative Hypothesis**

$$
H_A: p_T \ne p_C
$$

The resulting z-statistic was approximately **46.28**, with a p-value far
below the 0.05 significance level.

This provides strong statistical evidence of a difference in conversion rates
between the two experiment groups.

### Confidence Interval

The estimated Treatment-Control conversion-rate difference was:

**+6.08 percentage points**

The 95% confidence interval was:

**+5.82 to +6.33 percentage points**

The interval does not include zero, which is consistent with the hypothesis
test.

### Relative Lift

The observed relative lift was:

**51.18%**

This means that the Treatment conversion rate was approximately 51.18% higher
relative to the Control conversion rate.

Relative lift describes the magnitude of the observed difference and should
not be confused with the absolute percentage-point difference.

## Segment Analysis

The Treatment and Control groups were also compared across key user segments:

- Gender
- Location
- Device type

The segment analysis is primarily descriptive. Differences in segment-level
conversion rates alone do not establish that the Treatment effect is
statistically different across segments.

### Gender

The observed Treatment effect was positive across all analyzed gender
categories:

| Gender | Control Conversion | Treatment Conversion | Treatment Effect |
|---|---:|---:|---:|
| Female | 11.83% | 17.84% | +6.02 pp |
| Male | 11.89% | 18.06% | +6.17 pp |
| Other | 12.66% | 17.89% | +5.23 pp |

### Location

The observed Treatment effect was positive across all locations:

| Location | Control Conversion | Treatment Conversion | Treatment Effect |
|---|---:|---:|---:|
| Australia | 11.87% | 17.98% | +6.11 pp |
| Canada | 12.24% | 17.87% | +5.63 pp |
| Germany | 11.55% | 17.77% | +6.22 pp |
| India | 11.81% | 18.20% | +6.38 pp |
| Pakistan | 11.75% | 18.01% | +6.26 pp |
| UK | 12.05% | 17.79% | +5.74 pp |
| US | 11.85% | 17.92% | +6.07 pp |

### Device Type

The observed Treatment effect was also positive across device categories:

| Device | Control Conversion | Treatment Conversion | Treatment Effect |
|---|---:|---:|---:|
| Desktop | 11.95% | 18.08% | +6.13 pp |
| Mobile | 11.74% | 17.71% | +5.97 pp |
| Tablet | 11.85% | 18.01% | +6.16 pp |

Overall, the descriptive segment analysis shows higher observed Treatment
conversion across the analyzed gender, location, and device categories.

---

## Treatment Effect Heterogeneity

Descriptive segment differences do not establish whether the Treatment effect
actually varies between segments.

To formally investigate this, interaction terms were added to logistic
regression models.

An interaction term allows the effect of the Treatment group to depend on
another variable.

### Gender Interaction

The Treatment × Gender interaction terms did not provide sufficient
statistical evidence that the Treatment effect differs by gender.

### Location Interaction

The Treatment × Location interaction terms did not provide sufficient
statistical evidence that the Treatment effect differs systematically by
location relative to the reference category.

### Device Interaction

The Treatment × Device interaction terms did not provide sufficient
statistical evidence that the Treatment effect differs systematically by
device type relative to the reference category.

### Overall Interpretation

The Treatment group had higher observed conversion across gender, location,
and device segments, but the interaction analyses did not provide sufficient
statistical evidence that the Treatment effect differs systematically across
these segments.

---

## Adjusted Logistic Regression

Because the target variable `converted` is binary, logistic regression was
used to estimate the Treatment effect while adjusting for other observed
user characteristics.

The model includes:

- Experiment group
- Gender
- Location
- Device type
- Age
- Session duration
- Pages visited

The adjusted Treatment odds ratio was:

**1.624**

with a 95% confidence interval of:

**1.591–1.658**

Holding the other variables in the model constant, the estimated odds of
conversion under Treatment were approximately **1.62 times** the estimated
odds under Control.

This corresponds to approximately **62.4% higher estimated odds**, not a
62.4% increase in conversion probability.

The adjusted regression result is consistent with the overall A/B test,
which also showed a substantial difference in conversion between the two
experiment groups.

## Business Interpretation

The Treatment landing page showed a higher observed conversion rate than the
Control landing page.

The observed difference was **+6.08 percentage points**, with a 95%
confidence interval of **+5.82 to +6.33 percentage points**.

The relative lift was **51.18%**, indicating a substantial difference relative
to the Control conversion rate.

The adjusted logistic regression also estimated higher odds of conversion for
Treatment, with an adjusted odds ratio of **1.624** and a 95% confidence
interval of **1.591–1.658**.

If the underlying experiment used valid random assignment and the experimental
assumptions were satisfied, these results provide evidence consistent with a
causal effect of the new landing page on conversion.

Before making a full production rollout decision, the business should also
consider implementation cost, value per conversion, experiment stability over
time, and other operational factors that are not available in this dataset.

---

## Limitations

1. **Randomization cannot be verified**

   The dataset does not provide enough information to independently confirm
   how users were assigned to the Control and Treatment groups.

2. **Potential unobserved variables**

   Factors such as traffic source, previous user behavior, marketing
   campaigns, time of day, and seasonality may influence conversion but are
   not included in the analysis.

3. **Experiment duration**

   The available data does not establish whether the observed Treatment effect
   remains stable over longer periods.

4. **Dataset representativeness**

   The dataset is a prepared dataset and may not perfectly represent a
   production e-commerce experiment.

5. **Revenue impact**

   Conversion improvement does not directly establish profitability. The
   dataset does not provide sufficient information about implementation costs,
   customer lifetime value, or profit per conversion.

6. **Causal interpretation**

   Strong causal interpretation depends on valid experimental design and
   assumptions that cannot be completely verified from the available dataset.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- Statsmodels
- Jupyter Notebook
- Git & GitHub

---

## Project Structure

```text
ecommerce-ab-testing-causal-inference/
│
├── ab_testing_causal_inference.ipynb
├── requirements.txt
├── .gitignore
├── README.md
└── AB Testing Data.csv


Then add this at the very end:

```markdown
---

## Dataset

The dataset used in this project was obtained from Kaggle.

The raw dataset is not included in this repository because its redistribution
terms should be verified before publishing the file publicly.

To reproduce the analysis, download the dataset and place it in the project
directory with the filename:

`AB Testing Data.csv`