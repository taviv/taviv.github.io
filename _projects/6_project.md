---
layout: page
title: Farm360Ai — Satellite Imagery and AI for Crop Yield Prediction
description: Founded DaganTech (AgriLogicAI) to predict crop yields and agricultural risks using computer vision and neural networks on satellite imagery, achieving 87–93% accuracy
img: assets/img/agrilogic_slide07.jpg
importance: 6
category: work
related_publications:
---

*DaganTech / AgriLogicAI, 2017–2019. Tzvi Aviv, Founder & CEO.*

## Overview

I founded DaganTech (later rebranded AgriLogicAI) to apply machine learning and satellite imagery to one of agriculture's most persistent problems: uncertainty in crop yields and the financial risks it creates for farmers, insurers, and the entire food supply chain.

The product — **Farm360Ai** — monitored productivity and risks at the individual farm level, using neural network analysis of multi-spectral satellite imagery to generate pre-harvest yield predictions and early risk alerts. The platform was built for the crop insurance industry, which bears the financial exposure when harvests fail.

## The Market Problem

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/agrilogic_slide04.jpg" title="Crop Insurance Industry Structure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 1. US crop insurance industry structure. 16 private insurers manage 1.1 million policies covering 291 million acres, generating $9.9B in premiums and paying $6.8B in claims annually — with ~62% of premiums subsidized by the federal Risk Management Agency.
</div>

The US crop insurance market is large and structurally exposed to yield uncertainty. With $6.8B in annual claims against $9.9B in premiums, loss ratios fluctuate significantly year to year based on weather events, disease, and input decisions — most of which are difficult to predict or price accurately without farm-level data. Existing tools relied on county-level averages and manual field inspections, leaving insurers with poor visibility into individual farm risk.

## The Solution: Computer Vision on Satellite Imagery

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/agrilogic_slide06.jpg" title="Solution Architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 2. Farm360Ai solution: multi-spectral satellite imagery processed through neural networks to generate field-level features (land surface temperature, NDVI), fed into yield prediction models. The platform covered the full customer journey from farm onboarding to automated claim assessment.
</div>

Farm360Ai ingested multi-spectral satellite imagery and extracted time-series features — land surface temperature (day/night), normalized difference vegetation index (NDVI), and derived signals — for each field. Neural networks were trained on historical USDA yield data to predict current-season yields weeks before harvest, and to surface anomalies that indicated elevated loss risk.

The platform addressed five use cases: assessing past productivity, alerting farmers to imminent risks, automating claim processes, improving insurer profitability and financial planning, and improving the customer journey from onboarding to claims settlement.

## Figure 3 — County-Level Yield Analysis (2009–2017)

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/agrilogic_slide07.jpg" title="County Level Analysis" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 3. County-level corn yield predictions vs. USDA actuals (2009–2017). The choropleth map shows model accuracy across US corn belt counties at Week 10 of the growing season, with the majority of counties achieving 85–95% accuracy. The neural network model captured the distribution of yields across counties for 9 consecutive years.
</div>

The county-level model was trained across the US corn belt from 2009 to 2017 using satellite-derived features and USDA county yield reports. The model **achieved 87% accuracy** in predicting county-level yields, validating the satellite imagery approach before scaling to individual farms.

## Figure 4 — Indiana Pilot: Farm-Level Yield Predictions in 3,669 Corn Farms

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/agrilogic_slide08.jpg" title="Indiana Pilot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 4. Indiana pilot study in partnership with a large crop insurance company. Farm-level yield prediction error distributions (AddErr) for 3,669 corn farms across 2008–2017. The tight, near-zero error distributions demonstrate strong prediction accuracy at the individual farm level — achieving 93% accuracy overall.
</div>

The Indiana pilot — conducted in partnership with a large US crop insurance company — scaled the model from county-level aggregates to **3,669 individual corn farms**, achieving **93% accuracy**. The prediction error histograms show tight distributions centered at zero across all 10 years, including the severe drought year of 2012, demonstrating model robustness across different growing conditions.

## Figure 5 — Pilot Project: Predicting Corn Disease (Vomitoxin)

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/agrilogic_slide10.jpg" title="Corn Disease Prediction Pilot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 5. Pilot project to predict vomitoxin (DON) contamination in corn — a mycotoxin that caused $200M in losses in Ontario in 2018 alone. The model predicted DON risk levels by hybrid variety and field location, enabling targeted interventions before harvest.
</div>

Beyond yield quantity, Farm360Ai expanded into predicting crop quality risks. Vomitoxin (deoxynivalenol/DON) contamination — caused by *Fusarium* fungal infection — is invisible until harvest and cannot be remediated after the fact. The pilot demonstrated that satellite-derived field features could differentiate high-risk from low-risk fields and hybrid varieties, enabling pre-harvest interventions and more accurate insurance pricing.

## Milestones and Traction

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/agrilogic_slide13.jpg" title="Milestones and Traction" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 6. DaganTech milestones from 2017 to planned 2021 expansion. Partners and supporters included Syngenta (1st place in the Syngenta AI Challenge), Next Canada, and BioEnterprise.
</div>

Key milestones achieved by the time of this presentation (August 2019):

- **2017** — Award for soybean yield prediction across ~100 farms; validated the core satellite + ML approach
- **2018** — Pre-seed funding; proof-of-concept studies completed
- **2019** — Pilot study scaled to ~5,000 farms across multiple crops and geographies
- **Recognition** — 1st place in the **Syngenta AI Challenge**; supported by Next Canada and BioEnterprise

## Tech Stack

- Multi-spectral satellite imagery (MODIS, Landsat, Sentinel) processed at field level
- Neural network models for time-series feature extraction from satellite bands
- USDA NASS historical yield data for supervised training
- Geospatial analysis for farm boundary delineation and field-level feature aggregation
- Python / scikit-learn / TensorFlow stack; cloud-hosted prediction pipeline
