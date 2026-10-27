# 🧬 Mutation Trail Explorer

Built by Sourabh Singh

Python | Streamlit | MySQL | Biopython | Py3Dmol | ChEMBL API

A research workflow for tracing the path from a genetic mutation to protein disruption and therapeutic opportunity.

---

## Overview

Mutation Trail Explorer is a precision-medicine research pipeline that connects multiple layers of biological evidence into a single, auditable workflow.

It helps researchers answer four critical questions in sequence:

1. Where does the CRISPR edit occur in the DNA?
2. How does that mutation affect the protein structure and function?
3. Is the mutation likely destabilizing or neutral?
4. Which drug candidates may interact with the affected target?

Instead of manually jumping across NCBI, PDB, and ChEMBL, the pipeline consolidates the workflow into one dashboard for structured investigation and review.

---

## Why this project exists

In precision medicine, a mutation is not the end of the story — it is the beginning of a biological chain. A variant may appear benign in a raw sequence, yet still damage a protein's structure, alter its function, or create a druggable opportunity.

The challenge is that the relevant evidence is spread across disconnected sources:

- DNA sequence data from NCBI
- Structural information from RCSB PDB
- Functional and drug-binding insights from ChEMBL

Researchers lose time, context, and confidence when these steps are disconnected. Mutation Trail Explorer exists to provide a structured trail from mutation to mechanism to treatment.

---

## What the pipeline does

The system follows a 4-step evidence chain:

### 1. The Tailor: CRISPR Target Analysis
- Fetches DNA sequence data from NCBI using the target gene
- Identifies PAM motifs and candidate gRNA targets
- Estimates cut positions and cleavage plausibility
- Evaluates GC content and sequence suitability

### 2. The Check: Human-in-the-Loop Verification
- Requires researcher confirmation before proceeding
- Prevents fully automated clinical or biological decisions
- Ensures the sequence and target interpretation are validated before structural analysis

### 3. The Broken Zipper: Protein Impact Analysis
- Maps the mutation onto the protein structure using PDB data
- Visualizes the structure with Py3Dmol
- Evaluates protein surface properties using hydrophobicity analysis
- Uses BLOSUM62 scoring to classify mutations as destabilizing or neutral

### 4. The Cure: Drug Discovery
- Queries ChEMBL for relevant drugs and compounds
- Normalizes binding data into nanomolar units
- Classifies interaction strength using standardized thresholds
- Supports prioritization of candidate therapies for further investigation

---

## Key capabilities

- Gene-based DNA retrieval and validation
- CRISPR cut-site simulation and target evaluation
- Sequence verification gate for biological oversight
- Mutation-to-structure mapping
- Protein impact classification
- Drug target and binding affinity discovery
- Normalized affinity scoring across multiple assay types
- Detailed audit trail storage in MySQL

---

## Tech stack

- Language: Python
- UI: Streamlit
- Data analysis: Pandas, NumPy
- Bioinformatics: Biopython
- Structural visualization: Py3Dmol
- Biological databases:
  - NCBI E-utilities
  - RCSB PDB
  - ChEMBL
- Database: MySQL
- Visualization: Matplotlib

---

## Validation and testing

This project is built with a test-driven mindset. The validation suite targets biologically risky edge cases and conversion accuracy to prevent silent logic errors.

### Covered test areas
- CRISPR math:
  - reverse complement logic
  - lowercase normalization
  - empty sequence handling
- Protein physics:
  - hydrophobicity boundary values
  - invalid amino acid handling
- BLOSUM62 logic:
  - conservative mutation handling
  - destabilizing mutation classification
- Unit conversions:
  - uM, mM, pM, and M to nM
  - affinity normalization and classification

### Validation status
- 18/18 boundary and logic tests passing

- <img width="1920" height="718" alt="Screenshot 2026-10-26 230301" src="https://github.com/user-attachments/assets/1f1d24d6-eb14-487c-97e7-3815df8b3728" />


---

## Example use case

A researcher might begin with a mutant gene such as HBB and ask:

- Where does the CRISPR edit fall within the sequence?
- Does the mutation alter the protein surface hydrophobicity?
- Is the mutation destabilizing according to BLOSUM62 logic?
- What drugs or compounds are associated with the related protein target?

Mutation Trail Explorer is designed to help answer these questions in a single structured workflow.

---

## Local setup

### 1. Clone the repository

```bash
git clone https://github.com/CodeXSourabhsingh/Mutation-Trail-Explorer.git
cd Mutation-Trail-Explorer
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure application secrets
Set up your configuration file or Streamlit secrets with your MySQL credentials and any required API access settings.

### 4. Run the app

```bash
streamlit run app.py
```

---

## Project assumptions and constraints

This project is intended for research support, not direct clinical decision-making.

### Important limitations
- Research use only: This tool does not provide clinical diagnoses or treatment recommendations.
- PDB dependency: Structural rendering requires a valid protein structure in the RCSB database.
- API latency: The pipeline depends on live external services, which may be slower under heavy traffic.
- Human verification required: The workflow intentionally includes a review gate before deeper downstream analysis.

---

## Why the human-in-the-loop step matters

The system is intentionally designed to avoid premature automation in biology and medicine.

> "The mode is a data decision, not a capability decision. We build the bridge; the physician decides."

This reflects the project’s philosophy: computational tools can support exploration and prioritization, but expert review remains essential in scientific and clinical decision-making.

---

## Future roadmap

Planned improvements include:

- stronger off-target scoring models
- improved variant prioritization workflows
- integration with more protein structure sources
- support for additional organisms and gene families
- more robust benchmarking and reproducibility tools
- expanded case-study datasets for validation

---

## Final note

Mutation Trail Explorer is not meant to replace biological expertise or laboratory testing. It is a decision-support platform that reduces the manual burden of connecting genomic, structural, and therapeutic evidence into one traceable workflow.

For researchers working across the mutation-to-target-to-treatment chain, it provides a practical bridge between raw biological data and actionable interpretation.

---

"The mode is a data decision, not a capability decision. We build the bridge; the physician decides."
