# Kriu-Bench: Screening & Adversarial Robustness Benchmark for Resume Evaluation

Kriu-Bench is an open evaluation benchmark designed to measure how well AI resume screening systems and Applicant Tracking Systems (ATS) evaluate real-world resumes.

Unlike generic keyword search engines or basic LLM evaluators that get easily fooled by buzzwords and AI-generated fluff, this benchmark measures **adversarial robustness**, **format handling**, and **true engineering depth**.

---

## 📊 Benchmark Results Summary (v0.2 Baseline, N = 60)

| Evaluation Category | Kriu AI (v0.2 Baseline) | Expert Talent Recruiter *(Research Baseline)* | Notes & Research Basis |
| :--- | :---: | :---: | :--- |
| **Keyword Stuffing Defense** | **83.3%**<br>*(50 / 60)* | **70.0% – 75.0%**<br>*(42 – 45 / 60)* | Penetration rate against keyword dumps without project context. Recruiters on 6s skims often pass keyword lists. |
| **AI Fluff & JD Mirroring** | **50.0%**<br>*(30 / 60)* | **55.0% – 65.0%**<br>*(33 – 39 / 60)* | Resistance to hollow corporate jargon and JD copy-pasting. Studies show humans struggle to spot AI polish without live interviews. |
| **Execution vs. Exposure** | **50.0%**<br>*(30 / 60)* | **75.0% – 80.0%**<br>*(45 – 48 / 60)* | Distinguishing real commercial execution from tutorial labs/bootcamps. Recruiters excel here by vetting company credibility. |
| **Parser / Format Robustness** | **90.0%**<br>*(54 / 60)* | **98.0% – 100.0%**<br>*(59 – 60 / 60)* | Parsing resumes without failing on non-standard headers (Kriu dropped 6 resumes with 0.0 scores; humans read any format). |

> **Reproducibility Note:** This table is generated directly from raw candidate audit traces in `results/full_summary.json` via `python compute_metrics.py`.

---

## 📁 Repository Structure

```text
├── jds/                              # 3 realistic Job Descriptions (Backend, Data/ML, Sales)
├── resumes/                          # 60 DOCX resumes organized in 12 blind batches of 5
├── source/                           # Master source text and answer key specifications
├── _internal/
│   └── gold_labels.csv               # Ground-truth answer key (blind reference)
├── results/
│   ├── full_summary.json             # Execution outputs for all 60 candidate resumes
│   └── benchmark_summary_table.md    # Generated markdown benchmark table
├── build_bench.py                    # Rebuilds the 60 DOCX files and blind IDs from source
├── run_full_batches.py               # Runs all 12 batches against the Kriu evaluation API
├── compute_metrics.py                # Calculates metrics and outputs the summary leaderboard table
├── manifest.csv                      # Mapping of resume IDs, batches, and job descriptions
├── BENCHMARK.md                      # Complete evaluation methodology & scoring guidelines
└── README.md                         # This file
```

---

## 🚀 Quickstart

### 1. Requirements
* Python 3.10+
* `httpx`, `python-docx`

Install dependencies:
```bash
pip install httpx python-docx
```

### 2. View Benchmark Results Table
To compute metrics and view the leaderboard table from the existing 60-resume run:
```bash
python compute_metrics.py
```

### 3. Run Benchmark Against Custom Summary
You can also run the evaluation against any custom summary JSON:
```bash
python compute_metrics.py path/to/your_summary.json
```

### 4. Re-running the Full Benchmark Suite
To re-run the 60 resumes through the screening pipeline:
```bash
python run_full_batches.py
```
*(Results are cached per batch under `results/batch_XX-N_raw.json` so you do not re-bill or re-run existing batches).*

---

## 📖 Learn More
For detailed documentation on dataset generation, recipe design, and scoring rules, read [BENCHMARK.md](BENCHMARK.md).

---

## 🌐 Platform & Product
* **Product:** [Kriu](https://trykriu.com) — AI Technical Evaluator
* **Playground Console:** [trykriu.com/console.html](https://trykriu.com/console.html)
* **Organization:** [github.com/trykriu](https://github.com/trykriu)

---

## 📄 License
This benchmark dataset, evaluation runner, and scoring scripts are released under the [Apache License 2.0](LICENSE).
