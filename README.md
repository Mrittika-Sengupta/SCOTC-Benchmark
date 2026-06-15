SCOTC: Software Coverage and Test Completeness Benchmark


A rubric-based framework and dataset for evaluating LLM-generated software test cases across multiple application domains.




Overview

This repository contains the full experimental artifacts for the paper:

"A Rubric-Based Framework for Assessing Software Test Coverage Quality of Large Language Models Across Multiple Application Domains

SCOTC (Software COverage and Test Completeness) is a structured, rubric-driven evaluation framework for assessing the quality of LLM-generated functional test suites derived directly from natural language Software Requirements Specifications (SRS).


Dataset

PropertyDetailsTotal Requirements180Application Domains9Requirements per Domain20LLMs Evaluated11Total Evaluations1,980 (180 × 11)Annotators3 independent expert QA engineersEvaluation DimensionsCompleteness, Relevance, TraceabilityScoring Scale1–5 per dimension (max total: 15)Gold Standard Baseline12.0 (4.0 per dimension)

Application Domains

DomainFunctional ScopeAuthenticationMFA, SSO, session management, token validationE-CommerceCart, inventory, checkout, payment processingBankingFund transfers, ledger updates, overdraft, interestHealthcarePatient records, HIPAA access, telemedicineEducationCourse management, grading, SCORM trackingSocial MediaFeeds, comments, notifications, privacyERP/EnterpriseSupply chain, accounting, multi-tenant systemsIoT/Smart SystemsSensor streams, actuator control, edge processinge-GovernanceIdentity systems, tax filing, public service workflows

Requirement Complexity Tiers

LevelDefinitionSimpleSingle-step deterministic workflows, no branchingMediumConditional logic, validation rules, moderate multi-path flowsComplexMulti-step processes with concurrency, state transitions, or external interactions


Models Evaluated

CategoryModelsCommercialGPT-4o, Claude 3.5 Sonnet, Grok-2, Gemini Pro 1.0, ChatGPT (GPT-3.5), Command R+Open-WeightDeepSeek-V3, Mistral Large 2, Qwen2.5 72BOpen-SourceLlama 3.3 70B, Gemma 2 27B

All models were evaluated under identical zero-shot conditions (temperature τ = 0.2) with no fine-tuning or prompt engineering variations.


SCOTC Evaluation Framework

Scoring Dimensions


Completeness (C) — Coverage of functional actions, boundary conditions, negative cases, and exception handling
Relevance (R) — Contextual alignment with the requirement; penalizes redundant or hallucinated test steps
Traceability (TR) — Degree to which each test step maps directly to explicit requirement statements


Score Formula

Total_Score = Score_C + Score_R + Score_TR        [Range: 3–15]
Gold_Total  = 4.0 + 4.0 + 4.0 = 12.0
CR (%)      = (Total_Score / 12.0) × 100
CR_max      = (15.0 / 12.0) × 100 = 125%


Error Taxonomy (20 Error Types, 7 Categories)

IDCategoryError TypeSeverityET-01OriginalMissing Test CasesHighET-02OriginalIncorrect Test StepsHighET-03OriginalVague Expected ResultsMediumET-04OriginalWrong PreconditionsMediumET-05OriginalDuplicate Test CasesLowET-06BoundaryMissing Boundary CasesHighET-07BoundaryMissing Negative CasesHighET-08StructuralAmbiguous StepsMediumET-09StructuralMissing PreconditionsHighET-10StructuralMissing PostconditionsMediumET-11DataIncomplete Test DataMediumET-12DataIncorrect Expected ResultsHighET-13CoverageSecurity Scenario MissingCriticalET-14CoveragePerformance Scenario MissingHighET-15CoverageUsability Scenario MissingMediumET-16TraceabilityTraceability GapHighET-17TraceabilityRequirement MisinterpretationHighET-18QualityRedundant Test CasesLowET-19QualityIncorrect Priority AssignmentHighET-20StructuralDuplicate ScenariosLow



Explore the Annotation Dataset

The main dataset file is annotations/SCOTC_v3_Final.xlsx. It contains:


Per-requirement scores from all 3 annotators
Consensus final scores for all 11 models
Error taxonomy labels per evaluation row
Domain and complexity tier metadata


Citation

If you use this dataset or framework in your research, please cite:

bibtex@article{sengupta2025scotc,
  title     = {A Rubric-Based Framework for Assessing Software Test Coverage Quality of
               Large Language Models Across Multiple Application Domains},
  author    = {Sen Gupta, Mrittika and Mahmud, Danish and Alam, MD Rasel Ul},
  year      = {2026},
  institution = {North South University; University of the Cumberlands}
}


 License

This dataset and framework are released under the MIT License for open research use.


Acknowledgements

We thank the three expert QA annotators who independently evaluated 1,980 test suite outputs to construct the gold-standard consensus dataset.


