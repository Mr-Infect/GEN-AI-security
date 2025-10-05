##🔐 Lesson 10: Model Access Control and API Key Security

### 🚀 Objective

Learn how to control access to GenAI models, secure API keys, and prevent unauthorized use or model exfiltration.

---

## ⚙️ 1. Why Access Control Matters in GenAI

AI models — especially LLMs and vision transformers — are high-value assets.
If exposed, they can:

* Leak intellectual property (weights, parameters)
* Enable prompt injection and misuse
* Cause massive API cost abuse

**Example:**
In 2023, several open API endpoints running GPT-3.5 were scraped using automated requests — resulting in financial loss and data exposure.

---

## 🧩 2. Access Control Layers

| Layer                    | Description                            | Example                           |
| ------------------------ | -------------------------------------- | --------------------------------- |
| **User Authentication**  | Verify who is accessing the system     | OAuth2, JWT                       |
| **Authorization**        | Define what actions each user can take | RBAC (Role-Based Access Control)  |
| **API Key Management**   | Secure token-based access              | API keys for OpenAI, Hugging Face |
| **Rate Limiting**        | Prevent abuse through throttling       | 100 requests/min                  |
| **Logging and Auditing** | Track every request                    | CloudWatch, ELK Stack             |

---

## 🧱 3. Principles of Secure Model Access

1. **Principle of Least Privilege**
   Grant the minimum access required to perform a task.
   Example: Data engineer needs read-only, not model-deploy privileges.

2. **Zero-Trust Architecture**
   Always verify — never assume internal traffic is safe.

3. **Rotate Secrets Periodically**
   Rotate API keys every 30–90 days.

4. **Use Environment Variables**
   Never hardcode credentials into code repositories.

---

## 🧰 4. Example: Secure API Key Loading in Python

```python
import os
from dotenv import load_dotenv
import openai

# Load .env file
load_dotenv()

# Retrieve API key securely
api_key = os.getenv("OPENAI_API_KEY")

if not api_key:
    raise ValueError("❌ API key not found! Please set OPENAI_API_KEY in .env")

openai.api_key = api_key
print("✅ API key loaded securely!")
```

**Explanation:**
This ensures that API keys are never exposed in code.
The `.env` file should be listed in `.gitignore` to prevent accidental commits.

---

## 🧮 5. Example: Role-Based Access Control (RBAC)

```python
class AccessControl:
    def __init__(self):
        self.roles = {
            "admin": ["read", "write", "deploy"],
            "analyst": ["read"],
            "developer": ["read", "write"]
        }

    def has_permission(self, role, action):
        return action in self.roles.get(role, [])

# Example usage
ac = AccessControl()
if ac.has_permission("analyst", "deploy"):
    print("Access granted")
else:
    print("🚫 Access denied")
```

**Explanation:**
This ensures that users with the *analyst* role can only read, not deploy, maintaining control over model deployment and updates.

---

## 🧠 6. Common Security Mistakes

| Mistake                   | Risk                 | Prevention                     |
| ------------------------- | -------------------- | ------------------------------ |
| Hardcoding API keys       | Keys exposed in repo | Use `.env` and secret managers |
| Over-permissive IAM roles | Data breach          | Apply least privilege          |
| No rate limiting          | API abuse            | Configure throttling           |
| Shared keys across teams  | No accountability    | Issue per-user keys            |

---

## 🧩 7. Real-World Case Study

**Incident:**
A SaaS startup exposed their OpenAI key in a public GitHub repo. Attackers used it to generate millions of requests overnight, resulting in a **\$22,000 bill**.

**Fix:**
They migrated to AWS Secrets Manager, enforced role-based API access, and implemented request throttling.

---

## 🔑 Key Takeaways

* Treat API keys as **digital gold**.
* Enforce **RBAC** and **Zero Trust**.
* Always rotate, encrypt, and audit keys.
* Never store secrets in public repos.

---

## 🧠 Pro Tip

> Integrate **Vault-based Secret Management** (e.g., HashiCorp Vault, AWS Secrets Manager) for enterprise-grade control over GenAI API credentials.

---

### 📚 References

* [OWASP API Security Top 10](https://owasp.org/API-Security/)
* [HashiCorp Vault Documentation](https://developer.hashicorp.com/vault/docs)
* [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/)
* [OpenAI API Security Best Practices](https://platform.openai.com/docs/guides/security-best-practices)

---
