# Data Poisoning in RAG Systems - Write-Up

**Room:** [TryHackMe - Data Poisoning in RAG Systems](https://tryhackme.com/room/datapoisoninginragsystems)  
**Category:** AI / ML Security  
**Difficulty:** Medium  
**Focus:** How attackers poison training data, embeddings, and ingestion pipelines in RAG systems  
**Frameworks:** OWASP LLM04 (Data & Model Poisoning)

---

## 1. Summary & Key Takeaways

Data poisoning attacks the information an AI system trusts rather than the prompts it receives. In RAG systems this is especially dangerous because the model treats retrieved documents as authoritative context.

No model weights need to be changed. No prompts need to be injected. If the knowledge base or embedding space is poisoned, the model will confidently produce incorrect or malicious answers.

### Core Learnings
- **Training data poisoning** permanently alters what the model learns.
- **Corpus / embedding poisoning** changes what the retriever returns without touching the base model.
- **Ingestion pipeline attacks** exploit weak validation when documents are collected, parsed, and indexed.
- Effects are often **subtle** — gradual behavioural drift that looks normal while the infrastructure keeps running.
- In the practical, modifying **reference material** is enough to change the assistant’s behaviour (classic data poisoning).

---

## 2. Core Concepts

### Training Data Poisoning
Manipulates the data used during model training or fine-tuning. The poisoned examples become part of the model’s weights.

**Answer:** Type of poisoning that affects model training → **Training Data**

### Embeddings and Vector Databases
Two important corpus-level techniques:

| Technique              | Description |
|------------------------|-------------|
| **Corpus Flooding**    | Increases the density of attacker-controlled documents in a specific semantic region so they rank highly |
| **Semantic Mimicry**   | Imitates the tone and structure of trusted documents to blend in |
| **Embedding-Level Poisoning** | Manipulates how documents are represented in vector space without changing the base model |

### Ingestion Pipeline Attacks
The **ingestion pipeline** collects, parses, and indexes documents into the knowledge base. Weak controls here allow poisoned content to enter automatically.

Related real-world parallel: in the 2021 dependency confusion attacks, build systems automatically pulled **malicious packages** from public repositories.

### Impact on Model Behaviour
- **Subtle** effects produce small, gradual behavioural shifts that appear normal.
- When poisoning alters behaviour but the system stays operational, what has been corrupted is the **Data**.

### Practical (PaperTrail Technologies)
The lab AI assistant answers internal policy questions. Reference material can be updated by users without proper validation.

- Component modified to influence behaviour → **Reference Material**
- Attack class → **Data Poisoning**

---

## 3. Quick Answer Reference

| Question | Answer |
|----------|--------|
| Type of poisoning that affects model training | Training Data |
| Technique that increases density of attacker documents in a semantic region | Corpus Flooding |
| Poisoning that manipulates vector representations without changing the base model | Embedding-Level Poisoning |
| Technique that imitates tone/structure of trusted documents | semantic mimicry |
| Pipeline that collects, parses, and indexes documents | Ingestion Pipeline |
| What the 2021 dependency confusion build systems pulled | malicious packages |
| Poisoning effect with small, gradual behavioural shifts | Subtle |
| What is corrupted when behaviour changes but infrastructure stays up | Data |
| Component modified in the practical to change assistant behaviour | Reference Material |
| Attack class of modifying trusted knowledge | Data Poisoning |

---

## 4. Defensive Perspective

- Treat the ingestion pipeline as a security boundary — validate, sanitise, and review documents before they are indexed.
- Monitor for **output drift** and unexpected ranking changes in retrieval results.
- Prefer behavioural monitoring over pure signature-based detection (poisoning is often subtle).
- Control who can update reference / knowledge-base material and require review.
- Consider source provenance and integrity checks for both training corpora and runtime knowledge bases.
- Defence-in-depth: even if one layer is poisoned, limit the blast radius through access controls and monitoring.

---

## 5. Resources & Next Steps

- **Related room:** [RAG Security Fundamentals](https://tryhackme.com/room/ragsecurityfundamentals)
- Module: Data Poisoning (includes Sensitive Information Disclosure and practical challenges)
- Framework: OWASP LLM04 – Data & Model Poisoning
