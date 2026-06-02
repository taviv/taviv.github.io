---
layout: page
title: Causal Inference — Insulin Treatment and A1C Outcomes in Hospital Patients
description: Investigating the causal link between insulin treatment and A1C values using MIMIC-IV EHR data and T-Learner causal estimation — presented at Vector Institute's Causal AI Bootcamp
img: assets/img/causal_diabetes_slide5.jpg
importance: 5
category: work
related_publications:
---

*Presented at Vector Institute Demo Day — Causal AI Bootcamp, June 9, 2023. Authors: Jonathan Erez, Sudhandar Balakrishnan, Doaa Altarawy, Christina Feng, Ali Mahmood, Tzvi Aviv — Loblaw Health Data Products and Services.*

## Overview

Standard predictive models tell you what will happen — causal models tell you what *causes* it to happen. In diabetes care, the difference matters: knowing that insulin treatment is *associated* with lower A1C is less useful than knowing whether insulin treatment *causes* A1C to decrease, and by how much.

The challenge is confounding. Patient characteristics like age and gender influence both who gets prescribed insulin and what their A1C trajectory looks like — potentially obscuring the true treatment effect. This project applied causal inference methods from Vector Institute's Causal AI Bootcamp to a real-world EHR dataset to disentangle correlation from causation in diabetes management.

## Data

We used [MIMIC-IV](https://physionet.org/content/mimiciv/), a publicly available de-identified electronic health record dataset from a large US academic medical centre (Johnson et al., 2023). From this dataset we extracted:

- Patients who received **at least two A1C tests** during their hospital stay
- The **first two A1C measurements** per patient
- Patients were excluded if their two A1C tests were more than 365 days apart
- We counted the number of insulin medications administered **between** the two A1C tests

This yielded a cohort of **20,229 patients**.

---

## Figure 1 — Patient Characteristics

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/causal_diabetes_slide5.jpg" title="Patient Age and Gender Distribution" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 1. Age and gender distribution of the 20,229-patient cohort. Mean age: 60, median: 61. The cohort skews older — ~40% are 65+ — consistent with the known demographics of hospital-based diabetes populations. Female patients slightly outnumber males in the 65+ group.
</div>

---

## Figure 2 — Insulin Usage by Age and Gender

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/causal_diabetes_slide6.jpg" title="Age/Gender Insulin Distribution" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 2. Percentage of patients using insulin by age group and gender. Total insulin usage: 18.6%. Insulin use rises sharply with age — from ~2% in the 18–34 cohort to 25% in males 65+. Males show consistently higher insulin usage rates than females across all age groups.
</div>

These distributions motivate the need for causal analysis: age and gender are confounders that independently influence both insulin prescription likelihood and A1C trajectory. A naive comparison of A1C changes between insulin and non-insulin patients would be biased by this structure.

---

## Figure 3 — Causal Graph and Methodology

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/causal_diabetes_slide7.jpg" title="Causal Graph: X, T, Y" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 3. Causal graph depicting the study structure. X (covariates: age and gender) influences both T (treatment: number of insulin injections between A1C measurements) and Y (outcome: change in A1C from first to second measurement). The goal is to estimate the causal effect of T on Y, controlling for X.
</div>

### Causal Framework

The study uses the **potential outcomes framework**:

- **X** — covariates: patient age and gender
- **T** — treatment: number of insulin injections administered between the two A1C measurements
- **Y** — outcome: change in A1C value from first to second measurement

The fundamental challenge of causal inference is that **counterfactuals are unobservable** — we cannot observe what a patient's A1C would have been had they received a different treatment. This means the standard PEHE (Precision in Estimation of Heterogeneous Effects) metric cannot be computed directly.

### Implementation

To work around the counterfactual problem, we ran **nuisance models** to obtain a PEHE-like estimation, then applied a **T-Learner estimator with a Random Forest** as the base learner. The T-Learner trains separate outcome models for treated and control units, then estimates individual treatment effects by comparing their predictions.

---

## Figure 4 — Model Results

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/causal_diabetes_slide9.jpg" title="In-sample and Out-of-sample Results" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 4. In-sample and out-of-sample causal estimation results using Random Forest (RF2). Key metrics include value scores, tau estimates across multiple estimators (T, S, match, IPTW, DR), influence scores, and R-scores. The value_dr_clip_prop_score of ~0.04 in-sample and ~0.04 out-of-sample indicates stable doubly-robust estimation.
</div>

The doubly-robust clipped propensity score (`value_dr_clip_prop_score`) — one of the most reliable estimators in the presence of confounding — shows consistent performance in-sample (0.047) and out-of-sample (0.044), suggesting the causal effect estimates are stable and not driven by propensity score extremes.

---

## Conclusions and Impact

This project demonstrated that causal inference methods can be applied to real-world pharmacy and EHR data to move beyond association toward actionable treatment effect estimates. Key takeaways:

- Age and gender are meaningful confounders in insulin prescription patterns that must be accounted for in any analysis of treatment efficacy
- The T-Learner with Random Forest produces stable causal effect estimates on this dataset, with consistent in-sample and out-of-sample performance
- The doubly-robust estimator provides a reliable hedge against model misspecification in either the outcome or propensity model

Beyond the technical results, the project built organizational capability: applying and disseminating causal inference methodology within the data science team, using a concrete and clinically grounded use case.

## Future Directions

- Expand covariates X beyond age and gender to include comorbidities, prior medication history, and lab values
- Causal discovery analysis as a prerequisite to validate the assumed graph structure
- Extend to heterogeneous treatment effect estimation to identify patient subgroups who benefit most from insulin therapy
- Evaluate epsilon and hyperparameter sensitivity for the nuisance models
