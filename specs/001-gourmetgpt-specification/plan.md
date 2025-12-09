# Implementation Plan: GourmetGPT Model & Workflow

**Branch**: `001-gourmetgpt-specification` | **Date**: 2025-12-09 | **Spec**: specs/001-gourmetgpt-specification/spec.md
**Input**: Feature specification from `/specs/001-gourmetgpt-specification/spec.md`

## Summary

Implement a domain-specific GPT model for recipe generation, trained and evaluated in Google Colab, with artifacts exported for use in a Streamlit app. All code and data handling must comply with constitution.md.

---

## Phase 1: Model Development
- Design and implement GPT architecture in Colab notebooks.
- Load and validate pretraining and fine-tuning datasets.
- Train model, save checkpoints, and export artifacts (`model_state_dict.pth`, `tokenizer.json`, `config.json`).

## Phase 2: Evaluation
- Create evaluation notebook for metrics.
- Compute Perplexity, Ingredient F1, Human Eval, Model Footprint, Latency, Offline.
- Visualize results in Colab.

## Phase 3: Deployment
- Quantize model weights to 4-bit for edge devices.
- Integrate model artifacts into Streamlit app.
- Test offline recipe generation in Streamlit.

## Artifact Handover & Reproducibility
- Final Colab notebook cell must zip and download all model artifacts.
- Fix random seeds (e.g., `torch.manual_seed(123)`) for all initialization and splits.

---

## Technical Context

**Language/Version**: Python 3.11, PyTorch
**Primary Dependencies**: PyTorch, Jupyter/Colab, Streamlit
**Storage**: Google Drive (Colab), local files for artifacts
**Testing**: Unit tests in Colab, manual and automated metric evaluation
**Target Platform**: Colab (training), Laptop/Mobile CPU (inference)
**Project Type**: Single project, Colab notebooks + Streamlit app
**Performance Goals**: See Success Criteria in spec.md
**Constraints**: All training in Colab, offline inference, artifact handover
**Scale/Scope**: 100+ curated prompts, full recipe dataset

## Constitution Check
- All code in Colab notebooks
- Dataset schemas match constitution
- Metrics and evaluation as specified
- Artifact handover and reproducibility rules followed

## Project Structure

### Documentation (this feature)
- specs/001-gourmetgpt-specification/spec.md
- specs/001-gourmetgpt-specification/plan.md
- specs/001-gourmetgpt-specification/tasks.md

### Source
- notebooks/
- Dataset/
- streamlit_app/

### Artifacts
- model_state_dict.pth
- tokenizer.json
- config.json

### Tests
- Colab notebook cells for unit and integration tests
- Evaluation scripts for metrics

## Dependencies & Assumptions
- Datasets are curated and formatted as specified
- Colab access with A100 GPU
- Streamlit app is external to Colab

## Risks & Mitigations
- Data quality: Validate all datasets for schema and completeness before training. Add automated checks in data loading cells.
- Colab resource limits: Use Colab Pro/Pro+; checkpoint model frequently; monitor GPU usage and plan for restarts.
- Offline inference: Quantize model, export to local device, and run full offline test suite on target hardware.

---

## Constitution Compliance Checklist
- [x] All code in Colab notebooks
- [x] Dataset schemas match constitution
- [x] Metrics and evaluation as specified
- [x] Artifact handover and reproducibility rules followed
- [x] No local GPU training
- [x] Streamlit app loads only exported artifacts

## Next Steps
- Finalize tasks and implementation details
- Begin development in Colab
- Prepare evaluation and deployment scripts
