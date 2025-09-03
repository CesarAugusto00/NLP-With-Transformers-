# DistilBERT: Feature Extraction vs Fine-Tuning

## Feature Extraction (Frozen Model)
- **What it is:**  
  - Use DistilBERT to generate "hidden states" (embeddings) for text.
  - The DistilBERT model's weights are **frozen**—they do not change during training.
  - Train a separate classifier (e.g., logistic regression, random forest, or a small neural network) **on top of these embeddings**.
- **How it works:**  
  - Text is passed through DistilBERT.
  - The output from the last hidden layer (often the `[CLS]` token vector) is used as a fixed feature vector for each example.
  - Only the classifier's weights are updated/trained.
- **Pros:**  
  - Fast (less computation, less data needed).
  - No risk of overfitting the large number of parameters in DistilBERT.
- **Cons:**  
  - Performance is usually **worse than fine-tuning**.
  - The representations from DistilBERT are generic, not adapted to your specific classification task.

---

## Fine-Tuning
- **What it is:**  
  - **Train the entire DistilBERT model** (both the transformer body and the classification head) on your specific task.
  - All model weights are updated—DistilBERT is "fine-tuned" to your data.
- **How it works:**  
  - Text is passed through DistilBERT.
  - The output is used by a classification layer.
  - During training, gradients update all weights—so DistilBERT learns to create better features for your dataset.
- **Pros:**  
  - **Much better performance**—the model adapts to your dataset.
  - State-of-the-art results for many NLP tasks.
- **Cons:**  
  - Slower, more memory/computation needed.
  - Slightly higher risk of overfitting if your dataset is small.

---

## Confussion Matrix on Fine-Tunning 

<img width="703" height="636" alt="image" src="https://github.com/user-attachments/assets/bc290338-ae41-4951-9fa1-3196bc0ce1c0" />


---

**Bottom line:**  
- **Feature extraction** is quick and decent for simple or small-scale tasks.
- **Fine-tuning** generally gives much better results, because the model learns what's important for your dataset.

