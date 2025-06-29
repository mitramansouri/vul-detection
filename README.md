# Vulnerability Detection with Code Language Models

## Overview

This project presents a pipeline for detecting software vulnerabilities in C/C++ code at both the function and line levels using transformer-based language models. Leveraging the CodeBERT architecture and self-attention mechanisms, we fine-tune a sequence classification model to flag vulnerable functions (coarse-grained) and localize specific vulnerable lines (fine-grained) within those functions.

**Key Contributions:**

* **Function-Level Detection:** Fine-tuned CodeBERT (RobertaForSequenceClassification) on the Big-Vul dataset to classify functions as vulnerable or safe.
* **Line-Level Localization:** Extracted and aggregated self-attention scores to rank lines by vulnerability likelihood, reporting Top‑K precision/recall and false-alarm metrics.
* **Hyperparameter Optimization:** Automated tuning of learning rate, batch size, weight decay, and epochs using Optuna (TPESampler + MedianPruner).

## Data Preparation

* Download the [Big-Vul dataset](https://github.com/ZeoVan/MSR_20_Code_vulnerability_CSV_Dataset)

## Results

* **Function-Level Detection** (held-out test set):

  * Accuracy: 0.983
  * Precision: 0.895
  * Recall: 0.739
  * F1‑Score: 0.810
  * MCC: 0.805

* **Line-Level Localization** (Top‑10 ranking):

  | Metric           | Value |
  | ---------------- | ----- |
  | Top-10 Precision | 0.632 |
  | Top-10 Recall    | 0.552 |
  | IFA (Average)    | 8.51  |
  | IFA (Median)     | 5.50  |

Refer to the notebook for full validation curves and per-epoch metrics.

## Hyperparameter Optimization

* **Library:** [Optuna](https://optuna.org/)
* **Search Space:**

  * Learning rate: \[2e-6, 1e-5, 2e-5, 3e-5, 5e-5, 2e-4]
  * Batch size: \[8, 16, 32]
  * Weight decay: \[0.0, 0.01, 0.1]
  * Epochs: \[2–8]
* **Best Configuration:**

  * LR = 2e-5, Batch = 16, Weight Decay = 0.1, Epochs = 10

## Dependencies

* Python >= 3.8
* torch
* transformers
* optuna
* scikit-learn
* pandas
* matplotlib`

## Contributing

This was a university project for LLM course, colaborated with @Mina-Gharenazi and @rokkovach.

