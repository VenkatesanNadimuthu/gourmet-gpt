# GourmetGPT: Project Constitution
**Version:** 1.0
**Guidance:** [LLMs-from-scratch (Sebastian Raschka)](https://github.com/rasbt/LLMs-from-scratch)

## 1. Vision & Mission
To develop a domain-specific Large Language Model (GourmetGPT) capable of generating coherent, safe, and accurate culinary recipes. The model will be built from scratch, pretrained, and instruction fine-tuned within a Google Colab environment, with artifacts deployed to a Streamlit application.

## 2. Architecture & Environment

### Development Environment (The "Factory")
* **Platform:** Google Colab (Pro/Pro+ with A100 GPU).
* **Codebase:** All training and model definition code must reside in `.ipynb` notebooks.
* **Version Control:** Code must be committed to GitHub.
    * *Constraint:* Notebooks must be cleared of heavy outputs before committing, or use tools like `Jupytext` to sync scripts.

### Production Environment (The "Restaurant")
* **App Framework:** Streamlit.
* **Hosting:** Local / Streamlit Cloud (External to Colab).
* **Integration:** The App loads model artifacts (weights/config) generated and saved by the Colab "Factory".

## 3. Development Specification (Phased Approach)

### Phase 1: The Foundation (Reference: Ch 1-4)
* **Objective:** Implement the GPT architecture (Multi-Head Attention, Feed Forward, LayerNorm) using pure PyTorch.
* **Output:** A functional `GPTModel` class.
* **Verification:** Pass unit tests for output tensor shapes (e.g., `[batch, seq_len, vocab_size]`).

### Phase 2: Pretraining (Reference: Ch 5)
* **Objective:** Pretrain the model on a general corpus (or mixed culinary text) to learn language structure.
* **Dataset Schema:**
        - **Format:** Plain text (`.txt`), each recipe as a single block in the following format:
            ```text
            [BOS]
            Title: {Recipe Name}
            Ingredients: {List}
            Instructions: {Steps}
            [EOS]
            ```
        - **File:** One recipe per block/paragraph, separated by newlines or as individual lines.
* **Metrics:** Training Loss, Validation Loss.

### Phase 3: Instruction Fine-Tuning (Reference: Ch 7)
* **Objective:** Adapt the model to the specific "Recipe Generation" format.
* **Dataset Schema:**
        - **Format:** JSON Lines (`.jsonl`), each line is a JSON object:
            ```json
            {"instruction": "<prompt>", "response": "[BOS]\nTitle: ...\nIngredients: ...\nInstructions: ...\n[EOS]"}
            ```
        - **File:** Each `response` field contains the recipe in the same `[BOS]... [EOS]` format as pretraining.
* **Action:** Fine-tune using the curated Recipe Dataset.

### Phase 4: Optimization & Export
* **Objective:** Prepare model for the "edge" (Laptop/Mobile CPU).
* **Quantization:** Convert final weights to 4-bit precision (Int4).
* **Artifacts:** Save `model_state_dict.pth`, `tokenizer.json`, and `config.json`.

## 4. Metrics & Evaluation Requirements

### A. Domain Accuracy
* **Perplexity (PPL):**
    * *Method:* Calculate exponentiated average negative log-likelihood on a held-out culinary test set.
    * *Target:* Lower is better (Benchmark against baseline GPT-2 Small).

### B. Recipe Generation Accuracy (RGA)
* **Test Set:** 100 Curated Food Prompts.
* **Ingredient F1-Score:**
    * Compare generated ingredients list vs. ground truth ingredients.
    * Formula: $2 * (Precision * Recall) / (Precision + Recall)$
* **Instructional Coherence (Human Eval):**
    * *Evaluators:* 3 Domain-Aware Judges.
    * *Scale:* 1-5 Likert Scale (Logical flow, Safety, Correctness).

### C. Performance Benchmarks
* **Model Footprint:** Final size < X GB (target based on parameter count) after 4-bit quantization.
* **Inference Latency:**
    * Target: < Average time for 256 tokens on standard Laptop CPU.
    * Constraint: No Server-Side GPU.
* **Offline Functionality:**
    * Test: Disconnect internet -> Run Streamlit App -> Generate Recipe.
    * Result: Pass/Fail.

## 5. Rules of Engagement
1.  **Colab First:** No local GPU training. All compute-heavy tasks happen in Colab.
2.  **Artifact Handover:** The Colab notebook must end with a cell that zips and downloads the final model artifacts.
3.  **Reproducibility:** Random seeds must be fixed (e.g., `torch.manual_seed(123)`) for all initialization and split operations.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE) | **Last Amended**: 2025-12-09
