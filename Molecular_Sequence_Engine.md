Write a README.md for a GitHub repository called Molecular-sequence-engine. Use exactly this section order and keep the tone plain and honest. This is a research prototype, not a medical device. Do not use the words "validated," "clinical grade," "perfect," or "production-ready."

Use placeholders where I will paste screenshots, written as: ![Pytest results](docs/pytest.png) and ![Dashboard](docs/dashboard.png).

## 1. Molecular Sequence Engine
One or two sentences. A Python engine that takes a DNA sequence in FASTA format and returns GC content, sliding-window GC, the protein translated from the first start codon, NGG PAM sites on the forward strand, the reverse complement, and an estimated primer melting temperature (Tm) with the working shown.

## 2. The problem
Simple sequence tools often fail on real files: multi-record FASTA, Windows CRLF line endings, lowercase input, spaces inside sequences, and RNA pasted into a DNA field. Overlapping PAM sites are also missed by a plain regex that consumes matched characters.

## 3. The solution
- Cleans input: removes whitespace and line breaks, uppercases, strips CR characters.
- Rejects invalid input with a message that names the bad characters, and rejects U with a message asking for T.
- Blocks sliding windows larger than the sequence.
- Finds overlapping NGG sites with the lookahead regex (?=[ACGT]GG).
- Shows every formula with the working for the displayed numbers.

## 4. The mathematics
Give each formula in a code block, with a one-line explanation:
- GC% = 100 × (G + C) / N
- Number of sliding windows = N − W + 1
- Reverse complement: seq[::-1].translate(str.maketrans("ACGT", "TGCA"))
- Marmur-Doty Tm estimate: Tm = 81.5 + 16.6·log10([Na+]) + 0.41·(%GC) − k/L, where [Na+] is in molar (mM / 1000), L is primer length, and k is 600 or 675. Say the constant must be stated with any result, and that the formula is an estimate.
- Annealing temperature shown as Tm − 5 °C, labelled as a common rule of thumb.

## 5. The biology
Cover briefly and accurately:
- Complementary base pairing, and the 5′→3′ direction of strands.
- Transcription: T is swapped for U in the engine's internal step.
- Codons, the start codon AUG (translation starts at the first AUG), and the stop codons UAA, UAG, UGA (translation ends at the first stop; the stop is not in the protein).
- CRISPR SpCas9 and the NGG PAM. The engine searches the forward strand only and does not compute the 20-nt guide.
- GC content and why it affects melting temperature.
Use this example: the human HBB mRNA (NM_000518.5, 628 bp) translates to the 147-aa protein in NCBI record NP_000509.1, with the match checked letter by letter.

## 6. Tests
Explain that the pytest suite covers:
- GC content, including case-insensitive input
- Marmur-Doty Tm, including the salt and length trends
- Reverse complement, including the involution check
- Transcription and translation, including stop codons and incomplete codons
- Overlapping PAM detection, dense overlaps, and no-site cases
- GC windows, including window size 1 and rejection of windows larger than the sequence
- Rejection of invalid DNA and RNA
- CRLF handling
- Orchestrator smoke test on HBB and rejection of invalid DNA

State the counts exactly: 23 tests in test_mse.py and 10 tests in pytest_mse.py, all passing. Include the screenshot placeholder for the pytest results. Give the run command: python -m pytest -v.

## 7. Architecture
- Frontend: React and Tailwind, deployed on Vercel.
- Backend: FastAPI, deployed on Render. Endpoint: POST /api/run_mse. Input is validated with Pydantic. Rate limit: 20 requests per minute on the analysis endpoint, 5 per minute on login.
- Engine: mse_2.py, pure Python with no external bioinformatics libraries.
- Login uses a JWT. The token check is turned off for the demo with AUTH_ENABLED = False. Say this clearly, and say to turn it back on before any shared or public deployment.
- Downloads: the dashboard can export a plain-text report and the raw JSON, built in the browser.

Include the dashboard screenshot placeholder in this section.

## 8. Run it locally
Give the steps: clone, install Python dependencies, run the backend with uvicorn app:app, and run the frontend. Do not include any secret keys, passwords or live URLs.

## 9. Limitations
- Research prototype, not a medical device. Not clinically validated. Not for diagnosis or treatment decisions.
- Forward strand only for PAM sites. No guide sequence and no off-target scoring.
- Translation uses frame 1 only, from the first AUG. It does not search for open reading frames.
- The Tm formula is an estimate. Its constant must be stated with any result.
- The expected test values come from a script that uses the same rules as the engine, so they are a cross-check, not an independent reference.
- Not yet checked against BioPython or NCBI tools in an automated comparison.
- Authentication is off for the demo.

## 10. Final note
End with this exact sentence: "This is a research prototype, not a medical device."
