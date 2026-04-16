# CS 4650 - Cross-lingual Hallucination Detection (Mu-SHROOM)

**Team:** Zohair Hussain, Nabeel Arshad, Shreya Devaraju, Vinayak Ramasubramanian  
**Institution:** Georgia Tech · CS 4650

## Problem & motivation

Large language models **hallucinate**-and they do so **unevenly across languages**. Prior work suggests that accuracy and reliability differ between high- and low-resource settings, and that **cross-lingual transfer** often degrades with **linguistic distance** from a source language, including differences in **script** and **tokenization**.

This project asks whether **hallucination detectors** behave the same way: if we build a span-level detector using **only English** supervision, does it **generalize** when we apply it to **other languages**, or does it systematically **miss** failures that are more **language-specific** (including subtler or “cultural” errors in the broad sense)? We study this in a **controlled benchmark** with gold spans and human soft labels, not only with ad hoc generation.

## Research questions

- Does an **English-only** hallucination detector **transfer** to other languages, or does performance **drop**, and by how much **per language**?
- When it drops, is the gap related to **script**, **tokenization**, or **distance from English** more generally?
- How does that English-only detector compare to the **same architecture fine-tuned on the target language** on identical test conditions?
- **Which languages** are hardest for English-only transfer relative to a **language-specific** model?

## Approach (methodology)

We adopt a **cross-lingual transfer** setup on **Mu-SHROOM**:

1. **Token-level classification** over LLM answers: label tokens (or align spans) as **hallucinated vs not**, using a multilingual encoder (**XLM-RoBERTa-Large**) so one family of models can be compared fairly across settings.
2. **English-only training:** fine-tune on **English** labeled data, then **evaluate on other languages** (e.g. Spanish, Hindi, Finnish, and additional Mu-SHROOM languages as capacity allows).
3. **Target-language training:** fine-tune **separate models on each target language** (or language groupings as appropriate) using the same architecture and task formulation.
4. **Head-to-head comparison:** same splits and metrics for **English-only → target lang** vs **target-only** models, plus analysis of **where** the gap is largest.

**Baselines** are one piece of the evaluation-not the whole project: we include the task’s **random** and **XLM-R (organizer)** baselines so our main models are interpretable against **standard reference points**, and we report **development and test** performance as required by the benchmark and the course.

## Dataset

**Mu-SHROOM 2025** provides **multilingual** labeled data with **train, validation, and test** splits and many languages (e.g. 10+ in the core shared-task setup; extended coverage appears in the full Hugging Face release). We use the official release for training, tuning, and final evaluation.

| Resource | Link |
|----------|------|
| Dataset (Hugging Face) | [Helsinki-NLP/mu-shroom](https://huggingface.co/datasets/Helsinki-NLP/mu-shroom) |
| Task materials & participant kit (scorer, baselines) | [Helsinki-NLP/mu-shroom](https://github.com/Helsinki-NLP/mu-shroom) |

## Evaluation & analysis

**Metrics (official Mu-SHROOM scorer).**

- **Character-level IoU** between predicted and gold hallucination spans.
- **Correlation** between predicted and human **soft-label** (probability) annotations over spans.

We report metrics **per language** so we can see which languages **benefit most or least** from English-only transfer versus **target-language** fine-tuning. The **final report** ties numbers to **discussion**: failure modes, languages with large script/tokenization differences from English, and how results relate to **prior work** on multilingual hallucination and cross-lingual NLP (see the project proposal and report for citations).




