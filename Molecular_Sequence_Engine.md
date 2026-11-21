# Molecular Sequence Engine (MSE): FASTA Analysis, GC Windows, Translation and PAM Scanning

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Tailwind](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![Recharts](https://img.shields.io/badge/Recharts-22B5BF?style=for-the-badge)
![Pytest](https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white)

**Deterministic FASTA analysis: GC content, sliding windows, reverse complement, translation and SpCas9 PAM scanning.**

> Research use only. Outputs are calculations and flags for expert review. Nothing here is a clinical decision.

---

## 1. The Problem: Sequence Checks Are Repeated by Hand

Before a wet-lab experiment, a researcher often needs the same basic checks on a DNA sequence:

1. **Composition:** how much of the sequence is G or C (GC content), and where the GC-rich and GC-poor regions are.
2. **Reading frame:** what protein the sequence encodes, starting from the first AUG and stopping at the first stop codon.
3. **Strand handling:** what the reverse complement looks like, and where the other strand's motifs sit.
4. **Primer estimate:** an approximate melting temperature for a primer, with salt correction.

These checks are usually done in separate tools, or by hand, and the results are hard to trace back to the input. Hand-typed values are a known source of error. In an earlier draft of this project, a hand-typed reverse complement in the PDF was wrong. The fix was to take every number from program output.

MSE puts these checks in one pipeline, with each step returning a result or a named error.

---

## 2. The Solution: One Engine, Two Interfaces

MSE is a pure-logic engine with a web front end.

- **Engine (`mse_2.py`):** pure Python with no network calls. Every stage returns a result or a clear error. The engine is the only place where calculations happen.
- **Backend (`app.py`, FastAPI):** validates the request, runs the engine, and returns JSON. Login and run endpoints are rate limited.
- **Frontend (`App.jsx`, React):** parses FASTA in the browser, runs the same checks as the backend, shows the charts, and offers two downloads (a text report and a JSON file).

The pipeline for one input:

| Stage | Input | Output |
|---|---|---|
| Clean and validate | FASTA text (one or more records) | DNA only, or a named error |
| GC content | DNA | GC % |
| Sliding-window GC | DNA, window size W | N − W + 1 window values |
| Reverse complement | DNA | Opposite strand, 5′ to 3′ |
| Transcription and translation | DNA | mRNA, protein from first AUG to first stop |
| PAM scan (NGG) | DNA | Positions of every NGG, overlaps included |
| Primer Tm | Primer, Na⁺ (mM), constant (600 or 675) | Tm and a rule-of-thumb annealing temperature |

Each record in a multi-record file is analysed separately.
<img width="1875" height="903" alt="Screenshot 2026-11-21 090138" src="https://github.com/user-attachments/assets/b545948d-c00c-4fbd-8f9c-8ac0f329b013" />

<img width="1903" height="894" alt="Screenshot 2026-11-21 090150" src="https://github.com/user-attachments/assets/3c700267-3536-4f4d-9f61-6be87aa72010" />

<img width="1903" height="894" alt="Screenshot 2026-11-21 090150" src="https://github.com/user-attachments/assets/1a5fe05e-0a62-4dcc-9a79-f63c778150f7" />

<img width="1911" height="912" alt="Screenshot 2026-11-21 090210" src="https://github.com/user-attachments/assets/de1effba-0b3e-4e63-8f12-e3413c580674" />


---

## 3. Clinical Deep Dive: The Biology and Mathematics

MSE is a research tool, so this section is about the science behind each number.

### 3.1 Input rules
- Whitespace, line breaks and lowercase are normalised, so pasted FASTA works.
- Only A, C, G and T are accepted. RNA (U) is rejected with a message asking for DNA. Other characters (for example N) are rejected and named.

### 3.2 GC content
GC % = 100 × (G + C) / N

G and C pair with three hydrogen bonds, and A and T with two. Higher GC content generally means more stable double-stranded DNA.

### 3.3 Sliding-window GC
For a window of size W, the engine computes GC % at every position. A sequence of length N gives **N − W + 1** windows. Window size is limited to 3 to 100 and cannot exceed the sequence length.

Worked check: a 91 bp sequence with W = 5 gives 91 − 5 + 1 = 87 windows.

### 3.4 Reverse complement
Reverse the sequence, then replace A↔T and G↔C. Check: the reverse complement of AAGC is GCTT.

### 3.5 Transcription and translation
- **Transcription:** T becomes U, giving the mRNA.
- **Start:** the first AUG (methionine).
- **Reading frame:** codons (groups of three bases) from that AUG.
- **Stop:** the first UAA, UAG or UGA. The stop is not included in the protein.

Verified against NCBI: the HBB mRNA (NM_000518.5) translates to a 147-amino-acid protein, matching NP_000509.1.

### 3.6 PAM sites (SpCas9)
SpCas9 needs an NGG motif next to its target. The engine finds every position where the two bases after an N are G and G, and it counts overlapping sites.

### 3.7 Primer melting temperature
Marmur–Doty formula with salt correction:

**Tm = 81.5 + 16.6 × log₁₀([Na⁺]) + 0.41 × (%GC) − k / L**

- [Na⁺] is in molar units (input in mM, divided by 1000).
- k is 600 or 675 (default 675).
- L is the primer length.

The engine rejects primers shorter than 10 bases, because the formula is not reliable below that length. The interface warns below 14 bases. The annealing temperature shown is about 5 °C below Tm, labelled as a rule of thumb.

### 3.8 Verified test values

| Test file | Length | GC % | Protein | PAM sites | Windows (W = 5) |
|---|---|---|---|---|---|
| 1 single record (synthetic) | 91 | 52.75 | MAIVMGR | 8 | 87 |
| 2 two records | 91 and 24 | 52.75 and 54.17 | MAIVMGR and MKVLTAG | 8 and 2 | 87 and 20 |
| 3 Windows line endings | 91 | 52.75 | same as file 1 | 8 | 87 |
| 4 bad characters | n/a | n/a | rejected with message | n/a | n/a |
| 5 lowercase with spaces | 40 | 52.50 | MAIVMGR*GSKLG | 5 | 36 |
| 6 RNA in a DNA field | n/a | n/a | rejected with message | n/a | n/a |

Expected values are in `fasta/EXPECTED.txt`. A separate check script reproduces them.


---

## 4. Enterprise Architecture

This is a small, careful service, not a script.

- **Engine isolation:** `mse_2.py` is pure Python with no network calls, so it is tested directly.
- **Input validation (the gate):** one function checks every request before the engine runs. Empty sequences, RNA, bad characters, out-of-range windows and oversized inputs are rejected with a named reason. The maximum DNA length is 10,000 bases.
- **Constants allow-list:** the Tm constant must be 600 or 675. Other values are refused.
- **Rate limits:** 5 login attempts per minute and 20 engine runs per minute per client.
- **Errors:** engine errors are logged on the server and returned to the browser as a generic 500, so internal details are not leaked.
- **CORS:** only the frontend origin and a local development origin are allowed.
- **Authentication:** the backend contains JWT login code with a demo password. `AUTH_ENABLED = False` turns the token check off for the demo. This is a demo setting, not a production security design. The repository is private. The secret key must be rotated before the repository is ever made public.
- **Frontend:** React and Tailwind. The browser runs the same checks, so mistakes are shown before a request is sent.
- **Hosting:** frontend on Vercel, backend on Render. Live links are kept private. Share them only on request.

---

## 5. Extreme Stress Testing

Tests are split into three groups.

<img width="1912" height="508" alt="Screenshot 2026-11-20 105931" src="https://github.com/user-attachments/assets/6475e4c1-b8b3-4250-a7b4-be7377f3a9d2" />

<img width="1915" height="466" alt="Screenshot 2026-11-20 113758" src="https://github.com/user-attachments/assets/ab05179c-315b-4a58-a40d-6ffa46a4f350" />

<img width="1292" height="859" alt="WhatsApp Image 2026-11-21 at 9 14 04 AM" src="https://github.com/user-attachments/assets/4ef49f84-f998-4002-b9e8-478e86502386" />


---

## 6. Current Limits (Read Before Use)

- **Not validated against a reviewer.** No output has been signed off by a domain expert.
- **Tm is an estimate.** It is not a protocol. Real PCR depends on primer concentration, polymerase, and magnesium, none of which are modelled.
- **Translation is not yet cross-checked** against an independent tool. A Biopython cross-check is planned.
- **PAM sites are not guides.** A PAM site shows where SpCas9 could bind. It does not show that a guide works, and off-target effects, chromatin state and delivery are not modelled.
- **Input size is capped** at 10,000 bases in the web app. The engine itself has no such cap.

---


## 8. Regulatory Strategy: Research Tool, Not a Medical Device

- **Research use only.** MSE is a calculator and a viewer for sequence data. It makes no diagnosis, no treatment recommendation, and no patient-specific decision.
- **No patient data.** The app accepts sequence text only. It does not store uploaded sequences.
- **Deterministic and explainable.** Each number comes from a named formula, and each formula is in the engine and in the math guide.
- **Labelled limits.** Every output that is an estimate or a heuristic says so in the interface and in the documents.
- **Clinical or diagnostic use:** would require a separate design, validation and regulatory review. This project does not claim to meet that bar.

---

## 9. About the Architect

**Sourabh singh.** 

- **Focus:** verified calculations, honest documentation, and tests that check real data.
- **Contact:** `[https://www.linkedin.com/in/sourabh-singh-7b1249434/]`

Research use only. Outputs are calculations and flags for expert review, not clinical decisions.
