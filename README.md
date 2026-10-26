# 🧬 Domain-Polyglot Ecosystem

The Bridge Between Clinical Medicine and Software Architecture

Clinical software has a bottleneck: the people who understand the medicine can't code, and the people who code don't understand the medicine. I am a Domain Polyglot. I learn the biology, map the decision logic, and build the pipelines.

This repository is the public portfolio for my ecosystem. It contains the architecture, the engines, and the validation for 14 different clinical and bioinformatics domains.

---

🏗️ The Architecture

Every tool in this ecosystem follows the same modular design:

1. The Engine: Pure Python logic (Pandas, NumPy, Biopython). No UI, no database. Just the math.
2. The UI: A Streamlit dashboard for human interaction.
3. The Database: A MySQL audit trail (PII-free) to log every calculation.
4. The Tests: Custom Pytest suites validating the clinical boundary conditions.

Core Philosophy: Indicative data → flag. Verified patient-specific data → prescribe. Human-in-the-loop. Cited sources. Honest limitations.

---

🚀 The Public Arsenal (Live Prototypes)

These are the individual engines. They are deployed on Streamlit and the code is available in the linked repositories.

(Note: Add your Streamlit links here when you are ready)

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

4. PRISM: Clinical Trial Cohort Filter

· Logic: Fetches trial criteria from ClinicalTrials.gov, generates 10M synthetic patients, filters by genomic mutations.
· Validation: 12 Pytest cases.

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

🛠️ The Tech Stack

· Languages: Python
· Data Science: Pandas, NumPy
· Bioinformatics: Biopython, Py3Dmol, NCBI E-utilities, ChEMBL API, PDB API
· Database: MySQL (Relational Schema, LEFT JOINs, Audit Trails)
· UI: Streamlit, Matplotlib, Plotly
· Testing: Pytest

---

👨‍💻 About the Architect

I am Sourabh Singh. I am 20 years old, self-taught, and 3 months into coding. I don't have a CS degree. I learn domains fast, map the architecture by hand, and ship working tools.

· LinkedIn: [Link]
· Email: [Email]

“The mode is a data decision, not a capability decision.”
