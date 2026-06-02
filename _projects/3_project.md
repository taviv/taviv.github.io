---
layout: page
title: Cardiometabolic Treatment Trends in Pharmacy Records and Digital Surveys
description: Precision public health using pharmacy prescription records and digital surveys to map cardiometabolic treatment rates across Canada
img: assets/img/cardiometabolic_poster_p1.png
importance: 7
category: work
related_publications:
---

*Presented at a national health conference. Authors: John Chau, Jeremy Kardash, Ali Mahmood, Jonathan Erez, Tzvi Aviv — Loblaw Healthcare Data Products and Services.*

## Overview

Precision public health combines big data and digital methodologies with traditional epidemiology to forecast health risks and improve the quality of services provided to patients. This study used anonymized pharmacy prescription records from Loblaw's network across Canada — processed in compliance with applicable privacy laws and Loblaw's policies — alongside self-reported digital surveys to characterize cardiometabolic treatment trends at scale.

Cardiometabolic conditions (diabetes, hypertension, hyperlipidemia) represent a large and growing portion of chronic disease burden in Canada. This work establishes treatment prevalence baselines, surfaces geographic variation down to the Forward Sortation Area (FSA) level, and benchmarks pharmacy-derived estimates against Statistics Canada's Canadian Community Health Survey (CCHS).

## Methods

Prescription records were extracted from pharmacies across Canada. Patients were divided into twelve age-sex groups and assigned to FSAs by home address. **Treatment rates** were calculated as:

> (# patients taking cardiometabolic medication) ÷ (total prescription recipients per year) per age-sex group per FSA

Self-reporting digital surveys were fielded in September 2022 and compared to the CCHS ([Statistics Canada, Table 13-10-0096-01](https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=1310009601)).

---

## Figure 1 — Age-Group Treatment Prevalence by Province (2021)

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/cardiometabolic_fig1_4.jpeg" title="Age-Group Treatment Prevalence Rates by Province" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 1. Pharmacy treatment rates for diabetes, hypertension, and dyslipidemia by age group and province (2021). Rates increase sharply with age across all provinces. British Columbia shows consistently lower cardiometabolic treatment rates; Alberta shows notably lower dyslipidemia treatment rates.
</div>

Treatment rates rise steeply with age and are consistently higher in males than females across all three conditions and all provinces. The provincial variation — particularly the lower rates in BC and Alberta — likely reflects a mix of population demographics, prescribing practices, and underlying disease prevalence differences.

---

## Figure 2 — Diabetes Treatment Rates per FSA, Ontario (2017–2021)

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/cardiometabolic_fig1_3.png" title="Diabetes Treatment Rates per FSA, Ontario 2017-2021" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 2. Histograms of pharmacy-derived diabetes treatment rates among seniors per FSA in Ontario (2017–2021), compared to CCHS provincial estimates (dashed lines). Male rates exceed female rates. The wide spread of FSA-level distributions relative to the CCHS provincial benchmarks highlights significant intra-provincial geographic variation.
</div>

The FSA-level histograms reveal **large variance in diabetes treatment rates** across Ontario neighbourhoods — far more than aggregate provincial numbers suggest. Male pharmacy-derived rates track above CCHS benchmarks in most years; female rates track closer to or below. This gap may reflect differential medication uptake, access, or undiagnosed disease.

---

## Figure 3 — Hypertension Trends from Self-Reported Digital Surveys (September 2022)

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/cardiometabolic_fig1_2.png" title="Hypertension Trends from Digital Surveys" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 3. Self-reported digital survey results by age-sex group. Left: blood pressure measurement rates (measured, forgot values, not measured). Centre: distribution of reported BP readings by category. Right: location of most recent BP measurement (Doctor/Walk-In, Home, Pharmacy/Grocery, Hospital).
</div>

Key findings from the survey:

- **Blood pressure monitoring rates** range from ~60% in 18–34 year-olds to ~80% in adults 65+, with the remainder either not measured or unable to recall values
- **~10% of respondents report uncontrolled blood pressure** (above 140/90 mmHg) — a clinically significant share with direct implications for pharmacist intervention programs
- **20–40% report taking blood pressure readings at home**, varying by age-sex group — reflecting the growing role of consumer health devices
- Doctor/Walk-In clinics are the dominant measurement setting, but pharmacy and home measurement are meaningful shares, especially in older cohorts

---

## Conclusions

- Growing trends in cardiometabolic treatment prevalences observed across Canada
- Treatment rates increase with age and are higher in males across all conditions
- Lower treatment rates in British Columbia and Alberta warrant further investigation
- Large FSA-level variance in diabetes treatment rates points to meaningful geographic health inequities
- A substantial minority of patients have uncontrolled blood pressure or are not being monitored — a direct opportunity for pharmacist-led care programs

## Future Directions

This work supports the broader goal of improving accuracy of pharmacy-based health data models to enable better-targeted services. Next steps include:

- Improving FSA-level models with demographic covariates to disentangle true health variation from access and prescribing differences
- Linking digital survey data to pharmacy records for longitudinal validation
- Extending the hypertension survey framework to diabetes and dyslipidemia self-management behaviours
