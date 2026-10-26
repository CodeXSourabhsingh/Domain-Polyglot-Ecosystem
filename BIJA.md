# 🩺 BIJA — Clinical Fertility Triage

## Live Demo

Try the live BIJA app here:

https://egfkwhydbfb22uavluzdf4.streamlit.app/

## Executive Summary

BIJA is a clinical decision-support prototype designed to help patients and clinicians interpret common fertility lab values in context. It transforms hormone and semen analysis results into clear educational guidance, highlights clinically relevant patterns, and suggests likely next-step pathways without replacing physician judgment.

BIJA is intended for patient education, triage awareness, and clinical workflow understanding. It is not a substitute for physician evaluation, individualized treatment planning, or medical diagnosis.

> Important: BIJA is a decision-support educational tool, not a medical diagnosis or treatment plan. It uses reference-based logic and guideline-informed patterns to support interpretation and discussion, but final clinical decisions must be made by qualified healthcare professionals.

## At a Glance

- Purpose: fertility lab interpretation and educational triage
- Primary users: patients, clinicians, care coordinators, fertility education workflows
- Core inputs: AMH, FSH, LH, AFC, TSH, prolactin, semen analysis, age, tubal factor, genetic history
- Typical outputs: risk interpretation, reference-zone visual cues, likely care-path suggestions
- Key boundary: decision support only; not a diagnosis or treatment plan

## Why BIJA Exists

Fertility assessment can be emotionally intense and medically confusing. Patients often receive lab results without enough context to understand what the numbers mean or what their next steps should be. In many cases, the information arrives as raw values and thresholds, without clear guidance about likely clinical relevance.

BIJA addresses this by:

- 🧠 helping users interpret key fertility markers
- ⚠️ highlighting risk patterns based on clinical thresholds
- 🩺 surfacing likely next-step recommendations
- 🤝 separating education from diagnosis
- 👨‍👩‍👧‍👦 incorporating both female and male fertility factors

## The Philosophy of Bīja

Bīja is the Sanskrit word for “seed.” It represents origin, potential, and the beginning of life. We chose this name because a fertility journey is not merely a mathematical exercise—it is deeply personal, uncertain, and often emotionally significant.

BIJA aims to bring clarity to that complexity without pretending to replace clinical judgment.

## Design Principles

BIJA is intentionally designed around a human-in-the-loop model:

1. 😌 Empathy first
   Before asking for clinical inputs, the interface acknowledges stress and uncertainty.

2. 🚫 Flagging, not prescribing
   The tool uses reference-based logic and guideline-informed patterns to suggest possible clinical pathways, but it clearly states that it is not a medical diagnosis.

3. 👨‍🦱 Inclusion of male factor fertility
   Male factors are often underrepresented in fertility tools. BIJA explicitly evaluates parameters such as sperm count, motility, morphology, and history of varicocele where relevant.

## Intended Use

BIJA is intended for:

- 📚 patient education
- 🏥 triage support
- 🧾 clinical workflow awareness
- 📊 understanding fertility lab patterns in context

BIJA is not intended for:

- 🩺 replacing a physician
- 🧠 giving individualized treatment plans
- 🤖 autonomous medical decision-making
- 🏛️ use as a substitute for specialist evaluation

## System Overview

BIJA follows a modular, three-layer architecture:

- `BIJA_app.py` — 🖥️ User interface layer
  - Built with Streamlit
  - Manages user interaction, session state, and report generation
  - Keeps the experience readable and guided

- `BIJA_calculation.py` — 🧬 Clinical logic layer
  - Pure Python business logic
  - Accepts fertility inputs and applies ART/clinical decision rules
  - Returns a structured recommendation dictionary

- `BIJA_MYSQL.py` — 🗄️ Persistence layer
  - Connects to MySQL
  - Logs anonymized session metadata and recommendation outputs
  - Uses a unified table for auditing and telemetry

This separation keeps the front end, logic layer, and persistence layer independent and easier to validate.

## Repository Structure

```text
Domain-Polyglot-Ecosystem/
├── BIJA_app.py
├── BIJA_calculation.py
├── BIJA_MYSQL.py
├── BIJA.md
├── requirements.txt
├── test_BIJA.py
├── README.md (if present)
└── assets/
    └── screenshots/
```

## Clinical Logic Overview

The decision engine maps patient factors to fertility triage guidance using evidence-informed thresholds and guideline-based logic.

Key pathways include:

- 🧬 Genetic risk
  - Known genetic carrier status may indicate IVF + PGT

- 🚨 Absolute IVF indications
  - blocked tubes
  - diminished ovarian reserve
  - advanced maternal age
  - other clinically significant female-factor indications

- 👨‍🦱 Male factor considerations
  - low sperm count
  - low motility
  - abnormal morphology
  - possible need for IVF + ICSI when indicated

- 🩺 Ovulatory and endocrine dysfunction
  - PCOS-related patterns
  - irregular cycles
  - thyroid dysfunction
  - prolactin elevation
  - possible IUI + ovulation induction pathways when clinically appropriate

The tool does not attempt to replace clinician judgment; it highlights probable next steps for review.

## Visual Interpretation

BIJA includes dynamic visualizations to make fertility trends easier to understand. Charts highlight reference bands for key continuous variables.

- AMH
  - 🔴 low reserve
  - 🟢 normal range
  - 🟡 PCOS risk zone

- FSH
  - 🟡 low
  - 🟢 normal
  - 🔴 high / diminished ovarian reserve risk

- LH
  - 🟡 low
  - 🟢 normal
  - 🔴 high / PCOS risk

These visualizations are designed to support interpretation rather than diagnosis.

## Data and Privacy

BIJA does not store personally identifiable information such as:

- 👤 names
- 📞 phone numbers
- 📬 contact details

It stores anonymized clinical inputs and resulting recommendations for audit or operational analysis where needed. This is intended to support quality review without exposing sensitive patient information.

## Validation and Testing

The clinical engine is protected by automated tests covering key threshold boundaries.

### Current validation coverage

The core calculation engine is validated using a Pytest suite. The current suite contains 20 boundary tests covering standard cases, severe clinical outliers, and exact threshold edges.

Key validation topics include:

- AMH threshold boundaries
- morphology thresholds
- motility thresholds
- PGT logic
- core reproductive decision rules
- severe outlier and stacked-risk scenarios

### Edge-case audits

The suite includes specific edge-case audits to ensure clinical safety:

- **Extreme Outliers:** Validates severe PCOS risk (AMH > 15) and azoospermia (sperm count = 0)
- **Zero-Input Defense:** Ensures the engine handles `0.0` inputs gracefully without throwing a `ZeroDivisionError`
- **Stacked Severe Cases:** Confirms that when both partners have severe factors (e.g., advanced maternal age + severe male factor), the logic correctly recommends combined therapies (IVF + ICSI)

### Validation checklist

- ✅ 20 pytest tests
- ✅ boundary checks for AMH
- ✅ morphology thresholds
- ✅ motility thresholds
- ✅ PGT logic
- ✅ core reproductive decision rules

### Example screenshot areas

<img width="1883" height="722" alt="Pytest validation screenshot" src="https://github.com/user-attachments/assets/b9cab003-c8a0-414e-a054-8b04d6b9b784" />
<img width="1909" height="673" alt="Boundary validation screenshot" src="https://github.com/user-attachments/assets/b6ad42dd-f9b7-4300-a49e-2d88d8d6922d" />

## Clinical Reference Ranges and Thresholds

The BIJA calculation engine uses the following evidence-based thresholds. These reference-oriented values are intended to support interpretation and educational triage, not individualized diagnosis.

### 1. Female Hormonal Panel

| Biomarker | Low | Normal | High | Clinical Implication |
| :--- | :--- | :--- | :--- | :--- |
| **AMH** (ng/mL) | `< 1.0` | `1.0 - 4.0` | `> 4.0` | Low = diminished ovarian reserve (DOR). High = PCOS risk. |
| **FSH** (mIU/mL) | `< 3.5` | `3.5 - 12.5` | `> 12.5` | High = poor ovarian response / DOR. |
| **LH** (mIU/mL) | `< 2.4` | `2.4 - 12.6` | `> 12.6` | High LH often correlates with PCOS. |
| **AFC** (Antral Follicle Count) | `< 5` | `5 - 15+` | - | Low count indicates DOR. |
| **TSH** (mIU/L) | `< 0.4` | `0.4 - 4.0` | `> 4.0` | Thyroid dysfunction impairs ovulation. |
| **Prolactin** (ng/mL) | - | `< 25` | `> 25` | High prolactin inhibits ovulation. |

### 2. Male Panel (WHO 2021 Semen Analysis)

| Biomarker | Abnormal Threshold | Normal Range |
| :--- | :--- | :--- |
| **Sperm Count** (M/mL) | `< 15` | `>= 15` |
| **Total Motility** (%) | `< 40` | `>= 40` |
| **Morphology** (%) | `< 4` | `>= 4` |
| **Semen Volume** (mL) | `< 1.4` | `>= 1.4` |
| **Semen pH** | `< 7.2` | `>= 7.2` |

### 3. Age and Clinical History Triggers

| Trigger | Threshold / Status | Clinical Action |
| :--- | :--- | :--- |
| **Maternal Age** | `>= 35` | Escalate to specialist after **6 months** of trying (instead of 1 year). |
| **Maternal Age** | `>= 40` | Absolute indication for **IVF**. Do not wait. |
| **Tubal Factor** | Blocked tubes = `Yes` | Absolute indication for **IVF** (IUI is impossible). |
| **Genetics** | Known carrier = `Yes` | Indication for **IVF + PGT**. |

### SART Success Probability Data

- **IVF live birth rate per cycle**
  - `<35`: 53.2%
  - `35-37`: 39.9%
  - `38-40`: 26.2%
  - `41-42`: 13.2%
  - `>42`: 4.1%

- **IUI live birth rate per cycle**
  - `<35`: 10-20%
  - `35-37`: 8-15%
  - `38-40`: 5-10%
  - `>40`: <5%

- **Donor egg live birth rate**: 51.3% - 63.6%

## Technology Stack

- 🐍 Language: Python 3
- 🌐 Frontend: Streamlit
- 📊 Visualization: Matplotlib, Pandas
- 🗄️ Database: MySQL
- 🧪 Testing: Pytest, unittest.mock

## Limitations

BIJA is a reference implementation and has important limitations:

- 🚫 It is not medical advice
- 📉 It relies on input lab data and clinical context
- 👶 It is designed for adult populations
- 🧭 It uses reference-based patterns and may not reflect every patient scenario
- 🩺 It should not replace specialist evaluation or care pathways

The system is best viewed as a supportive educational and triage tool, not a definitive clinical engine.

## Reference Guidance

BIJA is informed by commonly cited reproductive medicine and fertility guideline frameworks, including:

- 🌍 WHO fertility and reproductive health guidance for interpreting laboratory values and clinical context
- 🧬 SART (Society for Assisted Reproductive Technology) benchmarks for ART decision support and treatment pathway awareness
- 👩‍⚕️ ACOG and ASRM guidance on infertility evaluation, ovulation induction, and reproductive endocrinology practice standards

These references provide the broader clinical context behind BIJA's triage logic, while the tool itself remains a decision-support educational implementation rather than a formal diagnosis or treatment recommendation.

## Quick Start

1. ⬇️ Clone the repository:

```bash
git clone https://github.com/CodeXSourabhsingh/Domain-Polyglot-Ecosystem.git
cd Domain-Polyglot-Ecosystem
```

2. 📦 Install dependencies:

```bash
pip install -r requirements.txt
```

3. ▶️ Run the app:

```bash
streamlit run BIJA_app.py
```

4. 🧪 Run validation:

```bash
python -m pytest test_BIJA.py -v
```

## Closing

BIJA is a thoughtful and clinically relevant project that combines patient empathy, educational value, and decision support. Its strongest asset is not just the logic—it is the restraint built around it. The tool aims to clarify complexity without overstating certainty, which is especially important in reproductive health.

Built by Sourabh Singh — Forward Deployed Engineer & System Architect.

---

This document is intended to describe the project clearly and accurately. It should be treated as an informational overview, not a clinical standard or individualized medical recommendation.
