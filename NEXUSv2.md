# **NEXUS - Clinical Trial Orchestrator**
<p align="center">
  <img src="https://img.shields.io/badge/FastAPI-0d9488?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite" />
  <img src="https://img.shields.io/badge/Tailwind-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white" alt="Pytest" />
</p>

<p align="center">


Deterministic clinical safety orchestration for trial matching and patient protection.

NEXUS is a full-stack clinical platform that merges genomics, therapeutic logic, trial matching, and hematologic safety checks into a single decision engine. It prevents fatal adverse events in clinic[...]

## **The Problem**

Traditional clinical trial matching optimizes for cohort fit but fails dangerously:

· Genetic outliers are missed: Patients look average but hide mutations (EGFR, KRAS) needed for trials.
· Safety is an afterthought: Blood work is excluded. A patient might match genetically but be clinically unsafe due to severe anemia or leukopenia.
· Black-box systems are not acceptable.

## **The Solution (The "Death Check" Guardrails)**

NEXUS is a 5-Domain pipeline that uses CRISPR mutation tracking to find hidden outliers and HEMA-CORE to run safety checks.

· Sex-Specific Ranges: The engine dynamically adjusts thresholds. A Hemoglobin of 12.5 clears a female patient but triggers a fatal anemia block for a male (Normal Male: 13.5 - 17.5).
· Dynamic Trial Overrides: Global ranges are overridden by trial criteria. If a trial allows Platelets > 100, the engine clears a patient with 120 Platelets, even though the global range is 150-450.
· Drug Safety Warnings: Recommending Osimertinib automatically appends a warning for Interstitial Lung Disease (ILD) and QTc prolongation.

## **System Architecture**

· Frontend (React + Tailwind): Real-time visual analysis of patient blood data vs. normal ranges.

<img width="1895" height="904" alt="Screenshot 2026-11-09 212443" src="https://github.com/user-attachments/assets/8c8deeaa-fc6a-4bef-8d6c-4b14abcb8441" />
<img width="1920" height="907" alt="Screenshot 2026-11-09 211409" src="https://github.com/user-attachments/assets/1c8457a7-b4fe-41a0-8d09-a54581024bf2" />
<img width="1920" height="884" alt="Screenshot 2026-11-09 211310" src="https://github.com/user-attachments/assets/31904d1b-d5e1-446c-b6ed-7447b44a5ff3" />
<img width="1920" height="906" alt="Screenshot 2026-11-09 211651" src="https://github.com/user-attachments/assets/ca6888da-b4b5-426b-a072-77a3439c9caa" />
<img width="1920" height="900" alt="Screenshot 2026-11-09 210116" src="https://github.com/user-attachments/assets/5168c96d-9495-4d7d-87c7-889265dd4536" />

· Backend (FastAPI + Python): PRISM Engine (Outlier detection), HEMA-CORE (CBC Analysis), ChEMBL/NCBI APIs, ClinicalTrials.gov API.

<img width="1885" height="647" alt="Screenshot 2026-11-10 030959" src="https://github.com/user-attachments/assets/d80b52f0-ff04-45b2-84a1-3e3ee95f0b0f" />
<img width="1910" height="850" alt="Screenshot 2026-11-10 031034" src="https://github.com/user-attachments/assets/18a09747-4218-4998-af1b-05a34fcae16e" />

· The Vault (Zero-Data-Retention): Deploys inside the hospital's VPC.

## **The 5-Step Pipeline**

1. Mutation Trail (CRISPR): Evaluates genomic signals.
2. Drug Logic (ChEMBL): Matches the mutation to targeted therapies (EGFR L858R -> Osimertinib).
3. PRISM (ClinicalTrials.gov): Fetches active trials and finds hidden outliers.
4. HEMA-CORE (The Death Check): Evaluates CBC data against sex-specific and trial-specific thresholds.
5. The Merge: Orchestrates signals into a single JSON verdict (CLEARED or BLOCKED).

## **Testing & Validation**

· 100/100 Randomized Stress Tests Passed (Offline Mocking): 100 synthetic oncology profiles with mocked external APIs.
  · 95 Critical Bleeding/Infection Risks Blocked.
  · 7 Dynamic Trial Overrides Triggered.
· Visual Validation: The UI dynamically blocks Male Hb 12.5, clears Female Hb 12.5, clears Platelets 120 (due to trial override), and hard-blocks WBC 1.5.

<img width="1902" height="145" alt="Screenshot 2026-11-09 204611" src="https://github.com/user-attachments/assets/c0566ada-f72a-4a80-a9c2-5895469e2ea4" />

## **About the Architect**

Sourabh Singh — Founder & Lead Systems Architect

I am a 20-year-old self-taught Systems Architect and a 4-0 amateur MMA fighter (Lightweight).

I bypassed traditional medical academia (3x NEET dropout) because I realized the legacy healthcare system was fundamentally broken. Instead of trying to fit into it, I decided to build the deterministic safety system that actually protects patients.

I am not just a developer; I am a one-man clinical engineering department. I act as the Founder, the Systems Architect, and the QA Lead. I identify the clinical bottleneck, model the biological logic, and front-load the compliance burden before the patient ever reaches a dangerous decision point.

I am the bridge between medicine and code. I don't just build prototypes; I build the deterministic safety gates that protect patients and reduce clinical liability.

## **Final Statement**

NEXUS is a clinical safety engine built to prevent dangerous mismatches, detect unsafe patients before enrollment, and convert fragmented biomedical signals into a single, defendable decision.
