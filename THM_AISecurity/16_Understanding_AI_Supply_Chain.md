
# Understanding AI Supply Chains - Write-Up

**Date:** 2026-11-04  
**Category:** AI Security / AI Supply Chain  
**Level:** Easy  
**Focus:** Concepts, attack layers, and real-world risks in AI supply chains

---

## Summary

This room introduces the AI supply chain: the models, datasets, frameworks, and dependencies that modern AI systems rely on. It contrasts traditional software supply chains with AI-specific risks and maps four attack layers.

**Key idea:** AI systems inherit trust from external components. Compromising any of those components can compromise the final system.

---

## Core Concepts

### Traditional vs AI Supply Chain
- **Traditional (e.g. SolarWinds):** Malicious code injected into the **build process**.
- **AI:** Extra surfaces — model weights, training data, serialisation formats, and the packages that load them.

**Transitive dependency example:** Installing `torch` also pulls in `filelock` (you never listed it).

### Four Key Components of an AI Supply Chain
(listed alphabetically)
- **Datasets**
- **Dependencies**
- **Frameworks**
- **Models**

Model files often contain **serialised objects**. When loaded, these can execute code (classic pickle risk).

### Two Ways to Consume AI
1. **Local models** — download and run yourself (dominant local LLM format: **gguf**).
2. **API / hosted models** — you never see the underlying weights or data; trust is placed in the provider.

### Four Attack Layers

| Layer          | Example attacks                          | Notes |
|----------------|------------------------------------------|-------|
| **Model**      | Pickle-based code execution, malicious serialisation | Convert to **SafeTensors** to eliminate serialisation-level attacks |
| **Dependency** | Dependency confusion, typosquatting     | e.g. torchtriton package abuse |
| **Data**       | Data poisoning, backdoored training sets | Even 0.1% crafted samples can introduce a backdoor |
| **Infrastructure** | Compromised build, hosting, or registry | Credential theft on high-trust repos |

---

## Key Answers (Quick Reference)

- SolarWinds injection point: **Build process**
- `filelock` type: **transitive dependency**
- Four components (alphabetical): **Datasets, Dependencies, Frameworks, Models**
- What lets model files run code: **serialised objects**
- Dominant local LLM format: **gguf**
- Pickle attacks occur at: **Model layer**
- SafeTensors eliminates: **Serialisation-level** attacks
- Poisoned 0.1% of dataset: **Data Layer**
- torchtriton-style attack: **Dependency Layer**

---

## Takeaways

- AI supply chains are longer and more opaque than traditional software ones.
- Serialisation (especially pickle) is a major practical risk; prefer SafeTensors / `weights_only=True`.
- Trust is transitive: a compromised model, dataset, package, or repo can reach production.
- Defence requires visibility (SBOMs, checksums, scanning) and least-privilege model loading.

This room is foundational for the later practical rooms (Supply Chain Attack Vectors, Securing the AI Supply Chain, etc.).
