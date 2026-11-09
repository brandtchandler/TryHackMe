# TryHackMe - Supply Chain Attack Vectors

**Platform**: [TryHackMe](https://tryhackme.com/room/supplychain-attack-vectors)  
**Difficulty**: Medium  
**Category**: AI / ML Security  
**Date**: 08 Nov 2026  
**Time spent**: ~2 hours (including write-up)  
**Tags**: `#AI-security` `#SupplyChain` `#Pickle` `#SafeTensors` `#DependencyConfusion` `#PromptSecurity`

---

## Summary

At TryTrainMe, an attacker claimed three weeks of access to enterprise servers through an “AI-powered” code reviewer. The investigation reveals a multi-vector supply chain attack that stacks compromises across model files, packages, repositories, and prompt templates, aligning with OWASP LLM03 and MITRE ATLAS AML.T0010.

## Key Takeaways

- **Adversaries stack vectors** — Attackers do not rely on a single technique; if model deserialisation fails, dependency confusion or repository manipulation acts as a fallback.
- **`pickle` deserialisation is arbitrary code execution** — Loading untrusted pickle files exposes the host system via the `__reduce__` method and the `os` module.
- **SafeTensors is not a silver bullet** — While it neutralises serialisation-level execution, architecture-level threats (such as malicious Keras `Lambda` layers) persist.
- **Supply chains extend to prompts and APIs** — Silent model changes and untrusted prompt templates alter downstream application behaviour without running host-level code.

---

## Learning Objectives & Tasks

### Task 1 – Summary & Overview

Sets the scene for the multi-layer breach at TryTrainMe. Highlights how modern AI applications rely on complex, interdependent supply chains spanning weights, code packages, public hubs, and upstream prompts.

### Task 2 – Core Attack Vectors

Adversaries leverage multiple layers of the machine learning pipeline to gain initial access and establish persistence.

#### Vector 1: Malicious Model Serialisation (Pickle)

Python’s `pickle` format implements a stack-based virtual machine. When an untrusted model is loaded, custom objects can trigger arbitrary code execution:

- Pickle invokes the **`__reduce__`** method to fetch reconstruction instructions.
- The **`os`** module serves as the primary sink for operating system commands.
- The **`REDUCE`** opcode executes the callable provided by `STACK_GLOBAL`.

Safe static analysis and disassembly are conducted via:

```bash
python3 -m pickletools -a [-o FILE]

Disassemble and optimize one or more pickle files.
```

In the lab exercise, the payload triggers an outbound connection attempt to `attacker.com`.

#### Vector 2: Serialisation vs Architecture-Level Attacks

Converting a Keras `.h5` model to SafeTensors:
- Eliminates pickle-based payloads (**serialisation-level attacks**).
- Leaves **architecture-level attacks** untouched.
- Fails to neutralise suspicious **`Lambda`** layers.

SafeTensors stores raw tensor arrays alongside JSON metadata and rejects arbitrary object instantiation. However, custom layers that evaluate computational code during graph construction remain an active vector.

#### Vector 3: Dependency Confusion & Typosquatting

- **Dependency confusion** – An attacker registers a public package using the same name as an internal corporate library, appending a higher version number so package managers fetch the external payload.
- **Typosquatting** – An attacker registers names visually similar to widely adopted packages or models (e.g., `torchtriton`).

#### Vector 4: Model Repository Manipulation

Threat actors establish spoofed publisher profiles on hosting platforms like Hugging Face (e.g., `trustworthy-ai-lab`) to make modified, backdoored models appear legitimate to downstream developers.

#### Vector 5: API & Prompt Template Supply Chain

When consuming AI capabilities upstream via remote APIs:
- **Silent model updates** swap underlying model checkpoints without consumer notice.
- **Untrusted prompt templates** or system instructions introduce systemic behavioural compromises across any application ingesting them.

---

## Threat Matrix & Mitigations

| Attack Layer | Mechanism / Indicator | Impact | Primary Mitigation |
| :--- | :--- | :--- | :--- |
| **Model Serialisation** | `__reduce__` → `os` via `STACK_GLOBAL` / `REDUCE` | RCE | Prefer SafeTensors; inspect with `pickletools` / Fickling; set `weights_only=True` |
| **Model Architecture** | Malicious Keras `Lambda` layers | Arbitrary code execution / graph abuse | Audit computation graphs; disallow arbitrary custom layer execution |
| **Dependencies** | Public package overrides internal library | Build and deployment pipeline takeover | Pin strict versions; enforce private package index URLs; verify hashes |
| **Model Registry** | Spoofed organisations (`trustworthy-ai-lab`) | Distribution of tampered weights | Enforce strict vendor validation; pin commit SHAs; avoid unvetted hubs |
| **Prompt / API Pipeline** | Upstream prompt templates or silent updates | Systemic behavioural control / injection | Treat prompts as version-controlled code; enforce change-management review |

---

## Question & Answer Reference

| # | Question | Answer |
| :-: | :--- | :--- |
| **1** | Python method pickle calls for reconstruction instructions | `__reduce__` |
| **2** | Built-in module commonly abused in pickle payloads | `os` |
| **3** | Attack type left untouched by SafeTensors conversion | architecture-level attacks |
| **4** | Suspicious layer type that survives conversion from `.h5` | `Lambda` |
| **5** | Module for safe pickle disassembly | `pickletools` |
| **6** | Opcode that executes the function from `STACK_GLOBAL` | `REDUCE` |
| **7** | Public package overrides internal package of same name | dependency confusion |
| **8** | Technique of registering closely resembling names | typosquatting |
| **9** | Vector used by creating `trustworthy-ai-lab` on Hugging Face | repository manipulation |
| **10** | Fallback vector if pickle payload is blocked | dependency confusion |
| **11** | Model behind an API endpoint changed without notice | silent model update |
| **12** | Untrusted artefact that can alter LLM behaviour across apps | prompt template |

---

## Defensive Perspective

- Default to SafeTensors formats over pickle-based alternatives whenever possible.
- Scan models with tools like **Fickling** and **ModelScan** prior to pipeline ingestion.
- Enforce strict zero-trust validation on external models, repositories, and prompt templates.
- Pin package versions and internal registry index URLs to thwart dependency confusion.
- Continuously monitor API endpoints for behavioural anomalies or unannounced model updates.
- Store, audit, and peer-review prompt templates under source control.

---

## Resources & Next Steps

- **Prerequisite Room**: Understanding AI Supply Chains
- **Next Room**: Securing the AI Supply Chain
- **Defensive Tooling**: Fickling, ModelScan, `pip-audit`, Syft (Software Bills of Materials)

---

## Final Summary

Securing AI applications requires treating models, dependencies, repositories, and prompt files as critical supply chain components. Blocking unsafe serialisation like `pickle` is only the first line of defence; robust protection demands signed artefacts, private dependency verification, computational graph inspection, and rigorous prompt auditing.
