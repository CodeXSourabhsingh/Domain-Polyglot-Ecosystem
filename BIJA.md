# 🩺 BIJA — Clinical Fertility Triage

**BIJA** is an evidence-based clinical decision support tool for reproductive endocrinology. It bridges the gap between cold lab reports and human anxiety by providing a two-tier system: an **Education Layer** for patients without lab results, and a **Calculation Engine** for those with lab data.

It is built to flag risk and guide next steps, not to replace a physician.

## 🧠 The Philosophy: Human-in-the-Loop

Fertility is a highly sensitive, emotionally loaded domain. Automating medical advice is dangerous. BIJA is built around three strict design principles:

1. **The "Waiting Room" (Empathy Layer):** Before asking for any numbers, the UI acknowledges the user's stress. *"Talking about fertility can be stressful... take a breath."*
2. **Flags, Does Not Prescribe:** The tool uses SART/CDC guidelines to suggest the next clinical step (e.g., IUI vs. IVF), but explicitly states: *"This tool is for triage and education only. It is not a medical prescription."*
3. **Male Factor Inclusion:** Fertility tech often ignores the male side. BIJA explicitly prompts for semen analysis, morphology, motility, and varicocele history, because male factors account for ~50% of cases.


🏗️ The Two-Tab Architecture: Education vs. Calculation

A patient landing on a medical tool is usually in one of two states:

1. "I have a problem and I'm scared, but I don't have my lab results yet."
2. "I just got my lab results, but I don't know what they mean."

If you build a tool that immediately demands lab values, the first type of user will bounce. To solve this, BIJA is built with a two-tier split:

· Tab 1: Patient Education (The "No Data" State): 
  Instead of asking for numbers, this tab asks contextual questions (age, cycle length, medical history). It then generates a personalized action plan, telling the user exactly which tests to ask their doctor for (e.g., "Ask for a Basic Fertility Panel: AMH, Day 3 FSH, Pelvic Ultrasound"). It lowers anxiety and gives the user a roadmap.
  
· Tab 2: Clinical Calculation Engine (The "Data" State):
  Once the user has their lab results, they switch to this tab. It uses the exact SART/CDC clinical thresholds to run the ART decision tree, flagging whether they are a candidate for IUI, IVF, or ICSI.

The Product Philosophy: The mode is a data decision. If the user has no data, the tool educates. If the user has data, the tool calculates. This prevents the user from feeling overwhelmed while ensuring that when they do get their tests done, the tool is waiting to interpret them.

## ⚙️ Architecture

The application is built using a modular, 3-file pipeline architecture to separate the UI, the clinical logic, and the database.

*   **`BIJA_app.py` (UI Layer):** Built with Streamlit. Uses `st.session_state` to ensure that changing a slider does not wipe the patient's results, requiring them to click "Generate Report" again.
*   **`BIJA_calculation.py` (Engine Layer):** Pure Python. No UI, no database. Takes inputs, runs the ART (Assisted Reproductive Technology) decision tree, and returns a dictionary.
*   **`BIJA_MYSQL.py` (Persistence Layer):** Safely connects to MySQL (with a 3-second timeout for cloud compatibility) and logs the session type (Education vs. Calculation) to a single unified table.

## 🧬 Clinical Logic & Decision Tree

The Calculation Engine maps lab values to clinical guidelines (WHO 2021, SART, ACOG).

*   **Genetics:** If a known genetic carrier is detected → **IVF + PGT**.
*   **Absolute IVF Indications:** Blocked tubes, Diminished Ovarian Reserve (AMH < 1.0, FSH > 15, AFC < 5), or advanced maternal age (>= 40) → **Standard IVF**.
*   **Male Factor:** Low sperm count (< 15M/mL), low motility (< 40%), or abnormal morphology (< 4%) → **IVF + ICSI** (Combined approach if female factors are also present).
*   **Ovulatory Dysfunction:** PCOS signs (LH:FSH > 2), irregular cycles, high TSH (> 4.0), or high prolactin (> 25) → **IUI + Ovulation Induction** (only if no absolute IVF indications are present).

## 📊 Visualizations

The dashboard utilizes **Matplotlib** to render dynamic, color-coded reference band charts for the three most critical continuous variables:
*   **AMH (ng/mL):** Red (Low Reserve), Green (Normal), Yellow (PCOS Risk).
*   **FSH (mIU/mL):** Yellow (Low), Green (Normal), Red (High / DOR Risk).
*   **LH (mIU/mL):** Yellow (Low), Green (Normal), Red (High / PCOS Risk).

## 🧪 Validation (Testing)

The core logic is protected by a suite of automated boundary tests. In clinical software, a boundary error isn't just a bug—it's a risk to a patient's family planning.

*   **16 Pytest tests** verify the exact clinical thresholds.
*   Tests cover the precise boundaries for AMH, sperm morphology, motility, and PGT logic.
*   Run the tests with:
    ```bash
    python -m pytest test_BIJA.py -v
    ```

## 🛠️ Tech Stack

*   **Language:** Python 3
*   **Frontend:** Streamlit
*   **Data Visualization:** Matplotlib, Pandas
*   **Database:** MySQL
*   **Testing:** Pytest, unittest.mock

## 🚧 Limitations & Disclaimer

*   **Not Medical Advice:** BIJA provides population averages based on national data. It is a reference implementation for triage and education.
*   **Requires Lab Data:** The Calculation Engine requires the user to have already completed their blood panels and semen analysis.
*   **Adult Ranges Only:** The reference ranges are strictly for adults.
*   **Data Privacy:** The app does not store PII (Personally Identifiable Information) like names or phone numbers. It only logs anonymized lab values and the resulting recommendation for audit purposes.

## 🚀 Run Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/CodeXSourabhsingh/BIJA.git
   cd BIJA
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the app:
   ```bash
   streamlit run BIJA_app.py
   ```

---

Built by Sourabh Singh — Forward Deployed Engineer & System Architect.
