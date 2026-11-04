# 🧬 Domain Polyglot Ecosystem

**Bridging clinical medicine, bioinformatics, and software architecture.**

This repository is a portfolio of clinical and bioinformatics prototypes built by learning each domain, translating its concepts into software, and validating the resulting logic. It brings together architecture, engines, and tests across **14 clinical and bioinformatics domains**.

> **Medical disclaimer:** These projects are for educational and research exploration only. They are not medical devices and do not provide medical advice, diagnosis, treatment recommendations, or a substitute for professional judgment. Do not use them to make decisions about patient care.

## 🚀 Public prototypes

The public prototypes are individual Streamlit applications. Their source code and demo details are available in each project's repository and README.

| Project | Focus | Validation and features |
| --- | --- | --- |
| **BIJA — Fertility Triage** | Maps AMH, FSH, and semen-analysis inputs to an ART decision-tree prototype covering IUI, IVF, and ICSI. | 20 pytest cases, including azoospermia and PCOS edge cases; includes a “Waiting Room” empathy layer and male-factor considerations. |
| **HEMA-CORE — Unified Hematology** | Blood compatibility, CBC interpretation using stated WHO 2023 thresholds, and Rh-pregnancy risk. | 16 pytest cases. |
| **METABO-CORE — Metabolic & Pharmacokinetic** | Glucose risk classification and pharmacokinetic estimates, including Vd, loading dose, and steady state. | 15 pytest cases. |

**Demo links:** See the corresponding project README for its current demo URL. Add direct repository and demo links to this table when publishing them, so visitors can find each prototype quickly.

## 🔒 Private systems

Some components are maintained in private repositories and are not included in this public portfolio. The concepts include:

- **Human Genetic Data Warehouse:** A proposed master-detail data model connecting domain records through a shared patient identifier.
- **Mutation Trail Explorer:** CRISPR simulation, 3D protein visualization with Py3Dmol, and ChEMBL interaction exploration.
- **EPI-CORE:** Viral immune-escape and microbiome Shannon-diversity risk exploration.
- **EVO-CORE:** Bacterial-resistance and Mendelian-inheritance simulations.
- **Molecular Sequence Engine:** PCR melting-temperature calculations, GC sliding windows, and RNA translation.

Private systems are not available for public use. Contact me via [LinkedIn](https://www.linkedin.com/in/sourabh-singh-7b124934/) to discuss a demonstration.

## 🧪 Validation

The public ecosystem currently reports **85+ passing pytest cases**. Tests target edge conditions such as NaNs, zero standard deviation, extreme outliers, and negative inputs. Test counts describe the current suite; they are not a claim of clinical validation or regulatory approval.

<p align="center">
  <img width="1910" height="706" alt="Prototype test results" src="https://github.com/user-attachments/assets/311b7c15-b74c-41ce-a097-0c483af1de07" />
  <img width="1883" height="722" alt="Prototype screenshot" src="https://github.com/user-attachments/assets/c0f85f5e-ffb7-4a9c-b0b5-db40576249d0" />
  <img width="1909" height="673" alt="Prototype screenshot" src="https://github.com/user-attachments/assets/9801570d-b142-4a0f-8ed8-b0702eff8933" />
  <img width="1920" height="651" alt="Prototype screenshot" src="https://github.com/user-attachments/assets/732464af-3350-4d01-92df-0ac97dd712ea" />
</p>

## 🧠 Engineering principles

1. **Human in the loop:** Tools surface calculations and information; a qualified professional remains responsible for interpretation and decisions.
2. **Relational integrity:** Where persistence is used, MySQL master-detail schemas and audit trails support traceability.
3. **Boundary validation:** Tests exercise thresholds and edge cases, not only typical inputs.
4. **Transparent limitations:** Each tool should document its intended use, assumptions, and limitations.

## 🛠️ Technology

- **Language:** Python
- **Data science:** Pandas, NumPy
- **Bioinformatics:** Biopython, Py3Dmol, NCBI E-utilities, ChEMBL API, PDB API
- **Database:** MySQL
- **Interfaces and visualization:** Streamlit, Matplotlib, Plotly
- **Testing:** pytest

This repository is a portfolio and project index. For installation and usage instructions, consult the README in the individual prototype repository.

## 👨‍💻 About

**Sourabh Singh** — Domain Polyglot and Systems Architect

I am a self-taught engineer with a PCB background. I learn the subject matter, translate it into software, validate the implementation, and ship the product.

- **LinkedIn:** [Sourabh Singh](https://www.linkedin.com/in/sourabh-singh-7b124934/)
- **Architecture notebook:** [Handwritten system designs](https://app.notion.com/p/Architecture-Notebook-11-Domains-40-Days-deb76e18923b4b01a7060ea8ec1a92dc)
- **Email:** [sourabh30542dev@gmail.com](mailto:sourabh30542dev@gmail.com)
