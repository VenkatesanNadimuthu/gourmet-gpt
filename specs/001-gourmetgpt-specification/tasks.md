---
description: "Task list for GourmetGPT implementation"
---

# Tasks: GourmetGPT Model & Workflow

**Input**: Design documents from `/specs/001-gourmetgpt-specification/`
**Prerequisites**: plan.md, spec.md

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

---

### US1: Train GourmetGPT Model
1. [P] [US1] Create Colab notebook for model architecture (`notebooks/gourmetgpt_architecture.ipynb`)
2. [P] [US1] Implement GPTModel class in PyTorch
3. [P] [US1] Load pretraining dataset (`Dataset/structured_recipes_pretrain.txt`)
4. [P] [US1] Train model and save checkpoints
5. [P] [US1] Export model artifacts (`model_state_dict.pth`, `tokenizer.json`, `config.json`)

### US2: Evaluate Model Performance
6. [P] [US2] Create Colab notebook for evaluation (`notebooks/gourmetgpt_evaluation.ipynb`)
7. [P] [US2] Compute Perplexity, Ingredient F1, Human Eval metrics
8. [P] [US2] Visualize metrics in Colab
9. [P] [US2] Quantize model weights to 4-bit
10. [P] [US2] Test inference latency on laptop/mobile CPU
11. [P] [US2] Validate offline functionality

### US3: Deploy Model Artifacts
12. [P] [US3] Prepare Streamlit app to load artifacts (`streamlit_app/`)
13. [P] [US3] Integrate model inference in Streamlit
14. [P] [US3] Test recipe generation in offline mode

---

## Tests
- [P] [US1] Unit tests for GPTModel output shapes
- [P] [US2] Automated metric scripts
- [P] [US3] Streamlit app functional tests

---
