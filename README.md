# Prompt Injection Detection Using Traditional ML and Transformer Models: A Comparative Robustness Analysis

**Author:** Anurag Harishchandra Khadye
**Student ID:** 14125645
**Module:** 6003CMD — Dissertation and Project Artefact
**Degree:** BSc Computer Science with Artificial Intelligence
**Institution:** Coventry University
**Supervisor:** Mr. Taylor Ring
**Academic Year:** 2025/26

---

## Overview

This project develops and evaluates NLP-based classification models for detecting and categorising prompt injection and jailbreak attacks against large language models (LLMs). The study compares traditional machine learning classifiers (TF-IDF with Logistic Regression and LinearSVC) against a transformer-based model (DistilBERT) across a four-phase experimental design:

1. **Binary classification** — distinguishing benign prompts from attacks
2. **Adversarial robustness evaluation** — testing models against six adversarial transformation types
3. **Adversarial training recovery** — retraining with augmented data to recover performance
4. **Seven-class multiclass classification** — differentiating between distinct attack styles

## Key Findings

- DistilBERT achieved the highest binary detection performance (0.9940 F1) on clean data
- An adversarially-trained LinearSVC matched or exceeded DistilBERT on all known attack types, demonstrating that training data composition can matter more than model architecture
- All models struggled to distinguish paraphrased attacks from direct jailbreaks in the multiclass setting, revealing semantic transformations as a fundamentally different challenge

## Repository Structure

```
├── main-working-book-prompt-injection-final-book.ipynb   # Complete experimental notebook
├── prompt_injection_prototype.html                        # Static front-end prototype
├── styles.css                                             # Prototype styling
├── Khadye_AH_14125645_2026.docx                          # Dissertation report
└── README.md                                              # This file
```

## Dataset

The study uses the [prompt-injection](https://huggingface.co/datasets/jayavibhav/prompt-injection) dataset published by jayavibhav on HuggingFace, containing approximately 327,000 prompts labelled as benign or attack with an approximately balanced 50/50 class distribution.

**Note:** In accordance with the assignment brief, datasets from Kaggle or the UCI Machine Learning Repository were not used.

## Adversarial Transformation Taxonomy

Six adversarial transformations across three categories were implemented:

| Category | Transformation | Description |
|----------|---------------|-------------|
| Surface-level | Character substitution | Leet-speak replacements at 18% probability |
| Surface-level | Unicode obfuscation | Cyrillic homoglyph replacements at 15% probability |
| Structural | Indirect injection | Attack wrapped in summarisation instruction |
| Structural | Narrative roleplay | Attack wrapped in fictional story framing |
| Semantic | Paraphrasing | Complete rewriting via Claude Sonnet 4.6 API |
| Semantic | Back-translation | EN→FR→EN round-trip via Helsinki-NLP OpusMT |

## Environment

All experiments were conducted on Kaggle Notebooks with the following setup:

- **GPU:** 2× NVIDIA Tesla T4 (16 GB VRAM each)
- **Python:** 3.12
- **Key libraries:** scikit-learn, transformers, torch, pandas, matplotlib, seaborn, anthropic

## How to Run

1. Open the notebook in [Kaggle]([https://www.kaggle.com/](https://www.kaggle.com/code/anuragkhadye/main-working-book-prompt-injection-final-book))
2. Enable GPU accelerator (2× T4)
3. Add the following Kaggle secrets:
   - `project-key` — Anthropic API key (for paraphrase generation)
   - `HF_TOKEN` — HuggingFace authentication token
4. Run all cells sequentially

**Note:** Paraphrase and back-translation datasets are pre-generated and loaded from Kaggle datasets. The API generation code is included but only runs if the pre-generated files are not found.

## Ethics

This project received ethical clearance (application P191118) through Coventry University's ethics system. All adversarial prompts were handled within a controlled experimental environment and were not used to interact with live LLM deployments.

## Acknowledgements

I would like to thank my supervisor, Mr. Taylor Ring, for his guidance in helping refine the technical direction of this project.

## License

This project was completed as part of assessed coursework at Coventry University. Copyright belongs to Coventry University as per institutional policy.
