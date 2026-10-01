# MedMCR: Multi-Agent Cross-Review for Medical QA Under Noisy Clinical Text

<p align="center">
  <img src="assets/Figure_1.png" alt="MedMCR framework overview" width="820">
</p>

## Overview

Clinical text often contains noise such as typos, OCR errors, and duplicated words, which can degrade LLM performance.
**MedMCR** improves robustness at inference time without retraining: two reasoning agents answer independently, review each other's reasoning, and an adjudicator selects the final answer.

- Reasoning agents: Qwen2.5-32B-Instruct, gemma-3-27b-it
- Adjudicator: gpt-oss-20B
- Dataset: MedQA with six noise types (typo, deletion, duplication, OCR, shuffle, substitution)

## Results

On clean MedQA, MedMCR improved accuracy from **66.1% to 77.1%** (*P* < .001, McNemar test), and the gain was maintained across all six noise types.

## Repository Structure

```
prompts/v1/              # Prompt templates
src/
├── data_processed/      # MedQA preprocessing
├── noise/               # Noise injection (six types)
└── model/
    ├── baseline/        # Zero-shot, CoT
    └── proposed/        # MedMCR pipeline
```

## Usage

```bash
uv sync

# 1. Generate noisy data
python src/noise/typo.py

# 2. Baseline
python src/model/baseline/0shot.py

# 3. MedMCR
python src/model/proposed/run_pipeline.py
```

Place MedQA under `data/raw/medqa/`. Data and results are not included in this repository.

## License

[MIT](LICENSE)
