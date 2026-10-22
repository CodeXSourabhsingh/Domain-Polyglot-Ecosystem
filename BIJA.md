# 🩺 BIJA — Clinical Fertility Triage

BIJA is an evidence-informed clinical decision support tool for reproductive endocrinology and fertility assessment. It helps bridge the gap between raw laboratory values and patient understanding by translating complex fertility data into plain-language triage guidance.

The system is designed to support education and clinical triage, not to replace a physician or provide individualized medical advice

### Visualizing the Data (Patient-Facing UI)
BIJA translates cold lab numbers into clear, empathetic visual zones. 
*The AMH chart visually maps patient results against clinical reference bands (Low Reserve, Normal, PCOS Risk).*

<img width="1379" height="876" alt="Screenshot 2026-10-20 235152" src="https://github.com/user-attachments/assets/b536341d-13f3-46c3-a0f6-0a5205e92d2c" />

### The Philosophy of Bīja

*Bīja* is the Sanskrit word for "seed." It represents the origin, the genetics, and the potential for life. We chose this name because a fertility journey is not a math equation—it is the most vulnerable, human experience a couple can face. BIJA was built to treat patients with the dignity and empathy they deserve, translating cold lab reports into a language of hope and action.

## 💡 Why BIJA Exists

Fertility assessment can be emotionally intense and medically confusing. Patients often receive lab results without enough context to understand what the numbers mean or what their next steps should be.

BIJA addresses this by:
- 🧠 helping users interpret key fertility markers
- ⚠️ highlighting risk patterns based on clinical thresholds
- 🩺 surfacing likely next-step recommendations
- 🤝 separating education from diagnosis
- 👨‍👩‍👧‍👦 incorporating both female and male fertility factors

## 🧭 Design Principles

BIJA is intentionally designed around a human-in-the-loop model:

1. 😌 Empathy first
   Before asking for clinical inputs, the interface acknowledges stress and uncertainty.

2. 🚫 Flagging, not prescribing
   The tool uses reference-based logic and guideline-informed patterns to suggest likely clinical pathways, but it clearly states that it is not a medical diagnosis.

3. 👨‍🦱 Inclusion of male factor fertility
   Male factors are often underrepresented in fertility tools. BIJA explicitly evaluates parameters such as sperm count, motility, morphology, and history of varicocele where relevant.

## ✅ Intended Use

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

## 🏗️ System Architecture

The application is built using a modular three-layer architecture:

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
  - Logs anonymized session metadata and output recommendations
  - Uses a single unified table for auditing and telemetry

This separation helps keep the front end, clinical logic, and data persistence independent and easier to validate.

## 🧪 Clinical Logic Overview

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

## 📈 Visual Interpretation

BIJA includes dynamic visualizations to make fertility trends easier to understand. Charts highlight reference bands for key continuous variables:

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

## 🔒 Data and Privacy

BIJA does not store personally identifiable information such as:
- 👤 names
- 📞 phone numbers
- 📬 contact details

It stores anonymized clinical inputs and resulting recommendations for audit or operational analysis where needed. This is intended to support quality review without exposing sensitive patient information.

## 🧪 Validation and Testing

The clinical engine is protected by automated tests covering key threshold boundaries.

Current validation includes:

<img width="1883" height="722" alt="Screenshot 2026-10-18 144817" src="https://github.com/user-attachments/assets/b9cab003-c8a0-414e-a054-8b04d6b9b784" />
<img width="1909" height="673" alt="Screenshot 2026-10-22 222214" src="https://github.com/user-attachments/assets/b6ad42dd-f9b7-4300-a49e-2d88d8d6922d" />


- ✅ 20 pytest tests
- ✅ boundary checks for AMH
- ✅ morphology thresholds
- ✅ motility thresholds
- ✅ PGT logic
- ✅ core reproductive decision rules

- ## 📊 Clinical Reference Ranges & Thresholds

The BIJA calculation engine uses the following evidence-based thresholds (SART/CDC, WHO 2021). These are the exact numbers powering the decision tree and the visual reference bands.

### 1. Female Hormonal Panel

| Biomarker | Low | Normal | High | Clinical Implication |
| :--- | :--- | :--- | :--- | :--- |
| **AMH** (ng/mL) | `< 1.0` | `1.0 - 4.0` | `> 4.0` | Low = Diminished Ovarian Reserve (DOR). High = PCOS risk. |
| **FSH** (mIU/mL) | `< 3.5` | `3.5 - 12.5` | `> 12.5` | High = Poor ovarian response / DOR. |
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

### 3. Age & Clinical History Triggers

| Trigger | Threshold / Status | Clinical Action |
| :--- | :--- | :--- |
| **Maternal Age** | `>= 35` | Escalate to specialist after **6 months** of trying (instead of 1 year). |
| **Maternal Age** | `>= 40` | Absolute indication for **IVF**. Do not wait. |
| **Tubal Factor** | Blocked tubes = `Yes` | Absolute indication for **IVF** (IUI is impossible). |
| **Genetics** | Known carrier = `Yes` | Indication for **IVF + PGT** (Preimplantation Genetic Testing). |

**The SART Success Probability Data:**
*   **IVF Live Birth Rate (per cycle):** `<35` (53.2%), `35-37` (39.9%), `38-40` (26.2%), `41-42` (13.2%), `>42` (4.1%).
*   **IUI Live Birth Rate (per cycle):** `<35` (10-20%), `35-37` (8-15%), `38-40` (5-10%), `>40` (<5%).
*   **Donor Egg Live Birth Rate:** 51.3% - 63.6%.

Run the test suite with:

```bash
python -m pytest test_BIJA.py -v
```

## 🛠️ Technology Stack

- 🐍 Language: Python 3
- 🌐 Frontend: Streamlit
- 📊 Visualization: Matplotlib, Pandas
- 🗄️ Database: MySQL
- 🧪 Testing: Pytest, unittest.mock

## ⚠️ Limitations

BIJA is a reference implementation and has important limitations:

- 🚫 It is not medical advice
- 📉 It relies on input lab data and clinical context
- 👶 It is designed for adult populations
- 🧭 It uses reference-based patterns and may not reflect every patient scenario
- 🩺 It should not replace specialist evaluation or care pathways

## 📚 Reference Guidance

BIJA is informed by commonly cited reproductive medicine and fertility guideline frameworks, including:

- 🌍 WHO fertility and reproductive health guidance for interpreting laboratory values and clinical context.
- 🧬 SART (Society for Assisted Reproductive Technology) benchmarks for ART decision support and treatment pathway awareness.
- 👩‍⚕️ ACOG and ASRM guidance on infertility evaluation, ovulation induction, and reproductive endocrinology practice standards.

These references provide the broader clinical context behind BIJA's triage logic, while the tool itself remains a decision-support educational implementation rather than a formal diagnosis or treatment protocol.

## 🚀 Quick Start

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

## 🧩 Closing

BIJA is a thoughtful and clinically relevant project that combines patient empathy, educational value, and decision support. Its strongest asset is not just the logic—it is the restraint built around it. The documentation should continue to emphasize that the tool is for triage, education, and informed discussion, not a substitute for care.

Built by Sourabh Singh — Forward Deployed Engineer & System Architect.
