**🧬 The Reproductive Quadruble: A Unified Women's Health Ecosystem**

<p align="center">
  <img src="https://img.shields.io/badge/FastAPI-0d9488?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite" />
  <img src="https://img.shields.io/badge/Tailwind-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white" alt="Pytest" />
</p>


Deterministic Orchestration for Reproductive Genomics, Microbiome Ecology, and Precision Dosing.

Built by Sourabh Singh | Systems Architect & Domain Polyglot | FastAPI | React | Docker | Python | Pytest

---

**Executive Summary (The Vision)**

The current standard of care for women’s health is fragmented. It treats the female reproductive system as a series of isolated silos: hormones are treated in one clinic, the microbiome in another, and genetic carrier status is often ignored until it is too late.

The Reproductive Quadruble is not a collection of apps. It is a single, unified clinical ecosystem. It merges Mendelian genetics, ecological microbiome tracking, evolutionary phylogenetics, and pharmacokinetics into a single deterministic architecture. We are shifting women's health from "population averages and guesswork" to explainable, mathematically proven precision medicine.

**The Core Problem (Why Legacy Systems Fail)**

Legacy healthcare IT systems fail women’s health for three reasons:

1. The "Black Box" of AI: Legacy systems rely on probabilistic ML models trained on messy, incomplete EHR data. In medicine, a hallucination is a fatality.
2. The "Blind" Standard of Care: Standard IVF protocols and antibiotic treatments ignore the patient's genetic metabolizer status (PGx) and fail to account for the evolutionary resistance of pathogens.
3. Data Silos: A doctor cannot see the patient’s microbiome phylogeny while prescribing an antibiotic, and they cannot see the patient’s CYP3A4 metabolism while prescribing IVF hormones.

**The 5 Engines (The Architecture of Care)**

1. BIJA-X: The Reproductive Genomic Orchestrator(Architecture done and deployed)

· The Concept: Merges standard fertility triage (AMH, FSH, Sperm Count) with genetic carrier screening (CFTR, HBB).
· The Value: It prevents fatal genetic diseases. If both parents are carriers for a monogenic disorder (e.g., Cystic Fibrosis), the engine automatically overrides standard fertility treatments and mandates IVF + PGT-M (Preimplantation Genetic Testing) AND mutation , protein(using BLOSUM62 for neutral and destablizing) and drug fetched from (NCBI,PDB.CHEMBL).

**BACKEND**

<img width="1920" height="615" alt="Screenshot 2026-11-08 053122" src="https://github.com/user-attachments/assets/2867bfff-506d-452f-a33b-5d0ac13a6dc0" />
<img width="1920" height="690" alt="Screenshot 2026-11-08 090742" src="https://github.com/user-attachments/assets/07cb271e-bcfa-4c4d-880a-75d44128879e" />
<img width="1920" height="690" alt="Screenshot 2026-11-08 090742" src="https://github.com/user-attachments/assets/68c943fa-f5d8-474a-89df-4219af6d8944" />
<img width="1920" height="632" alt="Screenshot 2026-11-08 090645" src="https://github.com/user-attachments/assets/60135705-e1d5-4dd8-bf43-b0d34c5ccff9" />

**FRONTEND**
<img width="1892" height="781" alt="Screenshot 2026-11-08 061343" src="https://github.com/user-attachments/assets/7bbefbaa-35a1-4d63-a435-d46b8184f3f5" />
<img width="1920" height="889" alt="Screenshot 2026-11-08 065123" src="https://github.com/user-attachments/assets/a2e3b9a8-969a-4604-ae23-6d25ba0e808f" />
<img width="1920" height="916" alt="Screenshot 2026-11-08 091501" src="https://github.com/user-attachments/assets/43cf2478-6b03-46d3-b89d-91f31a991805" />
<img width="1907" height="883" alt="Screenshot 2026-11-08 065932" src="https://github.com/user-attachments/assets/a7e8ba62-65a9-4901-9ba3-a5eb92e73f24" />

**PYTEST**
<img width="1920" height="639" alt="Screenshot 2026-11-03 194848" src="https://github.com/user-attachments/assets/4d369cae-532c-40be-abf9-f596bea7cc25" />
<img width="1920" height="639" alt="Screenshot 2026-11-03 194848" src="https://github.com/user-attachments/assets/9bcbf9c8-81c6-43a8-aa2e-acf94787eb80" />
<img width="1920" height="624" alt="Screenshot 2026-11-03 194906" src="https://github.com/user-attachments/assets/88952fdf-7d8b-445d-85a6-148ba342912e" />


2. Vagina-X: The Microbiome Stewardship Engine(Architecture done)

· The Concept: Analyzes the vaginal microbiome (Lactobacillus vs. Gardnerella) using the Shannon Diversity Index and ecological modeling.
· The Value: Predicts the risk of Bacterial Vaginosis (BV) recurrence. It mathematically proves that standard antibiotics alone will fail if the "good" bacterial ecology isn't restored, mandating combination therapy (antibiotics + probiotics).

3. BIJA-X + PGx: Precision IVF Dosing(Architecture done)

· The Concept: Merges fertility planning with Pharmacogenomics (CYP3A4 metabolism).
· The Value:  Patients undergoing IVF take massive doses of progesterone. If a woman is a "Poor Metabolizer," standard doses cause toxic accumulation (severe sedation, liver stress). This engine calculates the exact personalized dose to ensure a safe pregnancy.

4. Vagina-X + PGx: Antimicrobial Stewardship(Architecture done)

· The Concept: Merges microbiome treatment with antibiotic metabolism.
· The Value: Prevents the evolution of drug-resistant superbugs by ensuring the patient metabolizes the antibiotic at the correct rate. It avoids sub-therapeutic exposure, which is the primary driver of antimicrobial resistance (AMR).

5. Vagina-Phylo: Evolutionary Strain Tracking(Architecture done)

· The Concept: Merges the Vagina-X microbiome engine with Phylogenetic Tree Building (Jukes-Cantor distance, UPGMA clustering).
· The Value: It takes raw DNA sequences (FASTA) from a patient's swab and builds an evolutionary tree against known superbugs. If the engine spots a mutant strain branching off, it blocks standard antibiotics and mandates aggressive combination therapy before the infection becomes untreatable.

---

**System Architecture & Tech Stack**

This ecosystem is built on a Production-Grade Factory Architecture. It is designed to be deployed in regulated, high-stakes clinical environments.

· The Bouncer (FastAPI + Pydantic): Every API endpoint is strictly validated. If a clinician inputs messy, incomplete, or erroneous data, the engine rejects it with a 422 Unprocessable Entity. We do not let "garbage in, garbage out."
· The Box (Docker): Every engine is containerized. It runs identically on a local laptop or a hospital's cloud server without environment crashes.
· The Vault ("Bring Your Own Data"): We do not store Patient Health Information (PHI). The Docker containers are designed to be deployed directly into a hospital's AWS VPC. The patient data never leaves the hospital's walls, ensuring instant HIPAA compliance.
· The Interface (React + Tailwind + Streamlit): High-contrast, dark-mode clinical dashboards designed for quick triage and risk flagging.

**Validation & Testing (The Pytest Philosophy)**

In clinical software, a math error is a liability. A bug is a fatal adverse event.

· Deterministic Logic First: We reject unreliable black-box automation. The clinical math (pharmacokinetics, Mendelian inheritance, Shannon Diversity) is governed by strict, hardcoded formulas.

· Explainable AI (XAI): When ML is utilized (e.g., the BIJA-X ML fertility predictor), the model does not just output a prediction; it outputs the exact feature contributions. Example: "Age contributed 40%, AMH contributed 30% to the risk." The clinician sees the exact reasoning.

· Boundary Testing: The engines are validated with hundreds of Pytest cases covering extreme clinical edge cases (e.g., zero sperm count, toxic drug accumulation, missing genetic data) to ensure the API fails safely, never silently.

---

**About the Architect**

Sourabh Singh - Systems Architect & Domain Polyglot

I am a 20-year-old self-taught Systems Architect. My work is rooted in one principle: technology should make medicine safer, more explainable, and more operationally sound.

I am not a standard software engineer. I am the bridge. The people who understand the medicine can't code, and the people who code don't understand the medicine. I learn a medical specialty (Genomics, Virology, Reproductive Endocrinology), model its decision logic, and ship a production-grade platform.

I build software that is technically rigorous and operationally trustworthy. I don't just build prototypes; I build the deterministic safety gates that protect patients and reduce clinical liability.

Let’s build the future of women's health.
For collaborations, technical discussions, or pilot deployments, reach out via LinkedIn or my project repositories.

---
