## 🧠 Lesson 11: Adversarial Robustness, Explainability, and Security Auditing in GenAI

### 🎯 Objective
Understand how adversarial attacks target AI models, learn prevention mechanisms, and ensure security through explainability and auditing.

---

## ⚔️ 1. Understanding Adversarial Attacks

Adversarial attacks manipulate model inputs to cause misclassification or unintended behavior.  
They exploit weaknesses in model generalization and overfitting.

| Attack Type | Description | Example |
|--------------|--------------|----------|
| **Evasion Attack** | Alters input to bypass detection | Adding noise to an image to fool a classifier |
| **Poisoning Attack** | Corrupts training data | Injecting mislabeled samples |
| **Model Extraction** | Steals model weights or behavior | Query-based reverse engineering |
| **Model Inversion** | Reconstructs sensitive data | Inferring training images from embeddings |
| **Prompt Injection (GenAI)** | Injects malicious prompts into context | Overwriting system instructions in LLMs |

---

## 🧪 2. Real-World Example

**Case Study:**  
A Vision model trained to detect stop signs was fooled by adding **stickers** on a sign — misclassifying it as a speed limit.  
This demonstrated how small perturbations can have critical real-world consequences in autonomous systems.

---

## 🧰 3. Defending Against Adversarial Attacks

| Defense Type | Method | Description |
|---------------|--------|--------------|
| **Adversarial Training** | Train model with adversarial samples | Improves robustness |
| **Gradient Masking** | Obscure model gradients | Makes attack generation difficult |
| **Input Sanitization** | Filter noisy or manipulated inputs | Image filtering, normalization |
| **Model Ensemble** | Combine multiple models | Reduces single-point failures |
| **Rate Limiting & Monitoring** | Restrict queries to detect abuse | Prevents extraction attacks |

---

### 🧩 Example: Adversarial Noise Detection (Python)

```python
import numpy as np

def detect_adversarial_noise(image, threshold=0.05):
    """Detects adversarial perturbations by checking for pixel variance."""
    variance = np.var(image)
    if variance > threshold:
        print("⚠️ Possible adversarial noise detected.")
    else:
        print("✅ Image appears clean.")

# Example usage
import cv2
img = cv2.imread("sample_image.jpg")
detect_adversarial_noise(img)
````

**Explanation:**
This simple statistical detector flags input images that have unusual noise patterns or distribution shifts.

---

## 🔍 4. Explainability as a Security Tool

Explainability isn’t just ethical — it’s **defensive**.
When you can explain your model’s decisions, you can also **spot manipulations** or **bias-based exploits**.

| Technique                                                  | Tool                    | Use Case                           |
| ---------------------------------------------------------- | ----------------------- | ---------------------------------- |
| **LIME (Local Interpretable Model-agnostic Explanations)** | `lime`                  | Explain model predictions locally  |
| **SHAP (SHapley Additive exPlanations)**                   | `shap`                  | Quantify feature impact            |
| **Grad-CAM (for CNNs)**                                    | `torchcam`, `keras-vis` | Visualize attention regions        |
| **Prompt Logging (LLMs)**                                  | Custom Middleware       | Detect malicious prompt injections |

---

### 🔬 Example: Explain Model Prediction with SHAP

```python
import shap
import xgboost as xgb
from sklearn.datasets import load_iris

X, y = load_iris(return_X_y=True)
model = xgb.XGBClassifier().fit(X, y)

explainer = shap.Explainer(model)
shap_values = explainer(X)

# Display visualization
shap.plots.beeswarm(shap_values)
```

**Explanation:**
SHAP helps visualize which features influenced the model’s prediction most — useful for detecting bias or malicious behavior.

---

## 🧾 5. Security Auditing of GenAI Models

Security auditing ensures ongoing compliance and threat resilience of deployed AI systems.

| Audit Layer                | What to Verify                      | Tools                     |
| -------------------------- | ----------------------------------- | ------------------------- |
| **Data Lineage**           | Trace dataset origin                | DVC, LakeFS               |
| **Model Provenance**       | Verify training and signing history | MLflow, Sigstore          |
| **Access Logs**            | Track inference access              | AWS CloudTrail, ELK Stack |
| **Prompt Logs**            | Capture and analyze user inputs     | Custom Middleware         |
| **Vulnerability Scanning** | Detect library exploits             | pip-audit, Bandit         |

---

### 🧮 Example: Model Signature Verification

```python
import hashlib

def verify_model_signature(model_path, expected_hash):
    """Verify model integrity before deployment."""
    sha256_hash = hashlib.sha256()
    with open(model_path, "rb") as f:
        for byte_block in iter(lambda: f.read(4096), b""):
            sha256_hash.update(byte_block)
    current_hash = sha256_hash.hexdigest()

    if current_hash == expected_hash:
        print("✅ Model signature verified. Safe to deploy.")
    else:
        print("🚫 Model integrity compromised!")
```

**Explanation:**
Verifies that the model file has not been altered since the last trusted build.

---

## 🧠 6. Best Practices for Adversarial Robustness & Auditing

✅ Train with adversarial examples
✅ Implement continuous monitoring
✅ Use explainability frameworks (LIME, SHAP)
✅ Digitally sign models and datasets
✅ Conduct quarterly red-team simulations
✅ Keep an immutable audit log for all training and inference activities

---

## 🔑 Key Takeaways

* **Adversarial robustness** ensures models can resist manipulation.
* **Explainability** enhances model transparency and defense awareness.
* **Security auditing** validates the integrity and trustworthiness of the entire AI lifecycle.

---

## 💡 Pro Tip

> Integrate **Explainable Security Dashboards** that combine SHAP plots, model provenance logs, and anomaly detection — giving you real-time trust visibility over GenAI systems.

---

### 📚 References

* [MITRE ATLAS Framework](https://atlas.mitre.org/)
* [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
* [SHAP Documentation](https://shap.readthedocs.io/en/latest/)
* [LIME GitHub Repo](https://github.com/marcotcr/lime)
* [OWASP ML Security Guide](https://owasp.org/www-project-machine-learning-security-top-10/)

---


