# Chat Response Comparator Report

## Input files

- **Ground truth:** ground_truth.json
- **Prompt:** prompt_eng.md
- **Input:** input.json
- **Chat response files:** chat_response.json
- **Combined responses:** results_2026-07-09_11-14/combined_chat_responses.json

## Data quality

- **Compared samples:** 10
- **Chat responses:** 10
- **Ground truth rows:** 10
- **Invalid chat IDs:** 0
- **Invalid ground truth IDs:** 0
- **Duplicate chat IDs:** none
- **Duplicate ground truth IDs:** none

## Metrics

### Macro Average
- **Precision:** 16.67%
- **Recall:** 33.33%
- **F1:** 22.22%

### Weighted Average
- **Precision:** 25.00%
- **Recall:** 50.00%
- **F1:** 33.33%

### Global
- **Accuracy:** 50.00%
- **MCC:** 0.0000
- **Cohen's Kappa:** 0.0000

## Confusion Matrix

| Expert ↓ \ Model →   |   standard |   customization |   no_answer |
|:---------------------|-----------:|----------------:|------------:|
| standard             |          5 |               0 |           0 |
| customization        |          5 |               0 |           0 |
| no_answer            |          0 |               0 |           0 |

## Metrics per category

| Category | Precision | Recall | F1 | Support |
|----------|-----------|--------|----|---------|
| standard | 50.00% | 100.00% | 66.67% | 5.0 |
| customization | 0.00% | 0.00% | 0.00% | 5.0 |
| no_answer | 0.00% | 0.00% | 0.00% | 0.0 |

## Metrics per confidence

| Confidence >= | Accuracy | MCC | Kappa | Prec (macro) | Recall (macro) | F1 (macro) | Prec (wt) | Recall (wt) | F1 (wt) | N |
|---------------|----------|-----|-------|--------------|----------------|------------|-----------|-------------|---------|---|
| 1 | 50.00% | 0.0000 | 0.0000 | 16.67% | 33.33% | 22.22% | 25.00% | 50.00% | 33.33% | 10 |
| 2 | 50.00% | 0.0000 | 0.0000 | 16.67% | 33.33% | 22.22% | 25.00% | 50.00% | 33.33% | 10 |
| 3 | 50.00% | 0.0000 | 0.0000 | 16.67% | 33.33% | 22.22% | 25.00% | 50.00% | 33.33% | 10 |
| 4 | 50.00% | 0.0000 | 0.0000 | 16.67% | 33.33% | 22.22% | 25.00% | 50.00% | 33.33% | 10 |
| 5 | n/a | n/a | n/a | n/a | n/a | n/a | n/a | n/a | n/a | 0 |

## Missing and invalid rows

| Status | Count |
|--------|-------|

## Match count by confidence

| Confidence | YES | NO | NO_ANSWER | Total |
|------------|-----|----|-----------|-------|
| 4 | 5 | 5 | 0 | 10 |

## Detailed results

| ID | Name | Chat | Expected | Confidence | Match | Status |
|----|------|------|----------|------------|-------|--------|
| 1 | Customer Order Management | STANDARD | STANDARD | 4 | YES | |
| 2 | Purchase Requisition | STANDARD | CUSTOMIZATION | 4 | NO | |
| 3 | Stock Management | STANDARD | STANDARD | 4 | YES | |
| 4 | Accounts Payable | STANDARD | CUSTOMIZATION | 4 | NO | |
| 5 | Accounts Receivable | STANDARD | STANDARD | 4 | YES | |
| 6 | Production Planning | STANDARD | CUSTOMIZATION | 4 | NO | |
| 7 | Preventive Maintenance | STANDARD | STANDARD | 4 | YES | |
| 8 | Employee Management | STANDARD | CUSTOMIZATION | 4 | NO | |
| 9 | Business Intelligence Dashboard | STANDARD | STANDARD | 4 | YES | |
| 10 | Role-Based Access Control | STANDARD | CUSTOMIZATION | 4 | NO | |
