# NEXUS - Clinical Trial Orchestrator

<p align="center">
  <img src="https://img.shields.io/badge/FastAPI-0d9488?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite" />
  <img src="https://img.shields.io/badge/Tailwind-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white" alt="Pytest" />
</p>

<p align="center">
  <strong>Deterministic clinical safety orchestration for trial matching and patient protection.</strong>
</p>

NEXUS is a full-stack, distributed clinical platform that merges genomics, therapeutic logic, trial matching, and hematologic safety checks into a single decision engine. It is designed to prevent fatal adverse events in clinical trials by enforcing hard clinical boundaries before enrollment is approved.

---

## The Problem

Traditional clinical trial matching is typically optimized for eligibility and cohort fit, but it often fails in the most dangerous scenarios:

- **Genetic outliers are missed**: A patient may match a trial based on broad diagnostics while carrying a clinically critical mutation that changes treatment suitability.
- **Drug suitability is ignored**: Trial enrollment often does not validate whether a targeted therapy aligns with the patient’s genomic profile.
- **Patient safety is treated as an afterthought**: Blood work is frequently excluded from the matching decision, even when abnormal values indicate imminent clinical risk.
- **Black-box systems are not acceptable in medicine**: Clinical decisions need explainability, not probabilistic guesswork.

In oncology and translational research, a single unsafe enrollment can create catastrophic outcomes. The system must not merely find opportunities; it must also protect the patient.

---

## The Solution (NEXUS)

NEXUS introduces a deterministic clinical safety pipeline, built around a simple concept: if a patient is genomically compatible, therapeutically supported, and clinically unsafe, enrollment must be blocked.

This is the core principle behind the **Death Check** pipeline:

- **Mutation Trail** identifies the relevant mutation, such as EGFR L858R.
- **Drug Logic** finds the targeted therapy, such as Osimertinib, through ChEMBL data.
- **PRISM** finds real, active clinical trials that match the patient profile.
- **HEMA-CORE** evaluates CBC data against strict medical thresholds.
- **The Merge / Orchestrator** reconciles all signals and enforces a final clinical verdict.

If the genetics match a drug and a trial, but the blood work is dangerously abnormal — for example severe leukopenia — the system emits a structured safety decision:

- **ALLOW_CLINICAL_MATCH**
- **REVIEW_REQUIRED**
- **BLOCKED_CLINICAL_RISK**

The outcome is explicit, explainable, and auditable. In clinical environments, this matters more than speed alone: the system must be safe before it is useful.

<img width="1834" height="847" alt="Screenshot 2026-11-02 143135" src="https://github.com/user-attachments/assets/449e2db8-96c8-4645-98ee-301848122de9" />
<img width="1772" height="824" alt="Screenshot 2026-11-02 143043" src="https://github.com/user-attachments/assets/34a49929-e1ed-45a5-b78b-d0912700730b" />
<img width="1779" height="819" alt="Screenshot 2026-11-02 142659" src="https://github.com/user-attachments/assets/e4899e80-ec8b-4156-b5bc-7a1dc9142d6c" />

### Why NEXUS is different

- **Deterministic Logic over Black-Box ML**: Clinical decisions are governed by strict thresholds, not opaque probability curves.
- **Zero-Data-Retention Architecture**: The platform is designed to operate inside a hospital or research network boundary, supporting the “Bring Your Own Data” model without unnecessary external retention.
- **Fail-Safe Design**: If an external API fails or becomes unavailable, the system defaults to a conservative risk state instead of allowing unsafe enrollment.
- **Human-Centered Clinical Governance**: The system flags risk, explains the decision, and supports clinician review without replacing clinical judgment.

---

## System Architecture

NEXUS is a distributed application with a secure frontend, an orchestration backend, and external clinical data integrations.

### 1) Frontend: React + Vite + Tailwind CSS

The frontend is a production-grade web application designed for clinical teams and investigators.

**Capabilities**

- Secure login gate with user authentication flow
- Dark-mode clinical dashboard optimized for extended monitoring sessions
- Patient summary views and clinical risk status
- Real-time flags for safety decisions and trial matching outcomes
- Clean, high-contrast interface designed for operational use

**Deployment**

- Frontend is deployed on **Vercel**
- Built with **React**, **Vite**, and **Tailwind CSS**
- CI/CD pipelines support rapid, reliable frontend delivery

### 2) Backend: Python + FastAPI + Docker

The backend exposes a secure API layer for orchestration, authentication, and data processing.

**Capabilities**

- JWT-based authentication for API security
- FastAPI service layer for high-performance request handling
- Dockerized deployment for reproducible infrastructure
- Clinical orchestration logic for merging domain outputs
- Structured response schemas for explainable risk decisions

**Deployment**

- Backend is deployed on **Render**
- Containerized using **Docker**
- Supports secure, modular service delivery for clinical workloads
- 
- <img width="1888" height="710" alt="Screenshot 2026-11-01 201151" src="https://github.com/user-attachments/assets/95cab0ec-0f2d-40d5-88e3-2a3f5c6c1c74" />
<img width="1819" height="828" alt="Screenshot 2026-11-01 203053" src="https://github.com/user-attachments/assets/9d852f1d-6053-4405-8b77-296f40999b2e" />

### 3) External APIs and Data Sources

NEXUS integrates with authoritative public and domain-specific sources to assess patient fit.

- **Mutation Trail**: CRISPR and genomic mutation evaluation
- **Drug Logic**: ChEMBL API for target therapy matching
- **PRISM**: ClinicalTrials.gov API for active trial identification
- **HEMA-CORE**: CBC analysis against clinical safety thresholds

These services are orchestrated into a single clinical decision pipeline, with safety checks prioritized over eligibility convenience.

---

## The 5-Domain Pipeline

NEXUS is built on five interdependent domains that work together to produce a clinical safety verdict.

### 1. Mutation Trail (CRISPR)

The system evaluates patient genomic signals and identifies clinically relevant mutations such as EGFR L858R. The goal is not just to detect a mutation, but to map it to a treatment-relevant context.

### 2. Drug Logic (ChEMBL API)

Once a mutation is identified, the system queries drug intelligence to match the mutation with known targeted therapies. For example, a mutation may correspond to a known effective therapy such as Osimertinib.

### 3. PRISM (ClinicalTrials.gov API)

The system then checks the patient profile against currently active and relevant clinical trials. This produces a list of trials for which the patient may technically qualify.

### 4. HEMA-CORE (The Death Check)

This is the safety gate. HEMA-CORE analyzes patient CBC values such as:

- WBC
- Platelets
- Hemoglobin
- Other relevant blood markers

These values are compared against clinical boundaries to detect conditions such as severe leukopenia, cytopenia, or dangerous physiological instability.

### 5. The Merge (Orchestrator)

The final phase is the orchestrator: it merges the outputs of all domains into a single safety decision.

**Example clinical logic**

- Mutation matches a drug
- Trial is active and relevant
- Patient is genetically eligible
- But CBC values fall outside safe thresholds
- Result: **BLOCKED_CLINICAL_RISK**

This is the crucial distinction between matching a patient to a trial and protecting that patient from a harmful enrollment decision.

---

## Testing & Validation

NEXUS is not a prototype built on assumptions. It is engineered with a rigorous validation framework designed to stress the clinical edge cases where systems fail.

### Validation Coverage

The project includes **133 passing Pytest cases** covering:

- Boundary value analysis
- Missing or incomplete patient data
- Extreme clinical outliers
- API latency and timeout scenarios
- Degraded service behavior
- Safety-first fallback decisions
- Trial eligibility edge cases
- Hematology threshold violations
<img width="1920" height="682" alt="Screenshot 2026-10-31 232735" src="https://github.com/user-attachments/assets/f4aa906c-f1e3-4bbc-8cc5-840112235e92" />
<img width="1920" height="717" alt="Screenshot 2026-10-31 232752" src="https://github.com/user-attachments/assets/ddca11f1-b32b-489b-bfdf-ea2e311b04e4" />
<img width="1920" height="710" alt="Screenshot 2026-10-31 232800" src="https://github.com/user-attachments/assets/69b6d516-8ede-40a3-b290-d046dc8c3d0b" />
<img width="1903" height="715" alt="Screenshot 2026-10-31 232809" src="https://github.com/user-attachments/assets/b8dd9dec-be4a-4cdc-a659-435fbe51edc3" />
<img width="1920" height="720" alt="Screenshot 2026-10-31 232817" src="https://github.com/user-attachments/assets/594caae7-1563-4b88-8494-4f4352d0dff3" />

### What this means operationally

The system is designed to behave safely when data is incomplete, APIs are slow, or abnormalities cross medical thresholds. In production clinical software, this is far more valuable than simply producing a positive match result.

---

## Deployment

NEXUS is designed for real deployment in a regulated clinical environment, with a production-friendly cloud architecture.

### Frontend Deployment

- **Platform**: Vercel
- **Stack**: React + Vite + Tailwind CSS
- **Purpose**: Secure clinical access, dashboards, and patient status monitoring

### Backend Deployment

- **Platform**: Render
- **Stack**: Python + FastAPI + Docker
- **Purpose**: Authentication, orchestration, domain integration, and clinical decision logic

### CI/CD posture

The platform is intended to support continuous deployment pipelines for both the UI and backend, with operational discipline around:

- Secure environment management
- Dependency integrity
- Build verification
- Safe release validation
- Service-level resilience

---

## About the Architect

### Sourabh Singh

I am a systems architect and product-minded engineer focused on translating complex clinical logic into reliable software systems. My work is rooted in one principle: technology should make medicine safer, more explainable, and more operationally sound.

I build domain-specific engines that combine:

- Software architecture
- Bioinformatics reasoning
- Clinical risk logic
- Production-grade engineering discipline

NEXUS is one example of that approach: a platform designed to enforce safety over convenience, explainability over opacity, and deterministic logic over unreliable black-box automation.

I work at the intersection of systems design and clinical intelligence, building software that is technically rigorous and operationally trustworthy.

---

## Final Statement

NEXUS is not just a trial matching system. It is a clinical safety engine built to prevent dangerous mismatches, detect unsafe patients before enrollment, and convert fragmented biomedical signals into a single, defendable decision.

It is designed for teams that care about one thing above all else:

**getting the clinical decision right before the patient is put at risk.**

---

<p align="center">
  <strong>NEXUS</strong><br>
  Clinical Trial Orchestrator<br>
  Deterministic safety. Proven logic. Protected patients.
</p>
