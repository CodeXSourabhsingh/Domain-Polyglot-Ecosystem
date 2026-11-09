# **BIJA-X - Reproductive Genomic Orchestrator**
<p align="center">
  <img src="https://img.shields.io/badge/FastAPI-0d9488?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite" />
  <img src="https://img.shields.io/badge/Tailwind-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white" alt="Pytest" />
</p>

<p align="center">

Deterministic clinical safety orchestration for IVF and patient protection.

BIJA-X is a full-stack clinical platform that merges fertility triage, Mendelian genetics, pharmacogenomics (PGx), and protein impact analysis into a single decision engine. It is designed to prevent fatal adverse events and unnecessary genetic disease transmission during Assisted Reproductive Technology (ART).

## **The Problem**

Standard fertility protocols ignore genetic carrier status and pharmacology:

· Mendelian Blindspots: Standard IUI/IVF protocols proceed without checking if both parents are carriers of recessive disorders (CFTR, HBB).
· Pharmacogenomic Toxicity: Standard IVF protocols prescribe massive progesterone doses, ignoring if the mother is a Poor Metabolizer (CYP3A4).
· Teratogen Risks: Engines frequently pull drugs from oncology databases, risking exposure to Category D teratogens (like Hydroxyurea) during pregnancy.
· Domain Bleed: Oncology mutations (EGFR) accidentally trigger fertility protocols if the engine is not gated.

## **The Solution & Clinical Guardrails**

· Mendelian Override: If both parents are carriers for CFTR DeltaF508, the engine flags a 25% risk and overrides standard IUI to mandate IVF + PGT-M.
· Drug Override (Trikafta): For CFTR DeltaF508, the engine hardcodes Trikafta, bypassing broken ChEMBL API calls (which incorrectly output Ivacaftor).
· Teratogen Block: For HBB (Sickle Cell), the engine hard-blocks Hydroxyurea and recommends Voxelotor.
· Domain Block: If a user types an oncology gene (EGFR), the engine throws a CLINICAL DOMAIN BLOCK.
· Paternal Logic: If the mother is a carrier but the father is normal, the engine clears the PGT-M requirement, saving the patient $10,000.

## **System Architecture**

· Frontend (React + Tailwind): IVF Success Probability gauge, Male Factor vs. WHO Min charts, and mutation trail cards.

<img width="1920" height="874" alt="Screenshot 2026-11-09 154323" src="https://github.com/user-attachments/assets/e70043dd-99d3-4d4e-b0d7-a21832abf558" />
<img width="1920" height="921" alt="Screenshot 2026-11-09 155042" src="https://github.com/user-attachments/assets/1e1a3fef-f298-40a4-be14-077e99ba07ed" />
<img width="1920" height="910" alt="Screenshot 2026-11-09 155110" src="https://github.com/user-attachments/assets/cb4d7935-2ddc-4085-96a5-37af15bd38ea" />
<img width="1916" height="908" alt="Screenshot 2026-11-09 155314" src="https://github.com/user-attachments/assets/3688561a-3cd9-48f6-bc5f-c2654a5a8836" />
<img width="1920" height="1080" alt="Screenshot 2026-11-09 155357" src="https://github.com/user-attachments/assets/bace55f6-7b78-42a3-8ef5-e12214e84aff" />
<img width="1920" height="889" alt="Screenshot 2026-11-09 155435" src="https://github.com/user-attachments/assets/fcb6e8f9-a86d-4636-b8d6-c19e564774e9" />

· Backend (FastAPI + Python): Integrates CRISPR, Protein Impact (PDB), and Drug Logic (ChEMBL).

<img width="1920" height="613" alt="Screenshot 2026-11-10 025927" src="https://github.com/user-attachments/assets/80818878-1e5c-4386-bd4c-35967b1eda4e" />
<img width="1920" height="893" alt="Screenshot 2026-11-10 025954" src="https://github.com/user-attachments/assets/ef0e7c0b-0ad8-4464-b650-9b78b4d9ac7c" />
<img width="1907" height="599" alt="Screenshot 2026-11-10 030011" src="https://github.com/user-attachments/assets/8482bd42-9a03-4efc-85eb-24ebeb0156c1" />

· The Vault (Zero-Data-Retention): Deploys directly into the hospital's AWS VPC.

## **Testing & Validation**

· 100/100 Randomized Stress Tests Passed (Offline Mocking): 100 randomized patients mixing extreme genetics and domain blocks.
  · 45 Standard ART Paths cleared.
  · 30 PGT-M Overrides triggered.
  · 25 Clinical Domain Blocks triggered.
· Visual Validation: The UI proves the engine blocks EGFR, triggers IVF+PGT-M for double CFTR carriers, and blocks Hydroxyurea.

<img width="1920" height="543" alt="Screenshot 2026-11-09 153421" src="https://github.com/user-attachments/assets/d714d3aa-7039-4270-b893-100ae4a0af23" />


## **About the Architect**

Sourabh Singh — Founder & Lead Systems Architect

I am a 20-year-old self-taught Systems Architect and a 4-0 amateur MMA fighter (Lightweight).

I bypassed traditional medical academia (3x NEET dropout) because I realized the legacy healthcare system was fundamentally broken. Instead of trying to fit into it, I decided to build the deterministic safety system that actually protects patients.

I am not just a developer; I am a one-man clinical engineering department. I act as the Founder, the Systems Architect, and the QA Lead. I identify the clinical bottleneck, model the biological logic, and front-load the compliance burden before the patient ever reaches a dangerous decision point.

I am the bridge between medicine and code. I don't just build prototypes; I build the deterministic safety gates that protect patients and reduce clinical liability.

## **Final Statement**

BIJA-X is a reproductive safety engine built to prevent genetic disease transmission, protect mothers from drug toxicity, and convert fragmented biomedical signals into a single, defendable clinical decision layer.
