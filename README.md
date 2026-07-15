# Using Large Language Models to Support ERP Requirement Classification

Supplementary materials for the article:

**Using Large Language Models to Support ERP Requirement Classification: An Empirical Study**

Authors: Wlodzimierz Wysocki, Przemyslaw Plecka, Aleksander Jarzebowicz, Lukasz Radlinski, and Krzysztof Kowalewski.

## Overview

This repository supports an empirical study on the use of commercial Large Language Models (LLMs) for classifying Enterprise Resource Planning (ERP) requirements. The task is to decide whether a customer requirement can be implemented using standard ERP functionality or whether it requires source-code customization.

The study evaluated 18 LLM configurations on requirements derived from an industrial Comarch ERP XL implementation project. The evaluation used classification metrics, repeated runs, consistency analysis, mixed-effects logistic regression, and non-parametric comparisons.

The original industrial requirement datasets are not included because of confidentiality constraints. The repository provides the instrumentation and supplementary artifacts needed to reproduce the evaluation workflow on other ERP projects or inspect the reported experimental outputs.

## Repository Contents
```text
/
├── data/
├── prompts/
└── scripts/
    └── results_*
```
 - `Using_LLMs_to_Support_ERP_Requirement_Classification_Supplementary Materials.pdf` - additional results for RQ1 and GLMM model definitions for RQ2.

- **data/** - data produced in the study
 - `df_export.csv` - aggregated performance measures in CSV format
 - `df_req_export.csv` -  including requirement-level classification results in CSV format

- **prompts/** - prompt used in LLM assistant
 - `prompt.md` - default Polish prompt used to instruct an LLM assistant to classify ERP requirements
 - `prompt_eng.md` - English translation of the prompt, provided for readers

- **scripts/** - script and synthetic example data files
 - `comparator.ipynb` - Python/Jupyter comparator notebook for evaluating LLM classifications against expert labels
 - `chat_response.json` - example LLM output file using `id`, `classification`, `confidence`, and `justification`
 - `input.json` - example input requirements file using the English schema (`id`, `name`, `description`, optional `area`)
 - `ground_truth.json` - example expert/reference classification file using `id` and `expert_classification`
 - **results\*/**
	   - `report.md` - generated comparator report
	   - `combined_chat_responses.json` - merged LLM response file produced by the comparator


## Classification Task

Each requirement is classified into one of the following categories:

- `STANDARD` - the requirement can be implemented using standard ERP functionality, including configuration or parameterization.
- `CUSTOMIZATION` - the requirement requires source-code modification or customer-specific extension.
- `NO_ANSWER` - the model cannot determine the classification based on the available documentation and knowledge.

The comparator compares the model's `classification` field with the expert `expert_classification` field and computes classification performance against expert annotation.

## Running the Comparator

1. Prepare files in the working directory:

- `ground_truth*.json` - expert/reference classifications with `id` and `expert_classification`.
- `input*.json` - requirements to be analyzed with `id`, `name`, `description`, and optional `area`.
- `chat_response*.json` - LLM-generated classifications with `id`, `classification`, optional `confidence`, optional `source`, and optional `justification`.
- `prompt*.md` - prompt used in the run; by default this resolves to `prompt.md`. `prompt_eng.md` is available only as an English translation/reference version.

2. Open and run:

Jupyter Notebook can be run locally (Jupyter Notebook, JupyterLab, Anaconda, VS Code), in the cloud (Google Colab, Kaggle, Azure ML), on JupyterHub servers, on HPC clusters, and in Docker containers.

```text
comparator.ipynb
```

3. The notebook creates a results directory:

```text
results_YYYY-MM-DD_HH-MM/
```

with:

- `report.md` - human-readable metrics and detailed comparison.
- `combined_chat_responses.json` - merged model responses used in the run.

4. Optional MLflow tracking can be enabled with environment variables:

```bash
export MLFLOW_TRACKING_URI="http://your-mlflow-server"
export MLFLOW_EXPERIMENT_NAME="ERP requirement classification"
```

## Expected JSON Fields

The comparator notebook uses English-only JSON field names. The example JSON files in the repository root have been converted to this schema. Allowed classification values are `STANDARD`, `CUSTOMIZATION`, and `NO_ANSWER`.

Input requirements should contain at least:

```json
{
  "id": "REQ-001",
  "name": "Requirement name",
  "description": "Requirement description"
}
```

Reference classifications should contain:

```json
{
  "id": "REQ-001",
  "expert_classification": "STANDARD"
}
```

LLM responses should contain:

```json
{
  "id": "REQ-001",
  "classification": "STANDARD",
  "confidence": 5,
  "justification": "Short justification"
}
```

The comparator normalizes casing and whitespace in classification labels.

## Metrics

The comparator reports:

- accuracy,
- precision, recall, and F1-score,
- macro and weighted averages,
- Matthews correlation coefficient (MCC),
- confusion matrix,
- metrics by confidence threshold,
- detailed requirement-level comparison,
- missing, invalid, and unmatched rows.

The article uses MCC as a key measure because the task is imbalanced: standard requirements are more frequent than customization requirements.

## Data Availability

The industrial datasets used in the article cannot be published because they contain confidential customer requirements from a real ERP implementation project. The included files should therefore be treated as examples, templates, or local working artifacts unless explicitly stated otherwise.

To reproduce the workflow on another project, replace the example JSON files with your own requirements, expert labels, ERP documentation, prompt, and LLM responses.
