# Prompt Injection Detection Using Traditional ML and Transformer Models
### A Comparative Robustness Analysis

![Python](https://img.shields.io/badge/Python-3.12-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange)
![PyTorch](https://img.shields.io/badge/PyTorch-DL-red)
![Transformers](https://img.shields.io/badge/HuggingFace-Transformers-yellow)
![Model](https://img.shields.io/badge/Model-DistilBERT-green)

Detecting and categorising **prompt injection and jailbreak attacks** against large language models — comparing traditional ML against a transformer, with a focus on **adversarial robustness**.

**Author:** Anurag Harishchandra Khadye
**Module:** 6003CMD — Dissertation and Project Artefact
**Degree:** BSc (Hons) Computer Science with Artificial Intelligence, Coventry University
**Supervisors:** Mr. Taylor Ring (1st), Ms. Ushma Mulji (2nd) · **Academic Year:** 2025/26

---

## Overview

This project develops and evaluates NLP classification models for detecting and categorising prompt
injection and jailbreak attacks against LLMs. It compares **traditional ML** (TF-IDF with Logistic
Regression and LinearSVC) against a **transformer** (DistilBERT) across a four-phase experimental design:

1. **Binary classification** — benign prompts vs attacks
2. **Adversarial robustness evaluation** — testing against six adversarial transformation types
3. **Adversarial training recovery** — retraining with augmented data to recover performance
4. **Seven-class multiclass classification** — distinguishing between distinct attack styles

## Results at a Glance

| Phase | Best / notable result |
|-------|------------------------|
| 1 · Binary classification (clean) | **DistilBERT — 0.9940 F1** (LinearSVC 0.9879, LogReg 0.9800) |
| 2 · Adversarial robustness (no retraining) | Baseline LinearSVC macro-F1 falls to **0.9458** on the hardest (semantic) transform; DistilBERT more robust (~0.98–0.995) |
| 3 · Adversarial training recovery | Adversarially-trained LinearSVC recovers to **0.99+ macro-F1** across attack types (0.9928–0.9954) |
| 4 · Seven-class multiclass | **LinearSVC — 0.9009 macro-F1**, ahead of DistilBERT (0.8814) |

**Headline findings:**
- DistilBERT achieved the highest binary detection performance (**0.9940 F1**) on clean data.
- An **adversarially-trained LinearSVC matched or exceeded DistilBERT** on all known attack types — showing that *training-data composition can matter more than model architecture*.
- All models struggled to separate **paraphrased attacks** from direct jailbreaks in the multiclass setting, revealing semantic transformations as a fundamentally harder challenge.
- In the 7-class setting, a **LinearSVC (0.9009 macro-F1) outperformed DistilBERT (0.8814)** — traditional ML stayed competitive with the transformer.

<!-- Add charts here once exported from the notebook into an images/ folder, e.g.:
![Binary F1 comparison](images/f1_comparison.png)
![Multiclass confusion matrix](images/confusion_matrix_multiclass.png)
-->

## What This Project Demonstrates

- **Applied NLP & LLM security** — end-to-end pipeline from ~327k prompts to evaluated classifiers
- **Transformer fine-tuning** — training and evaluating DistilBERT
- **Adversarial ML** — designing a six-transformation attack taxonomy and measuring robustness
- **Rigorous evaluation** — F1/precision–recall framing, adversarial train/test separation, multiclass analysis

## Adversarial Transformation Taxonomy

Six transformations across three categories:

| Category | Transformation | Description |
|----------|----------------|-------------|
| Surface-level | Character substitution | Leet-speak replacements at 18% probability |
| Surface-level | Unicode obfuscation | Cyrillic homoglyph replacements at 15% probability |
| Structural | Indirect injection | Attack wrapped in a summarisation instruction |
| Structural | Narrative roleplay | Attack wrapped in fictional story framing |
| Semantic | Paraphrasing | Complete rewriting via the Claude Sonnet API |
| Semantic | Back-translation | EN→FR→EN round-trip via Helsinki-NLP OpusMT |

## Dataset

The [prompt-injection](https://huggingface.co/datasets/jayavibhav/prompt-injection) dataset (jayavibhav,
HuggingFace): ~327,000 prompts labelled benign or attack, with an approximately balanced 50/50 split.

> Per the assignment brief, datasets from Kaggle or the UCI ML Repository were not used.

## Repository Structure

```
├── Main_Working_Book.ipynb            # Complete experimental notebook
├── prompt_injection_prototype.html    # Static front-end prototype
├── styles.css                         # Prototype styling
└── README.md                          # This file
```

## Tech Stack

`Python 3.12` · `scikit-learn` · `PyTorch` · `HuggingFace Transformers` · `pandas` · `matplotlib` · `seaborn` · `anthropic`

## How to Run

The experiments were built on **Kaggle Notebooks** (2× NVIDIA Tesla T4, 16 GB each):

1. Open the notebook in Kaggle and enable the GPU accelerator (2× T4).
2. Add the required Kaggle secrets:
   - `project-key` — Anthropic API key (for paraphrase generation)
   - `HF_TOKEN` — HuggingFace authentication token
3. Run all cells sequentially.

> Paraphrase and back-translation datasets are pre-generated and loaded from Kaggle datasets; the API
> generation code runs only if the pre-generated files are not found.

## Ethics

This project received ethical clearance (application P191118) through Coventry University's ethics
process. All adversarial prompts were handled in a controlled experimental environment and were **not**
used against live LLM deployments.

## Acknowledgements

Thanks to my supervisor, Mr. Taylor Ring, for his guidance in refining the technical direction of this project.

## License

Completed as assessed coursework at Coventry University; copyright belongs to Coventry University per
institutional policy.
