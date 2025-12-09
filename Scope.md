I am developing a GPT Model from Scratch using Seabstian Rascha Github Repository as guidance. I want to use Github Specification based Development. Write me a Constituation.md to get started on the journey. Constraint: I want all the code to live in Google Colab Notebook as I have access to A100 High RAM CPU and Code to be checked into Github Repository.
I am targeting for a specific use case for Food & Nutrition: Recipe Generation Chatbot Called GourmetGPT. Streamlit App can be created outside of Colab Notbook for App that used the Model Artifacts from Google Colab Notebook.
Metrics Requirement: (Colab Environment with Visualization to support evaluation)
    Domain Accuracy and Coherence: Perplexity (PPL):PPL is measured on the held-out test set as a standard measure of language modeling fluency within the culinary domain.
    Recipe Generation Accuracy (RGA): For a curated set of 100 test prompts, the generated recipes are evaluated using:Ingredient F1-Score: The harmonic mean of precision and recall for generated ingredients against a ground-truth recipe.Instructional Coherence (Human Eval): A panel of threedomain-aware evaluators scores the logical flow, safety, and correctness of generated cooking steps on a 5-point Likert scale.
    Performance and Efficiency Benchmarks: Model Footprint:The final model size (in GB) after 4-bit quantization.
    Inference Latency: Measured as the average time to generate a 256-token response on target edge hardware, specifically,a representative mobile CPU and a laptop CPU, withoutserver-side GPU acceleration.
    Offline Functionality: A binary (Pass/Fail) test verifying the model’s ability to operate fully without an internet connection.
Dataset (Recipe Dataset):
Format: As below
[BOS]
Title: [Recipe Name]
Ingredients: [List]
Instructions: [Steps]
[EOS]