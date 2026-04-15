# CS4650 Project: Mu-SHROOM Cross-Lingual Hallucination Detection
Team project for CS4650 investigating whether hallucination detection models trained on English transfer effectively to other languages.
## Project Goal
We study cross-lingual transfer for hallucination span detection:
- Train/evaluate baseline models on Mu-SHROOM 2025.
- Compare random and XLM-R baselines.
- Build toward English-only vs multilingual fine-tuning analysis.
- Report per-language behavior and transfer limitations.
## Dataset
- **Mu-SHROOM 2025**: [Helsinki-NLP/mu-shroom](https://huggingface.co/datasets/Helsinki-NLP/mu-shroom)
## Metrics
Using the official Mu-SHROOM participant kit scorer:
- **IoU** (character-level span overlap)
- **Correlation** (Spearman correlation with human soft labels)
## Repository Contents
- `CS4650_Project.ipynb` - Main Colab notebook for setup, training, prediction, and scoring
- `scores_random.txt` - Random baseline score output
- `scores_xlmr.txt` - XLM-R baseline score output
- `predictions_random.jsonl` - Random baseline predictions (if included)
- `predictions_xlmr.jsonl` - XLM-R baseline predictions (if included)
## Baseline Results (Current)
| Model | IoU | Correlation |
|---|---:|---:|
| XLM-R | 0.1491 | 0.3753 |
| Random | 0.1225 | -0.0231 |
| Mark-none (sanity) | 0.0400 | 0.0000 |
| Mark-all (sanity) | 0.2887 | 0.0000 |
> Note: Mark-all/Mark-none are sanity checks, not meaningful detection models.
## How to Run (Google Colab)
1. Open `CS4650_Project.ipynb` in Colab.
2. Use GPU runtime (recommended: **L4 GPU**, High-RAM on).
3. Run cells in order from top to bottom.
4. Confirm outputs are generated:
   - `predictions_random.jsonl`, `scores_random.txt`
   - `predictions_xlmr.jsonl`, `scores_xlmr.txt`
5. Review the consolidated results table near the end.
