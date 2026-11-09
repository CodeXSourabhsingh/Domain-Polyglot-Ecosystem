 PGx Precision Dosing Engine

Deterministic pharmacogenomic orchestration for precision dosing and patient protection.

The PGx Engine is a full-stack, distributed clinical platform that merges genetic mutation scanning, pharmacokinetic math, and dynamic dose adjustment into a single decision engine. It is designed to prevent fatal adverse events in standard dosing protocols by enforcing hard clinical boundaries before a drug is prescribed.

The Problem

Standard drug dosing is optimized for population averages and fails dangerously:

· Genetic outliers are missed: A patient may receive a standard dose while carrying a clinically critical mutation (CYP2C9 3/3 or VKORC1 AA) that alters drug metabolism.
· Drug accumulation is ignored: Without adjusting for a "Poor Metabolizer" phenotype, standard doses lead to toxic accumulation.
· Patient safety is an afterthought: Blood work, age, race, and drug interactions are excluded from dosing decisions.
· Black-box systems are not acceptable: Clinical dosing decisions need explainability and deterministic math, not probabilistic guesswork.

The Solution (The Traffic Jam Analogy)

· The Highway (CYP2C9): This enzyme clears the drug. A Poor Metabolizer means the highway is jammed, causing toxicity.
· The Target (VKORC1): This enzyme determines sensitivity. An "AA" genotype means the patient is hyper-sensitive to the drug.
· The Merge: The engine dynamically calculates the exact dose based on the patient's genetics, age, race, height/weight, and DDIs (Amiodarone/Fluconazole). If the math calculates a dose < 2 mg/week, the engine overrides and advises switching to a DOAC (Apixaban).

System Architecture

· Frontend (React + Vite + Tailwind): Interactive clinical dashboard with real-time alerts and standard vs. adjusted dose visual bar charts.
<img width="1600" height="748" alt="image" src="https://github.com/user-attachments/assets/d279eb3b-8ca3-4e2c-bfec-f9bd796af956" />
<img width="1587" height="746" alt="image" src="https://github.com/user-attachments/assets/6fef1e59-aa22-414a-9242-8c2825a0bb09" />
<img width="1600" height="759" alt="image" src="https://github.com/user-attachments/assets/123ed096-65bb-4b1f-b7c7-2217c5d9b714" />

· Backend (Python + FastAPI + Docker): Mathematical engine executing the IWPC regression algorithm.
<img width="1600" height="555" alt="image" src="https://github.com/user-attachments/assets/f738abba-bbc6-4979-a8bb-625992e41659" />
<img width="1885" height="859" alt="Screenshot 2026-11-10 021601" src="https://github.com/user-attachments/assets/8c148c6c-7079-40df-8b8c-d5f031b44a49" />

· Data Layer (Pydantic & Pandas): Strict input validation ensuring "Garbage In, Garbage Out" is blocked at the API gate.
<img width="1915" height="867" alt="Screenshot 2026-11-10 021746" src="https://github.com/user-attachments/assets/62ed9f85-6309-4cbc-82a6-7b62f2488aa0" />

· The Vault (Zero-Data-Retention): Deploys directly into the hospital's AWS VPC. No PHI is stored or transmitted externally.

The 5-Step Pipeline

1. Input Validation: Enforces strict physiological boundaries using Pydantic.
2. Genetics Analysis: Scans CYP2C9 and VKORC1 genotypes.
3. Clinical Modifiers: Checks for hepatic impairment (Child-Pugh) and high-risk DDIs.
4. PK Math (IWPC): Calculates the precise weekly maintenance dose.
5. The Merge: Generates the structured JSON payload, practical pill schedule, and mandatory INR titration warnings.

Testing & Validation

The engine is engineered to stress the exact clinical edge cases where systems fail.

· 200/200 Randomized Stress Tests Passed: 200 synthetic profiles mixing extreme genetics, ages, and DDIs.
  · 84 Extreme Genetic Sensitivities Flagged.
  · 7 Patients Advised to switch to DOACs.
  · 29 Critical Bleeding Events Prevented (Dose = 0 mg).
· Visual Validation: The UI correctly blocks an 85-year-old Asian patient with extreme sensitivity at 0 mg, while clearing a standard patient at 13.87 mg.
ode. I model medical decision logic and ship production-grade platforms.
<img width="1920" height="448" alt="Screenshot 2026-11-09 122812" src="https://github.com/user-attachments/assets/6dfc1103-f341-4cec-8c47-2f35aa76d7b4" />

Final Statement

PGx is not just a dosing calculator. It is a clinical safety engine built to prevent dangerous prescriptions, detect unsafe patients before toxicity occurs, and convert fragmented biomedical signals into a single, defendable decision.
About the Architect

Sourabh Singh
I am a 20-year-old self-taught Systems Architect, 0-to-1 Builder, NEET (dropper) and an 4-0 amateur MMA fighter. I am the bridge between medicine and code. I model medical decision logic and ship production-grade platforms.

Final Statement

PGx is not just a dosing calculator. It is a clinical safety engine built to prevent dangerous prescriptions, detect unsafe patients before toxicity occurs, and convert fragmented biomedical signals into a single, defendable decision.
