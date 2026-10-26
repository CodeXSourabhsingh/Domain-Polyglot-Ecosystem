# 🧬 Domain-Polyglot-Ecosystem

The Bridge Between Clinical Medicine and Software Architecture

Clinical software has a bottleneck: the people who understand the medicine can't code, and the people who code don't understand the medicine. I am a Domain Polyglot. I learn the biology, map the decision logic, and build the pipelines.

This repository is the public portfolio for my ecosystem. It contains the architecture, the engines, and the validation for 14 different clinical and bioinformatics domains.

---

## LIVE DEMO is inside the tool readme

## 🚀 The Ecosystem

Click on any project below to view its detailed architecture, screenshots, clinical logic, and live demo link.


🚀 The Public Arsenal (Live Prototypes)

These are the individual engines. They are deployed on Streamlit and the code is available in the linked repositories.


1. BIJA: Fertility Triage

· Logic: Maps AMH, FSH, and semen analysis to an ART decision tree (IUI, IVF, ICSI).
· Validation: 20 Pytest cases covering extreme outliers (Azoospermia, PCOS).
· Features: The "Waiting Room" empathy layer, male-factor inclusion.

2. HEMA-CORE: Unified Hematology

· Logic: Blood compatibility, CBC interpretation (WHO 2023 thresholds), and Rh-pregnancy risk.
· Validation: 16 Pytest cases.

3. METABO-CORE: Metabolic & Pharmacokinetic

· Logic: Glucose risk classification + Pharmacokinetic dose estimation (Vd, Loading Dose, Steady State).
· Validation: 15 Pytest cases.

---

🔒 The Proprietary Megazone (Private Repositories)

The true power of this ecosystem is the Human Genetic Data Warehouse.

It is a unified Master-Detail schema that connects every domain using a master patient_id. A physician enters a single ID and instantly sees the patient's hematology, pharmacokinetics, fertility, and microbiome data.

Because this is proprietary IP, the merged code is kept in a private repository.

· Mutation Trail Explorer: CRISPR simulation → 3D Protein (Py3Dmol) → ChEMBL Drug Interactions.
· EPI-CORE: Viral immune escape + Microbiome Shannon Diversity combined risk.
· EVO-CORE: Bacterial resistance (Fleming) + Mendelian inheritance (Mendel) simulations.
· Molecular Sequence Engine: PCR Tm calculations, GC sliding windows, RNA translation.

If you would like a live demo of the Megazone or the proprietary engines, please reach out via LinkedIn.

---

🧪 Test-Driven Development (The Proof)

I don't just build; I validate. Every engine is tested against the worst-case biological scenarios (NaNs, SD=0, extreme outliers, negative inputs).

Current Test Coverage: 85+ Passing Pytest Cases
(Screenshot of terminal with green text goes here)

---

## 🧠 The Engineering Philosophy

Every platform in this ecosystem is built on the same foundational architecture:

1.  **Human-in-the-Loop:** The software flags risks, calculates probabilities, and surfaces insights. It does *not* autonomously prescribe. The physician or researcher makes the final decision.
2.  **Relational Integrity:** Data is persisted using Master-Detail schemas in MySQL. Nothing is ephemeral; every calculation is logged for auditability.
3.  **Boundary Validation:** Clinical logic is only as good as its edge cases. Every tool is backed by rigorous Pytest suites that test exact clinical thresholds.
4.  **Honest Limitations:** Every README and UI clearly states what the tool does *not* do.


🛠️ The Tech Stack

· Languages: Python
· Data Science: Pandas, NumPy
· Bioinformatics: Biopython, Py3Dmol, NCBI E-utilities, ChEMBL API, PDB API
· Database: MySQL (Relational Schema, LEFT JOINs, Audit Trails)
· UI: Streamlit, Matplotlib, Plotly
· Testing: Pytest


## 👨‍💻 About the Architect

**Sourabh Singh** 
* Domain polyglot & Systems Architect*

I am a self-taught engineer 12th pass (PCB) No degree, no bootcamp; I don't just write code; I learn the domain, architect the system, and ship the product. That's the job.

*   **LinkedIn:** [Sourabh Singh](https://www.linkedin.com/in/sourabh-singh-7b124934/)
*   **Architecture Notebook:** [View my handwritten system designs](https://app.notion.com/p/Architecture-Notebook-11-Domains-40-Days-deb76e18923b4b01a7060ea8ec1a92dc)
*   **Email:** sourabh30542dev@gmail.com
