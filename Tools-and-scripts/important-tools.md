##⚙️ Tools, Frameworks & Scripts — GenAI Security C
> Enterprise-grade, actionable catalog of tools you can plug into the **GenAI Security Hub**.
> Each entry: **what it is**, **why it matters for GenAI security**, and a **quick command / usage snippet** so contributors can onboard fast.

This file is intentionally **practical** and **executable** — copy/paste the snippets, run the commands, and integrate the tools into CI/CD, red-teaming, or monitoring pipelines. No fluff. Straight to the point.

---

## Table of Contents

1. [Adversarial Testing & Red-Teaming](#adversarial-testing--red-teaming)
2. [Prompt Security & Guardrails](#prompt-security--guardrails)
3. [Model Robustness & Adversarial Defenses](#model-robustness--adversarial-defenses)
4. [Explainability & Fairness](#explainability--fairness)
5. [Monitoring, Observability & Drift Detection](#monitoring-observability--drift-detection)
6. [MLOps, CI/CD & Reproducibility](#mlops-cicd--reproducibility)
7. [Model Provenance, Signing & Supply-Chain](#model-provenance-signing--supply-chain)
8. [Dependency & Vulnerability Scanning](#dependency--vulnerability-scanning)
9. [Dataset Tools & Data Quality](#dataset-tools--data-quality)
10. [Vector DBs & Retrieval](#vector-dbs--retrieval)
11. [Serving, Deployment & Inference Runtimes](#serving-deployment--inference-runtimes)
12. [Secret Management & Identity](#secret-management--identity)
13. [Evaluation & Benchmarking](#evaluation--benchmarking)
14. [Watermarking, IP & Output Forensics](#watermarking-ip--output-forensics)
15. [Utilities & Misc (logging, visualization, orchestration)](#utilities--misc)

---

## Adversarial Testing & Red-Teaming

1. **TextAttack** — Attack and evaluate NLP models (adversarial examples, attack recipes).

   ```bash
   pip install textattack
   textattack attack --model bert-base-uncased --dataset imdb
   ```
2. **OpenAttack** — Framework for adversarial NLP attacks and defense comparisons.

   ```bash
   pip install openattack
   ```
3. **Adversarial Robustness Toolbox (ART)** — Widely-used library for adversarial attacks & defenses (images, text).

   ```bash
   pip install adversarial-robustness-toolbox
   ```
4. **Foolbox** — Fast evaluation of model robustness against adversarial attacks (vision focus).

   ```bash
   pip install foolbox
   ```
5. **CleverHans** — Research-oriented library for adversarial ML (classic attacks & defenses).

   ```bash
   pip install cleverhans
   ```
6. **TextFooler / DeepWordBug** (toolkits available via TextAttack/OpenAttack) — Proven NLP attack algorithms (use via frameworks above).
7. **OpenAI Evals** — Structured evaluation harness for LLM behavior testing (red-team suites, scenario-based tests).
   *(Use within eval CI to run red-team checks against endpoints.)*

---

## Prompt Security & Guardrails

8. **Guardrails (by guardrails.ai)** — DSL and runtime enforcement layer for safe prompt outputs.

   ```python
   # guardrails config + runtime wraps LLM calls (see docs)
   ```
9. **Lakera Guard / Lakera** — Model monitoring & guardrails platform (policy enforcement, detection).
10. **Rebuff** — Prompt-injection defense and safety middleware (policy enforcement).
11. **PromptShield / PromptGuard / LlamaGuard** — Open-source and community prompt-sanitizer utilities; integrate as pre-filter middleware.
12. **Constitutional AI patterns (Anthropic-inspired)** — Policy-driven prompt templates for steering behavior (implement as server-side system prompts).

```python
# Pseudo: append constitutional rules to system prompt before inference
```

---

## Model Robustness & Adversarial Defenses

13. **Adversarial Training toolkits** (built on ART/TextAttack) — Use to augment training with adversarial examples.
14. **PGD / FGSM implementations** (within ART/Foolbox) — Standard attack/defense primitives for robustness testing.
15. **Robustness Gym** — Systematic framework for evaluating model robustness across perturbations.
16. **TRADES & other robust optimization recipes** — Integrate in training loops (PyTorch/TensorFlow).

---

## Explainability & Fairness

17. **SHAP** — Feature attribution using Shapley values (tabular / text via wrappers).

```bash
pip install shap
```

18. **LIME** — Local interpretable explanations for model predictions.

```bash
pip install lime
```

19. **Captum** — Model interpretability for PyTorch (integrated gradients, gradients × input).

```bash
pip install captum
```

20. **Grad-CAM / TorchCAM** — Visual explanations for CNNs (useful for multimodal models).
21. **AI Fairness 360 (IBM)** — Bias detection and mitigation toolkit.

```bash
pip install aif360
```

22. **Fairlearn** — Metrics and mitigation algorithms for fairness evaluation.

```bash
pip install fairlearn
```

---

## Monitoring, Observability & Drift Detection

23. **Evidently AI** — Data & model drift detection, dashboards and reports.

```bash
pip install evidently
```

24. **Arize AI** — Commercial-grade ML observability and model monitoring platform (drift, explainability).
25. **Prometheus + Grafana** — Metrics pipeline (expose model KPIs, latency, request counts).
26. **OpenTelemetry** — Standardized telemetry (traces, metrics, logs) for model infra.
27. **ELK Stack (Elasticsearch, Logstash, Kibana)** — Centralized logging and forensics; ingest prompt/response logs.
28. **Sentry** — Error monitoring for server-side LLM infra (exceptions, spikes).
29. **Neptune.ai / Weights & Biases** — Experiment tracking + model performance logging (useful for drift baselines).

```bash
pip install wandb
```

---

## MLOps, CI/CD & Reproducibility

30. **MLflow** — Experiment tracking, model registry, reproducible artifacts.

```bash
pip install mlflow
```

31. **DVC (Data Version Control)** — Track datasets, data hashes, and pipelines.

```bash
pip install dvc
```

32. **Airflow / Prefect / Dagster** — Orchestrate ETL, training, and retraining pipelines (use secure runners).
33. **Kubeflow** — End-to-end MLOps on Kubernetes (training, pipelines, serving).
34. **Flyte** — Scalable workflow orchestration with data lineage.
35. **Skaffold / ArgoCD** — GitOps for model deployment and infra drift control.

---

## Model Provenance, Signing & Supply-Chain

36. **Sigstore / Cosign** — Sign model artifacts (containers, wheels, model files) to guarantee provenance.

```bash
cosign sign --key cosign.key my_model.tar.gz
```

37. **in-toto** — Supply-chain metadata and provenance attestation (create verifiable build chains).
38. **SBOM tools (Syft, CycloneDX)** — Generate Software Bill of Materials for your model stack.

```bash
syft packages dir:. -o cyclonedx-json > sbom.json
```

39. **Model Registry (MLflow, Feast, Seldon/ModelDB)** — Store metadata (git sha, data hashes, training env) for validation.

---

## Dependency & Vulnerability Scanning

40. **pip-audit** — Audit Python dependencies for known CVEs.

```bash
pip install pip-audit
pip-audit
```

41. **Safety (pyup.io)** — Scan dependencies for security vulnerabilities.
42. **Bandit** — Static analysis tool to find common Python security issues.

```bash
pip install bandit
bandit -r your_package/
```

43. **Trivy** — Container and artifact vulnerability scanner (also supports IaC).

```bash
brew install aquasecurity/trivy/trivy
trivy image mymodelserver:latest
```

44. **Snyk / Dependabot** — Automated dependency monitoring and fix PRs (integrate with GitHub).

---

## Dataset Tools & Data Quality

45. **Hugging Face Datasets** — Fast dataset loading, streaming, and processing for NLP & multimodal.

```bash
pip install datasets
```

46. **FiftyOne** — Computer vision dataset inspection, visualization and debugging.

```bash
pip install fiftyone
```

47. **Great Expectations** — Data validation and expectation suites for dataset hygiene.

```bash
pip install great_expectations
```

48. **Cleanlab** — Label quality, noise estimation and dataset debugging.

```bash
pip install cleanlab
```

49. **Data Versioning (LakeFS)** — Git-like data lake management for reproducible dataset provenance.

---

## Vector DBs & Retrieval (RAG)

50. **FAISS** — Facebook AI Similarity Search — fast embeddings indexing (local).

```bash
pip install faiss-cpu
```

51. **Milvus** — Open-source vector database (scalable cluster).
52. **Weaviate** — Vector DB with semantic search + modules (context-aware RAG).
53. **Pinecone** — Managed vector DB (SaaS).
54. **Chroma** — Lightweight local vector DB for RAG prototypes.
55. **Annoy (Spotify)** — Fast approximate nearest neighbors (ANN) library.
56. **SentenceTransformers (SBERT)** — Embedding models for semantic indexing.

```bash
pip install sentence-transformers
```

---

## Serving, Deployment & Inference Runtimes

57. **BentoML** — Model packaging & serving with standardized APIs and model signatures.

```bash
pip install bentoml
```

58. **Seldon Core / KServe** — Kubernetes-native model serving with security integrations.
59. **TGI (Text Generation Inference)** — Inference server optimized for LLMs (Hugging Face ecosystem).
60. **vLLM** — High-throughput LLM serving backend (GPU optimization).
61. **Ollama** — Local LLM runtime / manager for on-prem inference and experimentation.
62. **TorchServe** — Serve PyTorch models in production (with model signature validation).

---

## Secret Management & Identity

63. **HashiCorp Vault** — Enterprise secret management (rotate, lease, revoke API keys).
64. **AWS Secrets Manager / AWS KMS** — Managed secret storage and encryption for cloud infra.
65. **Azure Key Vault / GCP Secret Manager** — Cloud-native secret stores — integrate with IAM.
66. **SPIFFE / SPIRE** — Workload identity for service-to-service authentication in microservices.

---

## Evaluation & Benchmarking

67. **HELM & HELM Benchmarks** — Benchmarking LLMs across downstream tasks (use for reproducible evals).
68. **OpenAI Evals** — Create, run and score LLM evals (unit tests for model behavior).
69. **BLEU / ROUGE / METEOR / BERTScore** — Standard NLP metrics (implement in CI).
70. **Evals frameworks: Ecco, Eval Harness, EleutherAI evals** — Multi-scenario testing harnesses for LLMs.

---

## Watermarking, IP & Output Forensics

71. **StegaStamp / Stegano-based tools** — Image watermarking / provenance (research-grade).
72. **Model & Output Fingerprinting (watermarking libs)** — Embed detectable watermarks in generated content for provenance and theft detection.

* Implementation varies per model; use research implementations & vendor APIs.

73. **Forensic logging patterns** — Always log request metadata + deterministic salts for traceability (custom implementation).

---

## Utilities & Misc (logging, visualization, orchestration)

74. **Grafana** — Visualize metrics, dashboards for model KPIs.
75. **PagerDuty / Opsgenie** — Incident management & escalation.
76. **Splunk / SIEM** — Security event management for prompt/response logs and forensic queries.
77. **Jupyter / JupyterLab + nbconvert** — Interactive notebooks for labs and reproducible experiments.
78. **Docker / Podman** — Containerize model infra with signed images.
79. **Terraform / Pulumi** — Infrastructure-as-Code with policy-as-code for secure provisioning.
80. **GitHub Actions / GitLab CI / CircleCI** — CI pipelines for running security checks (pip-audit, bandit, tests).

---

## Integration Guidance — How to assemble this into the GenAI Security Hub

**Suggested folder layout (repo):**

```
/tools
  /adversarial
    README.md
    setup.md
    examples/
  /monitoring
  /provenance
  /scanners
  /rags
  /serve
/playbooks
  red-team-playbook.md
  incident-response.md
/demos
  prompt-injection-demo/
  model-signing-demo/
```

**Quick integration play:**

* Add `tools/README.md` with TL;DR and links to quickstart for each category.
* Provide `docker-compose` for local demos (e.g., Faiss + TGI + BentoML).
* CI job examples:

  * `ci/security-scan.yml` → runs `pip-audit`, `bandit`, `trivy` on container images.
  * `ci/redteam-eval.yml` → runs a small OpenAI Evals suite against staging model endpoint.

---

## Governance & Security Considerations (must-haves)

* **All model artifacts must be signed** (cosign/sigstore) and validated on deployment.
* **API keys / secrets must live in Vault** (or cloud secret manager) — **never** in code or public repos.
* **Automate dependency audits** (pip-audit + Dependabot) and block PR merges when high severity CVEs exist.
* **Log every prompt and response** (hashed) — retain per your compliance matrix, redact PII, and ensure tamper resistance (append-only store).
* **Red-team cadence:** schedule monthly automated red-team tests (TextAttack/OpenAttack) + quarterly human review.

---

## Final Notes & Quickstart Checklist

* [ ] Pick 3 categories to enable first: e.g., (1) Prompt guard + pre-filter, (2) Monitoring + drift, (3) Red-team automation.
* [ ] Add CI gates: pip-audit, bandit, and a smoke-run of an eval.
* [ ] Create a `tools/quickstart.md` with `docker-compose` stacks for local reproducibility.
* [ ] Build one end-to-end demo: ingest dataset → sign model → deploy to BentoML → enable Guardrails → run TextAttack → trigger alert in Grafana/PagerDuty.

---

## SEO Tags (embed in repo pages)

`GenAI Security, LLM Security Tools, Prompt Injection Defenses, Adversarial ML, Model Provenance, MLOps Security, AI Supply Chain, Model Watermarking, Drift Detection, Vector Database, RAG Security`

---

