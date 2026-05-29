---
layout: page
title: AI/ML Platform for Canada's Largest Pharmacy Network
description: Product design and delivery of a patient-centric health data and AI platform at Loblaw Companies
img: assets/img/project_pharmacy.svg
importance: 1
category: work
related_publications:
---

## The Problem

Canada's pharmacy landscape changed dramatically when provincial regulations expanded pharmacists' scope of practice to include vaccinations, medication reviews, and treatment of minor ailments. This was a significant clinical and commercial opportunity — but the underlying IT infrastructure wasn't built for it.

Loblaw's 1,300+ pharmacy stores each operated decentralized, transactional dispensing systems. There was no unified patient view, no way to measure health outcomes across the network, and no platform to power AI-enabled services at scale. The key questions were:

- How do you unify data from thousands of independent pharmacy systems into a coherent, patient-centric view?
- How do you build an AI/ML platform that enables data scientists to ship clinical features quickly, safely, and repeatably?
- How do you do this under PIPEDA, pharmacy regulatory requirements, and enterprise data governance — without making it impossible to move fast?

## Platform Architecture

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/project_pharmacy.svg" title="Health Data Platform Architecture" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Platform architecture: data from 1,300+ pharmacy stores, clinical devices, provider registries, and surveys unified in BigQuery, powering NLP, ML, and targeting features.
</div>

## What I Built and Owned

As Director, Health Data Products & Services, I was accountable for the product strategy, architecture decisions, team delivery, and outcomes. I led a 10-person cross-functional team (ML engineers, data scientists, product owners, clinical analysts) and owned the roadmap from discovery through production.

The platform's foundation was a unified data architecture built on Google BigQuery, consolidating data from pharmacy transaction systems, public health sources, clinical device vendors, and patient survey platforms into a small set of clean, governed, reusable tables — including a patient identity resolution layer that linked records across stores without a common identifier.

<div class="row justify-content-center mt-3 mb-2">
    <div class="col-12">
        {% include figure.html path="assets/img/pharmacy_erd.png" title="Entity-Relationship Diagram" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Entity-Relationship Diagram of the unified pharmacy health data platform. Core tables cover ~60M patient profiles, ~2,000 stores, and billions of prescription transactions, augmented with clinical device data, provider registries, and population health surveys.
</div>

## AI Features Delivered on the Platform

The data platform was the foundation — the point was what it enabled. Features shipped on it included:

- **NLP-based clinical trial matching** — identifying eligible patients from pharmacy records for recruitment
- **Medication adherence prediction** — ML models surfacing patients at risk of non-adherence for pharmacist intervention
- **Vaccination targeting** — identifying patients eligible for vaccination by age, chronic condition, and history; queries that previously took hours now ran in minutes and were automated in the visualization platform

Each feature followed a consistent product discipline: discovery with pharmacy operations and clinical partners, explicit success criteria before build, evaluation protocols with defined performance thresholds, and post-launch monitoring.

## Outcomes

The platform underpinned the national rollout of new pharmacy programs — Minor Ailments, Diabetes Screening, and Medication Reviews — with documented patient and commercial impact. It replaced thousands of columns of unstructured transactional data with a governed, scalable architecture that cut analytic cycle times dramatically and made previously impossible analyses (like linking lab values to prescription records without a unified patient ID) feasible for the first time.

## Governance and Privacy

Sensitive fields are encrypted at rest; data access is governed through Google IAM policies and service accounts. The architecture was designed to meet PIPEDA requirements and enterprise data governance standards — privacy and security as product requirements, not afterthoughts.

One acknowledged limitation: the platform does not adhere to HL7 FHIR interoperability standards. Adopting standard clinical data formats at source systems remains an important future investment for the network.
