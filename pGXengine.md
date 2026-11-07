

PGx Engine - Precision Dosing API

https://img.shields.io/badge/FASTAPI-005571?style=flat-square&logo=fastapi&logoColor=white https://img.shields.io/badge/REACT-20232A?style=flat-square&logo=react&logoColor=61DAFB https://img.shields.io/badge/VITE-646CFF?style=flat-square&logo=vite&logoColor=white https://img.shields.io/badge/TAILWIND-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white https://img.shields.io/badge/DOCKER-2496ED?style=flat-square&logo=docker&logoColor=white https://img.shields.io/badge/PYTEST-0A9EDC?style=flat-square&logo=pytest&logoColor=white

Deterministic pharmacogenomic orchestration for precision dosing and patient protection.

The PGx Engine is a full-stack, distributed clinical platform that merges genetic mutation scanning, pharmacokinetic math, and dynamic dose adjustment into a single decision engine. It is designed to prevent fatal adverse events in standard dosing protocols by enforcing hard clinical boundaries before a drug is prescribed.

The Problem

Standard drug dosing is typically optimized for population averages, but it often fails in the most dangerous scenarios:

· Genetic outliers are missed: A patient may receive a standard dose while carrying a clinically critical mutation (e.g., CYP2C9 3/3) that drastically alters drug metabolism.
· Drug accumulation is ignored: Without adjusting for a "Poor Metabolizer" phenotype, standard doses lead to toxic accumulation.
· Patient safety is treated as an afterthought: Blood work and genetic data are frequently excluded from the dosing decision, even when abnormal phenotypes indicate imminent clinical risk.
· Black-box systems are not acceptable in medicine: Clinical dosing decisions need explainability and deterministic math, not probabilistic guesswork.

In pharmacology and translational research, a single unsafe prescription can create catastrophic outcomes. The system must not merely calculate a dose; it must protect the patient.

The Solution (PGx Engine)

The PGx Engine introduces a deterministic clinical dosing pipeline, built around a simple concept: if a patient is genetically compromised, the standard dose must be mathematically overridden to ensure safety.

This is the core principle behind the PGx pipeline:

· The Traffic Jam (Genetics): The API scans for the CYP2C9 mutation. If the patient is a "Poor Metabolizer," the enzyme highway is jammed.
· The Delivery Truck (PK Math): Because the highway is jammed, the drug (the delivery truck) stays in the body longer. The engine mathematically extends the drug's half-life (e.g., from 40 hours to 200 hours).
· The Merge / Orchestrator: The engine reconciles the genetic phenotype and dynamically drops the maintenance dose to a safe level (e.g., from 4.07mg to 0.81mg).

If the genetics indicate a Poor Metabolizer, the system emits a structured safety decision:

· SAFE_METABOLISM
· TOXICITY_RISK
· CLEARED_WITH_CUSTOM_DOSE

The outcome is explicit, explainable, and auditable. In clinical environments, this matters more than speed alone: the system must be safe before it is useful.

<img width="1920" height="878" alt="Screenshot 2026-11-06 164654" src="https://github.com/user-attachments/assets/2b9a5337-b44b-4814-a814-de23856e75ec" />
<img width="1917" height="887" alt="Screenshot 2026-11-06 164611" src="https://github.com/user-attachments/assets/59adff68-6d22-40ef-ad4f-2556291b2066" />
<img width="1920" height="889" alt="Screenshot 2026-11-06 164547" src="https://github.com/user-attachments/assets/3fd79e3a-4814-4c89-b70f-98c1d3936b27" />

Why PGx Engine is different

· Deterministic Logic over Black-Box ML: Clinical decisions are governed by strict pharmacokinetic formulas and genetic multipliers, not opaque probability curves.
· Zero-Data-Retention Architecture: The platform is designed to operate inside a hospital or research network boundary, supporting the "Bring Your Own Data" model without unnecessary external retention.
· Fail-Safe Design: If an external API fails or data is incomplete, the system defaults to a conservative risk state instead of allowing unsafe dosing.
· Human-Centered Clinical Governance: The system flags risk, explains the math, and supports clinician review without replacing clinical judgment.

System Architecture

The PGx Engine is a distributed application with a secure frontend, an orchestration backend, and a relational database for audit trails.

1) Frontend: React + Vite + Tailwind CSS

The frontend is a production-grade web application designed for clinical teams and investigators.

Capabilities

· Secure login gate with user authentication flow
· Dark-mode clinical dashboard optimized for extended monitoring sessions
· Patient summary views and clinical risk status
· Real-time flags for toxicity warnings and adjusted dosing outcomes
· Clean, high-contrast interface designed for operational use

Deployment

· Frontend is deployed on Vercel
· Built with React, Vite, and Tailwind CSS
· CI/CD pipelines support rapid, reliable frontend delivery

2) Backend: Python + FastAPI + Docker

The backend exposes a secure API layer for orchestration, authentication, and data processing.

Capabilities

· JWT-based authentication for API security
· FastAPI service layer for high-performance request handling
· Dockerized deployment for reproducible infrastructure
· Clinical orchestration logic for merging genetic data and PK math
· Structured response schemas for explainable risk decisions

Deployment

· Backend is deployed on Render
· Containerized using Docker
· Supports secure, modular service delivery for clinical workloads
<img width="1920" height="662" alt="Screenshot 2026-11-06 093335" src="https://github.com/user-attachments/assets/4d000052-c3a5-4e9d-8ab5-157330642f39" />
<img width="1920" height="856" alt="Screenshot 2026-11-06 093322" src="https://github.com/user-attachments/assets/dbdfb71d-581d-4cd7-9100-5140429239c9" />

3) The Audit Trail & Data Persistence

Clinical software must be auditable. The PGx Engine does not just calculate in the browser; it writes every decision to a MySQL database via SQLAlchemy.

This ensures a physician can track the exact mathematical logic used to adjust a patient's dose, creating a defensive legal and clinical shield. The audit log captures:

· patient_id
· gene & mutation (e.g., CYP2C9, 3/3)
· phenotype (Poor Metabolizer)
· base_half_life vs adjusted_half_life
· standard_dose vs personalized_dose
· timestamp

The 5-Step Pipeline

The PGx Engine is built on five interdependent steps that work together to produce a clinical dosing verdict.

1. Input Validation (Pydantic)

The API ingests JSON patient data (genetics, weight, target concentration) and validates it using Pydantic to ensure no malformed data enters the engine.

2. Mutation Analysis (CYP2C9)

The system evaluates the patient's genomic signals and identifies clinically relevant mutations such as CYP2C9 3/3. The goal is to map the mutation to a specific metabolizer phenotype.

3. Phenotype Classification (The Traffic Jam)

Once a mutation is identified, the system classifies the patient's metabolic rate:

· Normal Metabolizer (1/1)
· Intermediate Metabolizer (1/3)
· Poor Metabolizer (3/3)

4. Pharmacokinetic Math (The Delivery Truck)

The engine uses the patient's weight, target concentration, and base half-life to calculate the standard dose. If the patient is a Poor Metabolizer, the engine applies genetic multipliers to extend the half-life and drastically reduce the dose.

5. The Merge (Orchestrator)

The final phase is the orchestrator: it merges the outputs of all domains into a single safety decision.

Example clinical logic:

· Patient has CYP2C9 3/3 mutation
· Patient is a Poor Metabolizer
· Base half-life (40h) is extended to 200h
· Standard dose (4.07mg) is dropped to 0.81mg
· Result: CLEARED_WITH_CUSTOM_DOSE (or TOXICITY_RISK if the dose is not adjusted)

This is the crucial distinction between guessing a dose and protecting a patient from fatal toxicity.

Testing & Validation

The PGx Engine is not a prototype built on assumptions. It is engineered with a rigorous validation framework designed to stress the clinical edge cases where systems fail.

Validation Coverage
The project includes 45 passing Pytest cases covering:

· Normal Metabolizer boundaries
· Intermediate Metabolizer boundaries
· Poor Metabolizer boundaries
· Extreme weight boundaries
· Zero-division crash prevention (Half-life = 0)
· Missing or incomplete patient data
· API latency and timeout scenarios

<img width="1920" height="649" alt="Screenshot 2026-10-30 194856" src="https://github.com/user-attachments/assets/3444ffff-6b9d-4d00-8695-7d30a826213e" />
<img width="1920" height="669" alt="Screenshot 2026-10-30 194907" src="https://github.com/user-attachments/assets/bb090b13-0b45-4622-b381-e16111c97e49" />

What this means operationally

The system is designed to behave safely when data is incomplete, APIs are slow, or abnormalities cross medical thresholds. In production clinical software, this is far more valuable than simply producing a positive match result.

Deployment

The PGx Engine is designed for real deployment in a regulated clinical environment, with a production-friendly cloud architecture.

Frontend Deployment
Platform: Vercel
Stack: React + Vite + Tailwind CSS
Purpose: Secure clinical access, dashboards, and patient status monitoring

Backend Deployment
Platform: Render
Stack: Python + FastAPI + Docker
Purpose: Authentication, orchestration, domain integration, and clinical decision logic

About the Architect

Sourabh Singh
I am a systems architect and product-minded engineer focused on translating complex clinical logic into reliable software systems. My work is rooted in one principle: technology should make medicine safer, more explainable, and more operationally sound.

I build domain-specific engines that combine:

· Software architecture
· Bioinformatics reasoning
· Clinical risk logic
· Production-grade engineering discipline

PGx is one example of that approach: a platform designed to enforce safety over convenience, explainability over opacity, and deterministic logic over unreliable black-box automation.

I work at the intersection of systems design and clinical intelligence, building software that is technically rigorous and operationally trustworthy.

Final Statement

PGx is not just a dosing calculator. It is a clinical safety engine built to prevent dangerous prescriptions, detect unsafe patients before toxicity occurs, and convert fragmented biomedical signals into a single, defendable decision.

It is designed for teams that care about one thing above all else:
getting the clinical decision right before the patient is put at risk.

PGx Engine
Precision Dosing API
Deterministic safety. Proven logic. Protected patients.


The engine is deployed. The README is done. The PDF is ready.

Now, I want you to go eat your meal. You have a weekend to rest before you drop this bomb. 🫂🍲
