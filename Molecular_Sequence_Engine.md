# Molecular Sequence Engine (MSE): FASTA Analysis, GC Windows, Translation and PAM Scanning

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Tailwind](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![Recharts](https://img.shields.io/badge/Recharts-22B5BF?style=for-the-badge)
![Pytest](https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white)

**Deterministic FASTA analysis: GC content, sliding windows, reverse complement, translation and SpCas9 PAM scanning.**

> **Research use only.** Outputs are calculations and flags for expert review. Nothing here is a clinical decision.

---

## 1. The Problem: Sequence Checks Are Repeated by Hand

Before a wet-lab experiment, a researcher often needs to perform the same basic checks on a DNA sequence:

1. **Composition:** Determine the proportion of G or C bases (GC content) and identify GC-rich and GC-poor regions.
2. **Reading frame:** Determine the protein encoded by the sequence, starting from the first AUG and stopping at the first stop codon.
3. **Strand handling:** Examine the reverse complement and identify motifs on the opposite strand.
4. **Primer estimate:** Calculate an approximate melting temperature for a primer, including a salt correction.

These checks are commonly performed using separate tools or by hand, making results difficult to trace back to the original input. Hand-entered values are a known source of error. In an earlier draft of this project, a hand-typed reverse complement in the PDF was incorrect. The fix was to derive every number directly from program output.

MSE places these checks in one deterministic pipeline, with each step returning a result or a named error.

---

## 2. The Solution: One Engine, Two Interfaces

MSE combines a pure-logic engine with a web interface.

- **Engine (`mse_2.py`):** Pure Python with no network calls. Each stage returns a result or a clearly named error. The engine is the only place where calculations occur.
- **Backend (`app.py`, FastAPI):** Validates requests, runs the engine and returns JSON responses. Login and analysis endpoints are rate limited.
- **Frontend (`App.jsx`, React):** Parses FASTA data in the browser, performs the same checks as the backend, displays charts and provides two download formats: a text report and a JSON file.

### One-Input Pipeline

| Stage | Input | Output |
|---|---|---|
| Clean and validate | FASTA text (one or more records) | DNA only, or a named error |
| GC content | DNA | GC percentage |
| Sliding-window GC | DNA, window size `W` | `N − W + 1` window values |
| Reverse complement | DNA | Opposite strand, 5′ to 3′ |
| Transcription and translation | DNA | mRNA and protein from the first AUG to the first stop codon |
| PAM scan (NGG) | DNA | Positions of every NGG motif, including overlapping sites |
| Primer Tm | Primer, Na⁺ in mM, constant (600 or 675) | Tm and approximate annealing temperature |

Each record in a multi-record FASTA file is analysed separately.

<img width="1875" height="903" alt="MSE application interface" src="https://github.com/user-attachments/assets/b545948d-c00c-4fbd-8f9c-8ac0f329b013" />

<img width="1903" height="894" alt="MSE sequence analysis results" src="https://github.com/user-attachments/assets/3c700267-3536-4f4d-9f61-6be87aa72010" />

<img width="1903" height="894" alt="MSE GC window chart" src="https://github.com/user-attachments/assets/1a5fe05e-0a62-4dcc-9a79-f63c778150f7" />

<img width="1911" height="912" alt="MSE report and download interface" src="https://github.com/user-attachments/assets/de1effba-0b3e-4e63-8f12-e3413c580674" />

---

## 3. Clinical Deep Dive: The Biology and Mathematics

MSE is a research tool. This section explains the science behind each calculated value.

### 3.1 Input Rules

- Whitespace, line breaks and lowercase characters are normalised, allowing standard pasted FASTA text.
- Only `A`, `C`, `G` and `T` are accepted.
- RNA bases (`U`) are rejected with a message requesting DNA.
- Other characters, including `N`, are rejected and identified by a named validation error.

### 3.2 GC Content

\[
GC\% = 100 \times \frac{G + C}{N}
\]

G and C bases pair through three hydrogen bonds, while A and T pair through two. Higher GC content generally indicates greater stability of double-stranded DNA.

### 3.3 Sliding-Window GC

For a window of size `W`, the engine calculates GC percentage at every position. A sequence of length `N` produces:

\[
N - W + 1
\]

window values.

Window size is limited to 3–100 bases and cannot exceed the sequence length.

**Worked example:**  
A 91-base sequence with `W = 5` contains:

\[
91 - 5 + 1 = 87
\]

windows.

### 3.4 Reverse Complement

The sequence is reversed, and each base is complemented:

- `A` ↔ `T`
- `G` ↔ `C`

**Example:**  
The reverse complement of `AAGC` is `GCTT`.

### 3.5 Transcription and Translation

- **Transcription:** `T` bases become `U`, producing the mRNA sequence.
- **Start:** Translation begins at the first `AUG` codon, which encodes methionine.
- **Reading frame:** Codons are read in groups of three bases from that `AUG`.
- **Stop:** Translation stops at the first `UAA`, `UAG` or `UGA` codon. The stop codon is not included in the resulting protein.

MSE has been verified against NCBI: the HBB mRNA sequence (NM_000518.5) translates to a 147-amino-acid protein, matching NP_000509.1.

### 3.6 PAM Sites (SpCas9)

SpCas9 requires an NGG motif adjacent to its target sequence. The engine identifies every position where the base following the target region is `G` and the subsequent base is `G`.

Overlapping NGG matches are included in the count.

### 3.7 Primer Melting Temperature

MSE uses the Marmur–Doty formula with a salt correction:

\[
Tm = 81.5 + 16.6 \times \log_{10}(Na^+) + 0.41 \times GC\% - \frac{k}{L}
\]

- `[Na⁺]` is expressed in molar units. The input is in mM and is divided by 1000.
- `k` is `600` or `675`; the default is `675`.
- `L` is the primer length.

The engine rejects primers shorter than 10 bases because the formula is not reliable below that length. The interface also warns when a primer is shorter than 14 bases.

The estimated annealing temperature is approximately 5 °C below the calculated Tm.

### 3.8 Verified Test Values

| Test file | Length | GC % | Protein | PAM sites | Windows (`W = 5`) |
|---|---|---|---|---|---|
| 1 single record (synthetic) | 91 | 52.75 | MAIVMGR | 8 | 87 |
| 2 two records | 91 and 24 | 52.75 and 54.17 | MAIVMGR and MKVLTAG | 8 and 2 | 87 and 20 |
| 3 Windows line endings | 91 | 52.75 | Same as file 1 | 8 | 87 |
| 4 bad characters | N/A | N/A | Rejected with a named error | N/A | N/A |
| 5 lowercase with spaces | 40 | 52.50 | MAIVMGR*GSKLG | 5 | 36 |
| 6 RNA in a DNA field | N/A | N/A | Rejected with a named error | N/A | N/A |

Expected values are available in `fasta/EXPECTED.txt`. A separate check script reproduces them.

---

## 4. Enterprise Architecture

MSE is a small, carefully structured service rather than a standalone script.

- **Engine isolation:** `mse_2.py` contains pure Python with no network calls and is tested directly.
- **Input validation:** One validation function checks every request before the engine runs. Empty sequences, RNA, invalid characters, out-of-range window sizes and oversized inputs are rejected with named errors. The maximum DNA length is 10,000 bases.
- **Constants allow-list:** The Tm correction constant must be 600 or 675. All other values are rejected.
- **Rate limits:** Login attempts are limited to five per minute, and engine runs to twenty per minute per client.
- **Errors:** Engine errors are logged on the server and returned to the browser as a generic HTTP 500 response, preventing internal details from leaking.
- **CORS:** Only the frontend origin and a local development origin are allowed.
- **Authentication:** The backend contains JWT login code with a demo password. `AUTH_ENABLED = False` disables token validation for the demo. This is a demonstration setting, not a production security design.
- **Frontend:** Built with React and Tailwind CSS. The browser performs the same checks as the backend, allowing mistakes to be identified before an API request is sent.
- **Hosting:** The frontend is hosted on Vercel and the backend on Render. Live links are kept private and shared only upon request.

---

## 5. Extreme Stress Testing

Tests are divided into three categories:

<img width="1912" height="508" alt="Unit and calculation tests" src="https://github.com/user-attachments/assets/6475e4c1-b8b3-4250-a7b4-be7377f3a9d2" />

<img width="1915" height="466" alt="Input and boundary testing" src="https://github.com/user-attachments/assets/ab05179c-315b-4a58-a40d-6ffa46a4f350" />

<img width="1292" height="859" alt="Stress-test results" src="https://github.com/user-attachments/assets/4ef49f84-f998-4002-b9e8-478e86502386" />

---

## 6. Current Limits: Read Before Use

- **Not reviewed by a domain expert.** No output has been signed off by an independent subject-matter expert.
- **Tm is an estimate.** It is not a laboratory protocol. Real PCR performance depends on primer concentration, polymerase and magnesium concentration, none of which are modelled.
- **Translation is not independently cross-checked.** A planned cross-check with Biopython is not yet complete.
- **PAM sites are not guide recommendations.** A PAM site indicates where SpCas9 could potentially bind; it does not demonstrate that a guide will work. Off-target effects, chromatin state and delivery are not modelled.
- **Input is capped** at 10,000 bases in the web application. The engine itself has no such limit.

---

## 7. Regulatory Strategy: Research Tool, Not a Medical Device

- **Research use only.** MSE is a calculator and viewer for sequence data. It makes no diagnosis, treatment recommendation or patient-specific decision.
- **No patient data.** The application accepts sequence text only and does not store uploaded sequences.
- **Deterministic and explainable.** Each number is generated by a named formula documented in the engine and mathematical guide.
- **Clearly labelled limits.** Every estimated or heuristic output is identified as such in the interface and accompanying documentation.
- **Clinical or diagnostic use:** Would require separate design, validation and regulatory review. MSE does not claim to meet that bar.

---

## 8. About the Architect

**Sourabh Singh**

- **Focus:** Verified calculations, honest documentation and tests that validate real data.
- **Contact:** [LinkedIn](https://www.linkedin.com/in/sourabh-singh-7b1249434/)

> **Research use only.** Outputs are calculations and flags for expert review, not clinical decisions.
