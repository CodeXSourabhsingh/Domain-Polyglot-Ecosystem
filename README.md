# 🧬 Domain-Polyglot-Ecosystem

**The Bridge Between Medicine and Code.**

Clinical software has a bottleneck: the people who understand the medicine can't code, and the people who code don't understand the medicine. I am the bridge. I learn complex biological domains, model their clinical decision logic, and ship production-grade software pipelines.

This repository is the central hub for my clinical and bioinformatics platforms. 

> **🛑 COMMERCIAL LICENSING NOTICE:** 
> The source code for the platforms listed below is **proprietary and maintained in private repositories.** This public repository serves as the architectural showcase and documentation hub. All platforms are live and available for demonstration. For commercial deployment, integration, or source code licensing, please contact me directly.

---
## LIVE DEMO is inside the tool readme

## 🚀 The Ecosystem

Click on any project below to view its detailed architecture, screenshots, clinical logic, and live demo link.

### 1. [HEMA-CORE: Hematology & Clinical Triage](./HEMA_CORE.md)
A unified hematology pipeline that interprets Complete Blood Counts (CBC), calculates ABO/Rh blood compatibility, and evaluates Rh-pregnancy risk.
*   **Domain:** Hematology, Obstetrics
*   **Tech:** Python, Pandas, MySQL, Streamlit, Pytest
*   **Highlights:** Built on WHO (2023) and ACOG guidelines. Includes strict boundary testing to catch `<` vs `<=` clinical errors.

### 2. [METABO-CORE: Metabolic & PK Dosing](./METABO_CORE.md)
A clinical dashboard that merges metabolic risk assessment (glucose/diabetes) with pharmacokinetic dose estimation (Vd, Loading Dose, Maintenance Dose).
*   **Domain:** Metabolic, Pharmacology
*   **Tech:** Python, Pandas, MySQL, Streamlit, Matplotlib
*   **Highlights:** Uses a Single Table Inheritance SQL pattern to log both glucose and PK data in one schema. Implements real clinical parameters for Warfarin, Digoxin, and Gentamicin.

### 3. [BIJA: Fertility Triage Engine]
An empathetic patient-facing triage tool that translates complex fertility lab reports (AMH, FSH, LH) into actionable, human-readable guidance.
*   **Domain:** Reproductive Medicine
*   **Tech:** Python, MySQL, Streamlit, Plotly
*   **Highlights:** Built on SART/ACOG guidelines. Features an "Education Mode" for patients without labs, and strict human-in-the-loop architecture. Protected by 16 boundary tests.

### 4. [Mutation Trail Explorer: Precision Medicine]
A 4-step clinical research pipeline that traces a genetic mutation from CRISPR targeting to Protein structural impact, and finally to FDA-approved Drug targets.
*   **Domain:** Genomics, Structural Biology, Drug Discovery
*   **Tech:** Python, Biopython, Py3Dmol, ChEMBL API, MySQL
*   **Highlights:** Integrates NCBI, PDB, and ChEMBL APIs. Features BLOSUM62 scoring, Kyte-Doolittle hydrophobicity profiling, and a forced human verification step before API consumption.

### 5. [Molecular Sequence Engine: Pure Python Bioinformatics]
A unified platform that takes a raw DNA sequence, calculates the GC sliding window, translates it to a protein, and calculates the PCR Tm (thermodynamics). 
*   **Domain:** Molecular Biology, Genetics
*   **Tech:** Pure Python (No Biopython), MySQL, Streamlit
*   **Highlights:** Refactored from raw terminal scripts into a relational Master-Detail architecture. Uses `LEFT JOIN` queries to aggregate data across multiple tables. Implements the Marmur-Doty thermodynamic equation from scratch.

### 6. [EVO-CORE: Evolution Simulation Engine]
A computational biology engine that simulates the survival of the fittest. Models bacterial resistance under antibiotic pressure and Mendelian genetic inheritance.
*   **Domain:** Population Dynamics, Evolutionary Biology
*   **Tech:** Python, MySQL, Streamlit, Matplotlib
*   **Highlights:** Runs Monte Carlo simulations (up to 100,000 iterations) to prove the 9:3:3:1 ratio. Features logistic growth models for MRSA under penicillin pressure. 

### 7. [Advanced Bio-Code: The 6-Domain Ecosystem](./Advanced_Bio_Code.md)
A multi-domain bioinformatics suite covering CRISPR editing, PRISM clinical cohort filtering (10M records processed in <2 mins), Virology tracking, and Microbiome diversity.
*   **Domain:** Multi-omics, Clinical Trials, Epidemiology
*   **Tech:** Python, Pandas, Scikit-learn, MySQL
*   **Highlights:** 31 passing Pytest tests. Processes massive datasets on standard consumer hardware without GPU acceleration.

---

## 🧠 The Engineering Philosophy

Every platform in this ecosystem is built on the same foundational architecture:

1.  **Human-in-the-Loop:** The software flags risks, calculates probabilities, and surfaces insights. It does *not* autonomously prescribe. The physician or researcher makes the final decision.
2.  **Relational Integrity:** Data is persisted using Master-Detail schemas in MySQL. Nothing is ephemeral; every calculation is logged for auditability.
3.  **Boundary Validation:** Clinical logic is only as good as its edge cases. Every tool is backed by rigorous Pytest suites that test exact clinical thresholds.
4.  **Honest Limitations:** Every README and UI clearly states what the tool does *not* do.

---

## 👨‍💻 About the Architect

**Sourabh Singh** 
*Forward Deployed Engineer & Systems Architect*

I am a self-taught engineer. I don't just write code; I learn the domain, architect the system, and ship the product. 

*   **LinkedIn:** [Sourabh Singh](https://www.linkedin.com/in/sourabh-singh-7b124934/)
*   **Architecture Notebook:** [View my handwritten system designs](https://app.notion.com/p/Architecture-Notebook-11-Domains-40-Days-deb76e18923b4b01a7060ea8ec1a92dc)
*   **Email:** sourabh30542dev@gmail.com

*Available for founding engineer roles, custom pipeline development, and commercial software licensing.*
