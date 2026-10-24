# TryHackMe - AI Threat Modelling

**Platform**: TryHackMe  
**Difficulty**:  Medium
**Category**:  AI Security
**Date**:  18 OCT 2026
**Time spent**:  2 hours ( Including write up)
**Tags**: `#AISecurity` `#MITREATLAS` `#Stride` `#OWASPLLMTop10`

---

## Summary

AI Threat Modelling is a defender-focused room on TryHackMe that teaches how to systematically assess and document risks in enterprise AI/ML systems. You play the role of a threat analyst at MegaCorp, evaluating deployments such as a customer-facing LLM chatbot with RAG, a recommendation engine, and a fraud detection system. The room covers AI-specific assets (training data, model weights, embeddings, system prompts, model registries), adapts the STRIDE framework for AI, incorporates MITRE ATLAS techniques, and maps OWASP LLM Top 10 risks to architectural components. The goal is to produce a structured threat assessment that accounts for the unique behaviours and failure modes of AI systems.

## Key Takeaways / Personal Takeaways

- AI systems introduce entirely new assets that traditional threat models miss: training data, model weights, embedding vectors, system prompts, feature stores, and model registries. Missing these means missing whole categories of risk.
- The AI data supply chain is a critical attack surface. Threats can be introduced at collection, labelling, training, packaging, or inference stages — and the effects (especially data poisoning) are often delayed and hard to detect.
- Classic STRIDE still works, but it needs to be adapted. Categories like Tampering (data poisoning), Information Disclosure (model extraction), and Elevation of Privilege (jailbreaking / prompt injection) take on new meanings in AI systems.
- MITRE ATLAS fills the gaps left by STRIDE by providing AI-specific tactics, techniques, mitigations, and real-world case studies (the ATT&CK equivalent for AI/ML).
- OWASP LLM Top 10 is the practical mapping tool. It lets you look at an architecture diagram and immediately identify which components are exposed to which risks and at what severity.
- Threat modelling AI is a complete workflow, not a one-time checklist:
Identify AI assets → Map the data supply chain → Adapt STRIDE → Enrich with ATLAS → Map OWASP risks to components → Produce a prioritised assessment.

-The traditional models for security are a good start, but we need to evolve them to adapt properly to AI. Understanding the uniquness of AI and treat it as such. The effectiveness of our security models comes from adapting to this new distinct technology that we know as Artificial Intelligence. 

---

## Learning Objectives

- Identify AI-specific assets and attack surfaces that don't exist in traditional applications
- Apply STRIDE threat categories to AI/ML system components with appropriate context
- Use MITRE ATLAS to enumerate adversarial techniques targeting AI systems
- Map OWASP LLM Top 10 risks to architectural components to identify where threats live and how to prioritise them
- Produce a structured threat assessment for an AI deployment

---

## Learning Objectives & Tasks

### Task 1 – Introduction
Sets the scene: AI is already in production, traditional threat modelling (STRIDE) is insufficient on its own, and you join MegaCorp as a threat analyst tasked with assessing their AI deployments before a board meeting.

### Task 2 – AI-Specific Assets and Attack Surfaces
Introduces new asset types that traditional threat models miss: Training Data, Model Weights/Parameters, Embedding Vectors, System Prompts, Feature Stores, and Model Registry/Artifacts. Also covers non-deterministic behaviour and the black-box problem.

### Task 3 – Data Supply Chain and STRIDE’s Gaps
Maps the AI data supply chain (Data Collection → Cleaning/Labelling → Model Training → Validation/Packaging → Inference) and explains why classic STRIDE falls short for delayed, diffuse threats like training data poisoning.
STRIDE (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege)(Cuurently changing and adapting the definition for AI)

### Task 4 – Adapting STRIDE for AI Systems
Retunes each STRIDE category for AI contexts (e.g., Tampering → data poisoning, Information Disclosure → model extraction, Elevation of Privilege → jailbreaking/prompt injection). Links to OWASP LLM Top 10 entries where relevant.

### Task 5 – MITRE ATLAS: The AI Threat Technique Catalogue
Introduces MITRE ATLAS (Adversarial Threat Landscape for Artificial-Intelligence Systems) as the ATT&CK equivalent for AI/ML systems. Covers its structure (tactics, techniques, mitigations, case studies) and how to use it to enrich STRIDE findings.

### Task 6 – OWASP LLM Top 10: Mapping Risks to Components
Shows how to map the OWASP LLM Top 10 (2025) risks directly onto architectural components so you can look at a diagram and immediately identify which parts are exposed to which threats.

### Task 7 – Practical: Threat Modelling MegaCorp’s AI Assistant
Interactive exercise: map OWASP LLM Top 10 risks to components in MegaCorp’s architecture and produce a prioritised threat assessment.

### Task 8 – Conclusion
Recap of the full workflow: identify AI assets → map the data supply chain → adapt STRIDE → enrich with ATLAS → map OWASP risks to components → deliver a structured assessment.

---

## Practical Notes

- Focus is defender-side: identification, documentation, and prioritisation — not exploitation.
- Key assets to always inventory: Training Data, Model Weights, Embeddings, System Prompts, Feature Stores, Model Registry.
- STRIDE still works but needs AI-specific interpretation (especially Tampering and Elevation of Privilege).
- ATLAS provides the technique-level detail and real-world case studies that STRIDE lacks.
- OWASP LLM Top 10 is the practical lens for mapping risks onto architecture diagrams.
- Practical task requires selecting and justifying OWASP mappings against MegaCorp’s components.

---

## References

- TryHackMe room: https://tryhackme.com/room/aithreatmodelling  
- MITRE ATLAS: https://atlas.mitre.org/  
- OWASP LLM Top 10 (2025): https://genai.owasp.org/  
