# SCOTC: Software Coverage and Test Completeness Benchmark

> A rubric-based framework and dataset for evaluating LLM-generated software test cases across multiple application domains.

---

##  Overview

This repository contains the full experimental artifacts for the paper:

**"A Rubric-Based Framework for Assessing Software Test Coverage Quality of Large Language Models Across Multiple Application Domains"**
*Mrittika Sen Gupta, Danish Mahmud, MD Rasel Ul Alam*
North South University & University of the Cumberlands

SCOTC (**S**oftware **CO**verage and **T**est **C**ompleteness) is a structured, rubric-driven evaluation framework for assessing the quality of LLM-generated functional test suites derived directly from natural language Software Requirements Specifications (SRS).

---

##  Dataset at a Glance

| Property | Details |
|---|---|
| Total Requirements | 180 |
| Application Domains | 9 |
| Requirements per Domain | 20 |
| LLMs Evaluated | 11 |
| Total Evaluations | 1,980 (180 × 11) |
| Annotators | 3 independent expert QA engineers |
| Evaluation Dimensions | Completeness, Relevance, Traceability |
| Scoring Scale | 1–5 per dimension (max total: 15) |
| Gold Standard Baseline | 12.0 (4.0 per dimension) |

### Application Domains

| Domain | Functional Scope |
|---|---|
| Authentication | MFA, SSO, session management, token validation |
| E-Commerce | Cart, inventory, checkout, payment processing |
| Banking | Fund transfers, ledger updates, overdraft, interest |
| Healthcare | Patient records, HIPAA access, telemedicine |
| Education | Course management, grading, SCORM tracking |
| Social Media | Feeds, comments, notifications, privacy |
| ERP/Enterprise | Supply chain, accounting, multi-tenant systems |
| IoT/Smart Systems | Sensor streams, actuator control, edge processing |
| e-Governance | Identity systems, tax filing, public service workflows |

### Requirement Complexity Tiers

| Level | Definition |
|---|---|
| Simple | Single-step deterministic workflows, no branching |
| Medium | Conditional logic, validation rules, moderate multi-path flows |
| Complex | Multi-step processes with concurrency, state transitions, or external interactions |

---

##  Models Evaluated

| Category | Models |
|---|---|
| Commercial | GPT-4o, Claude 3.5 Sonnet, Grok-2, Gemini Pro 1.0, ChatGPT (GPT-3.5), Command R+ |
| Open-Weight | DeepSeek-V3, Mistral Large 2, Qwen2.5 72B |
| Open-Source | Llama 3.3 70B, Gemma 2 27B |

All models were evaluated under identical **zero-shot** conditions (temperature τ = 0.2) with no fine-tuning or prompt engineering variations.

---

##  SCOTC Evaluation Framework

### Scoring Dimensions

- **Completeness (C)** — Coverage of functional actions, boundary conditions, negative cases, and exception handling
- **Relevance (R)** — Contextual alignment with the requirement; penalizes redundant or hallucinated test steps
- **Traceability (TR)** — Degree to which each test step maps directly to explicit requirement statements

### Score Formula

```
Total_Score = Score_C + Score_R + Score_TR        [Range: 3–15]
Gold_Total  = 4.0 + 4.0 + 4.0 = 12.0
CR (%)      = (Total_Score / 12.0) × 100
CR_max      = (15.0 / 12.0) × 100 = 125%
```

---

##  Error Taxonomy (20 Error Types, 7 Categories)

| ID | Category | Error Type | Severity |
|---|---|---|---|
| ET-01 | Original | Missing Test Cases | High |
| ET-02 | Original | Incorrect Test Steps | High |
| ET-03 | Original | Vague Expected Results | Medium |
| ET-04 | Original | Wrong Preconditions | Medium |
| ET-05 | Original | Duplicate Test Cases | Low |
| ET-06 | Boundary | Missing Boundary Cases | High |
| ET-07 | Boundary | Missing Negative Cases | High |
| ET-08 | Structural | Ambiguous Steps | Medium |
| ET-09 | Structural | Missing Preconditions | High |
| ET-10 | Structural | Missing Postconditions | Medium |
| ET-11 | Data | Incomplete Test Data | Medium |
| ET-12 | Data | Incorrect Expected Results | High |
| ET-13 | Coverage | Security Scenario Missing | Critical |
| ET-14 | Coverage | Performance Scenario Missing | High |
| ET-15 | Coverage | Usability Scenario Missing | Medium |
| ET-16 | Traceability | Traceability Gap | High |
| ET-17 | Traceability | Requirement Misinterpretation | High |
| ET-18 | Quality | Redundant Test Cases | Low |
| ET-19 | Quality | Incorrect Priority Assignment | High |
| ET-20 | Structural | Duplicate Scenarios | Low |

---

##  Key Results

### Top Model Rankings (SCOTC Total Score out of 15)

| Rank | Model | Avg C | Avg R | Avg TR | Total | CR (%) |
|---|---|---|---|---|---|---|
| 1 | GPT-4o | 3.706 | 3.644 | 3.500 | 10.850 | 90.4% |
| 2 | Claude 3.5 Sonnet | 3.494 | 3.561 | 3.433 | 10.488 | 87.4% |
| 3 | DeepSeek-V3 | 3.483 | 3.417 | 3.439 | 10.339 | 86.2% |
| 4 | Grok-2 | 3.356 | 3.394 | 3.239 | 9.989 | 83.2% |
| 5 | Llama 3.3 70B | 3.339 | 3.289 | 3.122 | 9.750 | 81.3% |

### Key Findings

- **Non-functional blind spot**: ET-14 (Performance Missing, 2,493 instances) and ET-13 (Security Missing, 2,447 instances) are the most frequent errors across all models.
- **Boundary testing gap**: Missing negative cases (ET-07: 2,325) and boundary cases (ET-06: 2,195) account for a major share of defects.
- **Complexity degradation**: GPT-4o Completeness drops from 3.822 (simple) to 3.547 (complex); Gemini Pro drops from 3.456 to 2.849.
- **Domain sensitivity**: All models perform best on Social Media and Authentication; worst on IoT and e-Governance.

---

##  Getting Started

### Clone the Repository

```bash
git clone https://github.com/<your-username>/SCOTC-Benchmark.git
cd SCOTC-Benchmark
```

### Explore the Annotation Dataset

The main dataset file is `annotations/SCOTC_v3_Final.xlsx`. It contains:
- Per-requirement scores from all 3 annotators
- Consensus final scores for all 11 models
- Error taxonomy labels per evaluation row
- Domain and complexity tier metadata

### Reproduce Coverage Ratios

```python
import pandas as pd

df = pd.read_csv("results/benchmark_rankings.csv")
df["CR"] = (df["Total"] / 12.0) * 100
print(df[["Model", "Total", "CR"]].sort_values("CR", ascending=False))
```

---

##  Citation

If you use this dataset or framework in your research, please cite:

```bibtex
@article{sengupta2025scotc,
  title     = {A Rubric-Based Framework for Assessing Software Test Coverage Quality of
               Large Language Models Across Multiple Application Domains},
  author    = {Sen Gupta, Mrittika and Mahmud, Danish and Alam, MD Rasel Ul},
  year      = {2025},
  institution = {North South University; University of the Cumberlands}
}
```

---

##  License

This dataset and framework are released under the [MIT License](LICENSE) for open research use.

---

##  Acknowledgements

We thank the three expert QA annotators who independently evaluated 1,980 test suite outputs to construct the gold-standard consensus dataset.

---

##  Contact

For questions or collaborations, please open a GitHub Issue or contact the authors via their institutional affiliations.
