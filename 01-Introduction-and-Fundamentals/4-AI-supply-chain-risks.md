## 🏗️ Lesson 5: AI Supply Chain & Dependency Risks

### 🎯 Objective

Understand how AI systems inherit risks from third-party dependencies, datasets, and model supply chains — and learn how to secure them through verification, provenance tracking, and dependency auditing.

---

### 🧩 1. What is the AI Supply Chain?

An **AI supply chain** consists of all the components that contribute to building and deploying a GenAI system:

* Datasets (training + fine-tuning)
* Pre-trained models (Hugging Face, OpenAI, etc.)
* Frameworks and libraries (TensorFlow, PyTorch, etc.)
* APIs and plugins
* Deployment pipelines and infrastructure

Each of these components introduces **potential entry points for compromise**.

---

### ⚠️ 2. Common Supply Chain Threats

| Threat Type                 | Description                                                                | Example                                        | Impact                              |
| --------------------------- | -------------------------------------------------------------------------- | ---------------------------------------------- | ----------------------------------- |
| **Dependency Hijacking**    | Malicious versions of open-source packages uploaded to public repositories | Fake `torch-update` PyPI package               | Remote code execution               |
| **Model Backdoors**         | Hidden triggers embedded in pre-trained models                             | Modified weights responding to secret keywords | Data exfiltration or unsafe outputs |
| **Data Provenance Attacks** | Fake or mislabeled data injected into the pipeline                         | Poisoned “face dataset” with manipulated tags  | Bias, misclassification             |
| **Pipeline Tampering**      | CI/CD or model registry compromised                                        | Attacker injects malicious checkpoint          | System-wide compromise              |

---

### 🔍 3. Real-World Example: Dependency Hijacking

In 2023, a malicious PyPI package **“torchtriton”** was uploaded mimicking PyTorch’s dependency.
It contained malicious code that exfiltrated sensitive system info during installation.

```python
# Example: Dangerous import
import torchtriton  # looks legitimate but is malicious
```

🧠 **Functionality & Explanation**
Attackers exploit **name similarity** and **auto-install behavior** in package managers (like pip) to deliver trojanized code.
These attacks often go undetected until runtime.

---

### 🧩 4. Real-World Example: Backdoored AI Models

Attackers upload a tampered checkpoint to a model-sharing platform.

```python
# Unsafe model loading example
from transformers import AutoModel

model = AutoModel.from_pretrained("attacker/model-with-backdoor")
```

🧠 **Explanation:**
The model may include malicious logic or triggers within specific neuron activations.
When a certain input pattern is received, the model produces harmful or manipulated outputs.

---

### 🔐 5. Defensive Strategies

| Layer              | Control Mechanism                  | Example                                |
| ------------------ | ---------------------------------- | -------------------------------------- |
| **Code Layer**     | Dependency auditing                | Use `pip-audit` or `safety check`      |
| **Model Layer**    | Model provenance validation        | Verify SHA256 checksums before loading |
| **Data Layer**     | Dataset origin tracking            | Maintain dataset hash registry         |
| **Pipeline Layer** | CI/CD signing and integrity checks | Use GPG signatures for build artifacts |

---

### 🧠 6. Practical Demo: Dependency Risk Scanner

A simple Python tool that checks installed packages for known vulnerabilities.

```python
import subprocess

def check_vulnerabilities():
    print("🔍 Scanning Python dependencies for known issues...\n")
    result = subprocess.run(["pip", "audit"], capture_output=True, text=True)
    print(result.stdout)

check_vulnerabilities()
```

🧩 **Functionality & Explanation:**
This code uses the `pip audit` command (available from Python 3.10+) to check for known CVEs or vulnerable packages in your environment — an essential part of AI supply chain hygiene.

---

### 💡 7. Key Best Practices

* Use **hash-based verification** for all pre-trained models.
* Always maintain a **dependency lock file** (`requirements.txt` or `poetry.lock`).
* Implement **supply chain transparency** using tools like:

  * [Sigstore](https://www.sigstore.dev/)
  * [in-toto](https://in-toto.io/)
  * [SBOM (Software Bill of Materials)](https://spdx.dev/)

---

### 🚀 8. SEO-Optimized Keywords

`AI Supply Chain Security`, `Model Provenance`, `Dependency Hijacking`, `AI Model Backdoor`, `Dataset Integrity`, `MLOps Security`, `GenAI Risk Management`, `AI Pipeline Hardening`, `Python Package Vulnerability`, `SBOM for AI`.

---

### 📚 9. Key Takeaways

* AI systems are only as secure as their weakest dependency.
* Most compromises occur **before** deployment — at dataset, dependency, or model ingestion stages.
* Always validate, lock, and verify every external component before use.

---

### 🔗 10. Recommended References

* [MITRE ATLAS: AI Supply Chain Risks](https://atlas.mitre.org/)
* [OWASP: Machine Learning Security Top 10](https://owasp.org/www-project-machine-learning-security-top-10/)
* [Google: Secure AI Supply Chain](https://cloud.google.com/security/ai)

