# BIJA & BIJA-X — Clinical Fertility & Genomic Orchestrator
<p align="center">
  <img src="https://img.shields.io/badge/FastAPI-0d9488?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite" />
  <img src="https://img.shields.io/badge/Tailwind-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white" alt="Pytest" />
</p>

<p align="center">
**Deterministic ART Triage and Mendelian Safety Gates.**

## 1. The Problem: The Fertility Blindspot

Standard fertility protocols fail in two critical areas:

1. Data Silos: Patients are forced to Google their AMH and FSH levels at 2 AM, while doctors spend 15 minutes of every consultation explaining basic triage.
2. Silent Genetic Carriers: Two healthy parents can both be carriers of a severe autosomal recessive disease (like Cystic Fibrosis). Standard IUI proceeds blindly, resulting in a 25% chance of passing[...]

## 2. The Solution: A Two-Tier Clinical Engine

BIJA is a full-stack clinical platform split into two distinct modules:

· Base BIJA (The Triage Layer): A patient-facing education and calculation tool that ingests WHO semen analysis and ASRM endocrine panels to map the correct ART pathway (IUI, IVF, ICSI).
· BIJA-X (The Genomic Layer): A doctor-facing safety gate. When a Mendelian mutation is detected, BIJA-X overrides standard ART and forces Preimplantation Genetic Testing (PGT-M).

## 3. Clinical Deep Dive: The Base BIJA Triage

Base BIJA uses deterministic logic to navigate the 6 ART Branches:

1. Standard IUI
2. IUI + Ovulation Induction
3. Standard IVF
4. IVF + ICSI (Male Factor)
5. IVF + PGT-M (Genetic Factor)
6. IVF + Donor (Severe DOR)

The Clinical Guidelines Used:

· WHO 2021 Guidelines: Used for strict male factor evaluation (Sperm Count < 15M, Motility < 40%, Morphology < 4%).
· ASRM / SART / CDC: Used for female endocrine evaluation (AMH, Day 3 FSH, LH:FSH ratio) and age-based IVF/IUI success probability mapping.

<img width="1920" height="876" alt="Screenshot 2026-11-14 005538" src="https://github.com/user-attachments/assets/87d82efc-abb0-46f4-9197-546ba4d54cf2" />

<img width="1920" height="872" alt="Screenshot 2026-11-14 004817" src="https://github.com/user-attachments/assets/e6995f2f-6a68-40ac-bdaa-82db423769e4" />

<img width="1920" height="904" alt="Screenshot 2026-11-14 004603" src="https://github.com/user-attachments/assets/62919691-ef96-48ee-afca-08e1cf5768b4" />

## 4. Clinical Deep Dive: The BIJA-X Mendelian Layer

Unlike black-box AI, BIJA-X uses hardcoded Mendelian inheritance rules to dictate the clinical strategy.

· Autosomal Recessive (e.g., CFTR, HBB): If both parents are carriers, there is a 25% chance of an affected embryo. The engine mandates IVF + PGT-M.
· Autosomal Dominant (e.g., BRCA1, Huntington's): Only one parent needs the mutation. 50% transmission risk. The engine mandates IVF + PGT-M regardless of partner status.
· X-Linked (e.g., DMD, Fragile X): The mother is a carrier. Male embryos have a 50% chance of being severely affected. The engine mandates IVF + PGT-M (Sex Selection Required).
· The "Unknown Partner" Hold: If the mother is a carrier but the partner's status is unknown, the engine hard-blocks the cycle and flashes: HOLD - MANDATORY PARTNER TESTING.

<img width="1903" height="919" alt="Screenshot 2026-11-15 122718" src="https://github.com/user-attachments/assets/5befd951-9d39-4c50-babd-5aa2ebdfe294" />

<img width="1900" height="884" alt="Screenshot 2026-11-15 123023" src="https://github.com/user-attachments/assets/5c0556f2-1a0a-45ee-b2b0-9283ffa46537" />

<img width="1920" height="902" alt="Screenshot 2026-11-15 123043" src="https://github.com/user-attachments/assets/f9c1e99a-495f-4143-8022-bbdc4c67532b" />

<img width="1920" height="879" alt="Screenshot 2026-11-15 123119" src="https://github.com/user-attachments/assets/a137925d-4494-4b56-86f8-b158ec217f50" />

## 5. Enterprise Architecture

This is not a toy script. It is a production-grade architecture built for clinic evaluation.

· The Vault (Zero-Data-Retention): The Docker container deploys into the clinic's VPC. We store zero PHI.
· The Bouncer (Pydantic): Strict input validation prevents impossible data (e.g., negative AMH) from reaching the math engine.
· The Frontend: React + Tailwind CSS, with real-time Recharts visualizations mapping the patient's hormones against normal clinical ranges.

## 6. Extreme Stress Testing

To prove it is production-grade, we engineered a hostile Pytest suite to break the engine.

· 13 Targeted Clinical Cases: Proven to correctly trigger IUI, IVF, ICSI, Autosomal Recessive, Autosomal Dominant, and X-Linked pathways.
· The Negative Bouncer: Tested with negative ages and zero hormones to ensure the math never divides by zero.
· The Chaos Fuzzer: 500 randomized, impossible patient profiles were thrown at the API. The engine processed all of them without a single crash.

<img width="1920" height="690" alt="Screenshot 2026-11-15 123632" src="https://github.com/user-attachments/assets/f20742b0-02e0-4277-97da-f2a7c84cea8e" />

## 7. The Ecosystem Roadmap: Node 2 Vision

While the current BIJA-X engine is a lightweight, pure-logic decision gate, it is built to scale into a massive Genomic Orchestrator.

· Phase 2 (The Mutation Trail): In future enterprise deployments, BIJA-X will integrate with NCBI, PDB, and ChEMBL APIs to fetch live DNA sequences, predict protein destabilization, and check drug in[...]
· The Clinical Compiler: BIJA is Node 2 of a massive ecosystem. Node 1 is the PGx Warfarin engine. Together, they prove the architecture can merge Fertility, Pharmacology, and Genetics into a single [...]

## 8. Regulatory Strategy: CDS vs. SaMD

Our regulatory philosophy: Explainable, Deterministic, and Accountable.

· Clinical Decision Support (CDS): Under the 21st Century Cures Act, BIJA is strictly classified as a CDS tool. It does not autonomously prescribe or perform embryo transfers.
· Defensible Audit Trail: Because our logic is hardcoded to Mendelian inheritance patterns and WHO guidelines, it is fully explainable.

## 9. About the Architect

Sourabh Singh — Founder & Lead Systems Architect

I am a 20-year-old self-taught Systems Architect and a 4-0 amateur MMA fighter (Lightweight).

I am a 3x NEET candidate. I cleared the cutoff for a private medical college, but I refused to buy my way in. I wanted to earn it, but I was training for MMA fights at the same time, which kept me fro[...]

Instead of crying about the legacy system, I realized the medical field didn't just need more doctors—it needed better software architecture. So I taught myself Python, FastAPI, and React.

I am not just a developer; I am a one-man clinical engineering department. I identify the clinical bottleneck, model the biological logic, and build the patient-safety layer that turns raw data into d[...]

## Final Statement
BIJA is not just a fertility calculator. It is a clinical safety engine built to prevent genetic disease transmission, detect unsafe patients before ART initiation, and convert fragmented biomedical s[...]

---

## 🚨 LEGAL DISCLAIMER & TERMS OF USE

Not a Medical Device: The BIJA / BIJA-X Engine is a software prototype designed to demonstrate the capabilities of deterministic Clinical Decision Support (CDS). It is not a medical device, does not p[...]

No Substitute for Clinical Judgment: The outputs generated by this engine (including genetic overrides, warnings, and recommendations) are for informational purposes only. The engine does not autonomo[...]

Regulatory Status: This software has not been cleared or approved by the US Food and Drug Administration (FDA) or any equivalent international regulatory authority (e.g., EMA, MHRA). It is currently a[...]

Limitation of Liability: The Architect (Sourabh Singh) assumes no liability for any clinical outcomes, adverse events, or damages arising from the use of, or reliance upon, the information or software[...]

Data Privacy: The deployment architecture described herein utilizes a "Zero-Data-Retention" (Bring Your Own Data) model. The developer does not collect, store, or transmit any Protected Health Informa[...]
