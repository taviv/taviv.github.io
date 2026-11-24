---
layout: page
title: Clinical Trials Intelligence — ClinicalTrials.gov Pipeline with ICD-10 Coding on AWS
description: A serverless weekly pipeline that turns ~224k ClinicalTrials.gov studies into an ICD-10-CM-coded analytics layer and dashboards, with an evidence-checked LLM coding tier on Amazon Bedrock
img: assets/img/project_ctgov.svg
importance: 3
category: work
related_publications:
---

## The Problem

ClinicalTrials.gov is the largest public registry of clinical research, but it is hard to analyze at scale. Conditions are entered as free text or MeSH terms, and **there are no ICD-10 codes**, so trial activity can't be lined up with the coding system that hospitals, payers and pharmacy data use. Answering simple portfolio questions (*How many Phase 1 oncology trials started each year? How long do Phase 3 cardiovascular trials actually take?*) means reprocessing a large, constantly changing dataset.

I built this pipeline to answer three questions:

- How do you keep a fresh, analysis-ready copy of the registry without running a database around the clock?
- How do you assign ICD-10-CM codes to trial conditions reliably, and know where the codes came from?
- Where can an LLM add coverage safely, without making up codes or overwriting exact ones?

## Architecture

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/project_ctgov.svg" title="ClinicalTrials.gov Pipeline Architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Pipeline architecture: EventBridge triggers a weekly Step Functions run. Lambda functions running DuckDB fetch changed studies, convert them to Parquet, assign ICD-10-CM codes and publish an immutable snapshot on S3. CloudFront dashboards and Athena read from that snapshot.
</div>

The design is fully serverless: **no database, no VPC, nothing running between runs.** Each Monday, EventBridge starts a Step Functions workflow:

1. **Fetch:** pulls only studies updated since the last successful run from the ClinicalTrials.gov v2 API, requesting only the fields it needs
2. **Transform:** ten parallel Lambdas convert each page into per-table Parquet files using DuckDB
3. **Build:** merges changed studies into the current data, adds condition codes, writes a new **immutable snapshot**, and moves a `CURRENT.json` pointer to it

A failed run leaves the previous snapshot in place, and rolling back just means pointing `CURRENT.json` at an older snapshot. By default the pipeline covers every phased study (Early Phase 1 through Phase 4, about 224k). A single parameter narrows it to, for example, about 35k Phase 1 studies since 2016.

The data model is a set of tables keyed by `nct_id` (studies, protocol text, phases, conditions, interventions, outcomes, locations, sponsors, MeSH terms and condition codes), registered in Glue so it can be queried ad hoc with Athena.

## ICD-10-CM Condition Coding

The core of the project is a layered coding engine. Every code records **how** it was assigned (`via`), so you can tell an exact mapping from an inferred one:

| Tier | `via` | How the code is assigned |
|---|---|---|
| 1 | `mesh` | The condition's MeSH term maps to ICD-10-CM through a crosswalk: curated overrides, then MONDO, UMLS, Wikidata and SNOMED CT |
| 2 | `text` | A curated rule matches the free-text condition, or UMLS maps it to a single ICD-10-CM concept |
| 3 | `intervention` | `Z23` for vaccine trials that enroll healthy volunteers |
| 4 | `llm` | An LLM picks a category for studies that have no exact code, with a quoted piece of evidence |
| 5 | `mesh_ancestor` | A broader code from a parent MeSH term, used only when nothing else applies |

Every code is checked against the official CMS ICD-10-CM release.

### An LLM tier with guardrails

For studies that don't get an exact code, the protocol text (titles, conditions, interventions, summary and description excerpts, and inclusion criteria with the exclusions removed) is sent to **Claude Haiku 4.5 on Amazon Bedrock** along with the ICD-10-CM category list. The model can choose up to 12 categories, but **it has to quote the protocol text that supports each one.** Answers are thrown out if the quote can't be found in the protocol, or if it appears only in the exclusion criteria, since a condition that excludes patients isn't the condition being studied. LLM codes **never replace exact codes**. They only fill gaps. Results are cached per study, so each weekly run sends only new or changed studies to the model.

Accuracy is measured, not assumed. A separate evaluation workflow measures precision and recall for each ICD-10 chapter against hand-labelled studies, using study-clustered bootstrap confidence intervals and preset go/fix thresholds. The LLM tier also has a scorecard on 300 Phase 3 and Phase 2/3 studies.

## Dashboards

Three static Chart.js dashboards are served through CloudFront:

- **Overview:** study status, starts by year, top conditions and countries, ICD-10-CM chapters and categories, sponsors, interventions, enrollment and recent studies
- **Study Duration:** start-to-completion times, filterable by phase, year, country and healthy-volunteer status, backed by a DuckDB query API (`/api/query`) behind CloudFront
- **LLM Coding:** how much the LLM tier adds to exact-code coverage, the top added categories, example studies with their quoted evidence, and the evaluation scorecard

*A link to the live dashboards can be shared upon request.*

## Engineering Discipline

- **Verification:** `make verify` checks run status, freshness, row counts, uniqueness, filter correctness, orphan rows, coding coverage, whether the dashboards match the API, and a spot check of 20 random studies against the live registry
- **Infrastructure as code:** AWS SAM / CloudFormation, deployed with a single `make deploy`
- **CI:** GitHub Actions runs linting (ruff, cfn-lint), pytest and SAM validation on every pull request
- **Local-first:** the whole pipeline runs locally without AWS (`make local`, `make serve`)
- **Licensing hygiene:** licensed vocabularies (UMLS, SNOMED CT) stay in a private bucket. Only open-licensed or public-domain material is published.

## Stack

- **Orchestration:** Amazon EventBridge, AWS Step Functions
- **Compute:** AWS Lambda (Python 3.13) with DuckDB
- **Storage and query:** Amazon S3 (Parquet), AWS Glue, Amazon Athena
- **Serving:** Amazon CloudFront, Lambda Function URL (IAM-authenticated), Chart.js
- **AI:** Amazon Bedrock (Claude Haiku 4.5)
- **Vocabularies:** CMS ICD-10-CM, MeSH, MONDO, UMLS, Wikidata, SNOMED CT

## Code

[View the repository on GitHub](https://github.com/taviv/ct_aws_db)

## Why It Matters

Putting trial registry data into ICD-10-CM opens it up to the same analysis as claims, EHR and pharmacy data. That makes it possible to compare research activity with disease burden, size the pool of eligible patients for a trial, or track a therapeutic area's pipeline over time. The architecture also shows a pattern I use for clinical AI work in general: deterministic methods first, the LLM only where they fall short, every LLM answer backed by evidence that can be checked, and accuracy measured against human labels.
