# PRISM-X — Universal Genomic Outlier Engine

Deterministic statistical anomaly detection at planetary scale.

## 1. The Problem: The Data Deluge & The AI Hallucination

Modern genomics and clinical research are drowning in data, but legacy systems are failing dangerously:

· The "Black Box" Problem: Research labs use probabilistic Machine Learning models that hallucinate patterns in messy data. If you feed a model garbage (typos, extreme biological anomalies), it gives[...]
· The RAM Bottleneck: Standard Python scripts (using Pandas) crash when trying to process millions of genomic records. You cannot process a 500-million-row clinical trial dataset on a standard web se[...]
· The Data Privacy Trap: Sending massive, highly sensitive patient CSVs to a third-party cloud server violates HIPAA and GDPR, putting the lab at massive legal risk.

## 2. The Solution: The Deterministic Sieve

PRISM-X is not an AI. It is a lightning-fast, deterministic data sieve.

You feed it a raw CSV of genomic data. It calculates the exact mathematical boundaries (Mean ± 2 Standard Deviations) and isolates the statistical outliers. It then groups those anomalies by their ge[...]

· Deterministic Math: No guessing. Just pure, auditable statistics.
· The "Bring Your Own Data" Architecture: The React frontend uploads the file, the FastAPI backend processes it in memory, and returns the outliers. Once the request is complete, the server RAM is wi[...]

## 3. The Breakthrough: Chunking Architecture

Standard servers crash when loading large datasets. PRISM-X uses a proprietary Chunking Architecture.

· Instead of loading a 20GB CSV into RAM, the engine streams the file and processes it in batches of 100 million rows.
· It calculates the math, flushes the RAM, and loads the next 100 million.
· The Result: Infinite scalability. PRISM-X can process a dataset of 10 million or 10 billion rows without ever exceeding 1.5 GB of RAM.

## 4. UI & Visual Validation

The dashboard is designed for clinical researchers and data scientists.

· Drag and Drop: A clean React interface for uploading the raw CSV.
· Instant Visualization: Real-time Recharts bar graphs displaying the exact number of outliers per mutation (e.g., EGFR, KRAS, CFTR, BRCA1).
· One-Click Export: The researcher can instantly download a cleaned CSV containing only the outlier records for further lab investigation.

<img width="1920" height="803" alt="Screenshot 2026-11-14 181657" src="https://github.com/user-attachments/assets/d8697891-5bc7-4251-b6da-8bef98ead900" />

<img width="1920" height="914" alt="Screenshot 2026-11-14 201258" src="https://github.com/user-attachments/assets/b974cfde-f08d-4883-85c8-26aa18bfc570" />

## 5. Extreme Scale: The 2-Billion Patient Stress Test

To prove it is production-grade, we did not just test it on 100 patients. We pushed it to the absolute limit.

· The Benchmark: We generated a synthetic dataset of 2,000,000,000 patient records with 20 different diseases and injected a known 5% statistical outlier rate.
· The Result: PRISM-X processed all 2 billion records, mapped the mutations, and isolated the anomalies in 436 seconds.
· The Speed: 4.5 million patients processed per second.
· The Memory: It never used more than 1.5 GB of RAM.

<img width="1920" height="816" alt="Screenshot 2026-11-14 153725" src="https://github.com/user-attachments/assets/fddc6220-e327-4d24-b3b1-22c4f005b3d3" />

<img width="1920" height="797" alt="Screenshot 2026-11-14 072458" src="https://github.com/user-attachments/assets/9a2bc716-0dbf-4544-8a3f-92a24de174bd" />

## 6. Validation & Edge Case Bouncers

We engineered a hostile Pytest suite to break the engine before a lab could:

· The Pydantic Bouncer: If a lab uploads a CSV missing the biomarker_value column, the API throws a clean 422 Unprocessable Entity error instead of crashing.
· The Zero SD Bouncer: If a dataset has all identical values (Standard Deviation = 0), the engine detects it and prevents a ZeroDivisionError crash.
· The Chaos Fuzzer: 500 randomized, impossible patient profiles (negative ages, missing mutations) were thrown at the engine. Zero crashes.

## 7. Enterprise Architecture & Deployment

PRISM-X is built to be dropped directly into a CRO's AWS VPC.

· The Stack: React + FastAPI + Docker.
· Stateless by Design: We do not use a MySQL database to store the results. The data goes in, the anomalies come out, and the memory is wiped. This is the ultimate HIPAA/GDPR compliance flex.
· The API Gate: The backend is protected by JWT authentication, ensuring only authorized lab technicians can process data.

## 8. The Ecosystem Roadmap: Node 3

PRISM-X is not a standalone tool. It is Node 3 in a massive Clinical Compiler.

· Node 1 (PGx): Precision Warfarin dosing.
· Node 2 (BIJA-X): Reproductive genetic triage.
· Node 3 (PRISM-X): Planetary-scale data cleaning and outlier detection.

## 9. About the Architect

Sourabh Singh — Founder & Lead Systems Architect

self-taught Systems Architect 

field didn't just need more doctors—it needed better data architecture. So I taught myself Python, FastAPI, and React.

I am not just a developer; I am a one-man clinical engineering department. I identify the data bottleneck, model the mathematical logic, and build the pipelines that turn massive, messy datasets into [...]

## Final Statement
PRISM-X is not a black-box AI. It is a mathematical sieve. It converts millions of lines of messy genomic data into a clean, actionable map of biological anomalies in seconds.

---

## 🚨 LEGAL DISCLAIMER & TERMS OF USE

Not a Medical Device: The PRISM-X Engine is a software prototype designed to demonstrate the capabilities of deterministic statistical analysis. It is not a medical device, does not provide medica[...]

No Substitute for Clinical Judgment: The outputs generated by this engine are for informational and research purposes only. A qualified researcher or clinician must review all outputs and independe[...]

Regulatory Status: This software has not been cleared or approved by the US Food and Drug Administration (FDA) or any equivalent international regulatory authority (e.g., EMA, MHRA). It is curren[...]

Limitation of Liability: The Architect (Sourabh Singh) assumes no liability for any clinical outcomes, adverse events, or damages arising from the use of, or reliance upon, the information or sof[...]

Data Privacy: The deployment architecture described herein utilizes a "Zero-Data-Retention" (Bring Your Own Data) model. The developer does not collect, store, or transmit any Protected Health In[...]
