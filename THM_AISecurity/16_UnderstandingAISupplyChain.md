# Understanding AI Supply Chains - Room Write-Up

**Room Link:** [TryHackMe - Understanding AI Supply Chains](https://tryhackme.com/room/understanding-ai-supplychains)  
**Category:** AI / LLM Security  
**Difficulty:** Easy  
**Focus:** AI Supply Chain Architecture, Artifact Serialization Risks, and Attack Layers  
**Framework Alignment:** OWASP LLM03 (Supply Chain Vulnerabilities) | MITRE ATLAS AML.T0010 (ML Supply Chain Compromise)

---

## 1. Executive Summary & Room Objectives

The **Understanding AI Supply Chains** room breaks down how modern artificial intelligence and machine learning pipelines source, integrate, and deploy external assets. Modern AI systems rarely start from scratch; instead, they inherit dependencies across training data, base model weights, specialized frameworks, and runtime libraries. 

While traditional software supply chain attacks (such as the SolarWinds compromise) focus on tampering with the build pipeline or source code, AI supply chains introduce domain-specific attack vectors. These include executable weight serialization, dataset poisoning, unvetted runtime adapters, and dependency confusion targeting ML-specific packages.

### Key Objectives
* Differentiate between classic software supply chain threats and AI-specific attack surfaces.
* Map and classify vulnerabilities across the **Four Attack Layers** (Model, Dependency, Data, Infrastructure).
* Analyze deserialization threats (e.g., Python `pickle`) versus secure weight formats (e.g., `SafeTensors`).
* Understand operational trust boundaries between self-hosted local inference and hosted Model-as-a-Service (MaaS) APIs.

---

## 2. Core Concepts & Technical Architecture

### Traditional vs. AI Supply Chain

* **Traditional Supply Chain:** Relies on third-party libraries, package registries, and build servers. Attackers target the code repositories or the build process directly (e.g., SolarWinds inserting malicious build-time scripts).
* **AI Supply Chain:** Inherits all traditional software risks and adds opaque, high-dimensional artifacts:
  * **Serialized Weights:** Binary files containing learned parameters that can embed hidden executable instructions.
  * **Training Corpora:** Massive, unvetted datasets scraped from external sources or public repositories.
  * **Transitive Dependencies:** Installing a core framework like `torch` silently pulls in unlisted sub-packages (e.g., `filelock`), expanding the attack surface.

```
Classic Software:  [Source Code] ──> [Build Pipeline (Injected)] ──> [Executable]
AI Pipeline:       [Untrusted Data] ──> [Pretrained Weights (.pt/.pkl)] ──> [Framework/Transitive Libs] ──> [Inference Engine]
```

### Four Key Components of an AI Supply Chain

1. **Datasets:** Raw text, image, audio, or tabular data used for pre-training, fine-tuning, or alignment.
2. **Dependencies:** Direct and transitive software packages required to load and execute the model (e.g., `transformers`, `torch`, `filelock`, `numpy`).
3. **Frameworks:** Core execution runtimes, training engines, and serving platforms (e.g., PyTorch, TensorFlow, ONNX, vLLM).
4. **Models:** Learned parameter weights, architecture definitions, and modular checkpoints (e.g., base weights, LoRA adapters, quantized GGUF binaries).

### Model Consumption Models & Trust Boundaries

* **Local Models (Self-Hosted):**
  * *Standard Local Format:* **GGUF** (via `llama.cpp` for CPU/GPU quantization) and **SafeTensors** (Hugging Face standard).
  * *Trust Mechanism:* The user downloads, inspects, and executes model weights locally. The host assumes all security liability if weights contain executable payloads or corrupt memory.
* **API / Hosted Models (Model-as-a-Service):**
  * *Standard Providers:* Centralized cloud APIs (OpenAI, Anthropic, AWS Bedrock).
  * *Trust Mechanism:* The user sends prompts and receives outputs without access to underlying weights, training pipelines, or server configurations. Trust is delegated entirely to the external provider.

---

## 3. The Four Attack Layers

| Layer | Attack Vectors & Techniques | Real-World Incident / Mechanism | Primary Defenses |
| :--- | :--- | :--- | :--- |
| **Model Layer** | Arbitrary Code Execution via deserialization, weight tampering, hidden backdoor triggers. | Legacy PyTorch `.pt`/`.bin` files using Python's `pickle` library to trigger reverse shells upon loading. | Enforce **SafeTensors** to eliminate code execution; load PyTorch with `weights_only=True`; verify cryptographic SHA-256 hashes. |
| **Dependency Layer** | Typosquatting, dependency confusion, malicious transitive dependencies. | The `torchtriton` supply-chain attack on PyPI, where a malicious package mirrored an internal PyTorch dependency. | Maintain strict dependency lockfiles; use private internal mirrors (Nexus, Artifactory); run automated Software Composition Analysis (SCA). |
| **Data Layer** | Training set poisoning, backdoored labels, compromised RAG knowledge bases. | Modifying as little as **0.1%** of a training dataset to inject a latent backdoor while preserving standard benchmark performance. | Track data provenance and lineage; enforce dataset hashing; run out-of-distribution anomaly detection during preprocessing. |
| **Infrastructure Layer** | Registry compromise, CI/CD pipeline takeover, stolen model hub credentials. | Credential harvesting against high-privilege organization accounts on Hugging Face or GitHub. | Require multi-factor authentication (MFA); scope API keys with least privilege; isolate model evaluation inside hardened sandboxes. |

---

## 4. Question & Answer Reference

| Step / Prompt | Question / Concept | Answer / Key Value |
| :---: | :--- | :--- |
| **1** | Injection point for traditional attacks like SolarWinds | `Build process` |
| **2** | Type of dependency illustrated by `filelock` when installing `torch` | `transitive dependency` |
| **3** | Four core components of an AI supply chain (alphabetical order) | `Datasets, Dependencies, Frameworks, Models` |
| **4** | Technical mechanism that allows malicious model files to run arbitrary code | `serialised objects` |
| **5** | Dominant file format used for running quantized LLMs locally | `gguf` |
| **6** | Supply chain layer where pickle-based code execution occurs | `Model layer` |
| **7** | Level of attacks eliminated by converting models to SafeTensors | `Serialisation-level` |
| **8** | Supply chain layer targeted when backdooring 0.1% of a dataset | `Data Layer` |
| **9** | Supply chain layer targeted by a `torchtriton`-style package attack | `Dependency Layer` |

---

## 5. Defensive Hardening & Operational Best Practices

* **Eliminate Unsafe Deserialization:** Mandate the use of serialization-safe weight formats such as **SafeTensors** across all pipelines. If legacy checkpoints (`.pt`, `.bin`) must be processed, ensure loading calls specify `torch.load(..., weights_only=True)`.
* **Implement AI Bill of Materials (A-BOM):** Maintain complete manifests recording model commit hashes, base architecture digests, fine-tuning dataset provenance, and transitive library versions.
* **Scan Ingested Artifacts:** Run automated artifact scanners (such as `picklescan` or `fickling`) on any third-party weight files before staging them in local storage or training clusters.
* **Isolate Runtime Loading:** Execute external, untrusted models within non-root, ephemeral container sandboxes with network egress filtering enabled to prevent command-and-control callbacks.

---

## 6. Correlated Resources & Training Progression

* **Next Labs in Curriculum:**
  * [TryHackMe: Supply Chain Attack Vectors](https://tryhackme.com/room/supplychain-attack-vectors)
  * [TryHackMe: Securing the AI Supply Chain](https://tryhackme.com/room/securing-the-ai-supply-chain)
  * [TryHackMe: Data Poisoning](https://tryhackme.com/module/data-poisoning)
* **Industry Standards:**
  * **OWASP Top 10 for LLM:** [LLM03 - Supply Chain Vulnerabilities](https://genai.owasp.org/llmrisk/llm03-supply-chain-vulnerabilities/)
  * **MITRE ATLAS:** [AML.T0010 - ML Supply Chain Compromise](https://atlas.mitre.org/techniques/AML.T0010)
