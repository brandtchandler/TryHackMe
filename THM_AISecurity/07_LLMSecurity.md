# TryHackMe - AI Security

**Platform**: TryHackMe  
**Difficulty**: Medium  
**Category**: AI Security  
**Date**:  17 OCT 2026
**Time spent**: 1-2 hour 
**Tags**: `#LLMSecuriy` `#AISecurity` `#OWASP` `#PromptInjection`

---

## Summary

Understand LLMs as an attack surface and get an overview of the main LLM security threats. Covers four threat categories: data-based, model-based, system-based and user-based

## Key Takeaways / Personal Takeaways

- Understanding the weaknesses of any AI is important when it comes to defending it. 
- There are multiple ways to attack LLM's which means the defense must also me in-depth and broad.

---

## Learning Objectives

- Understand LLM-specific vulnerabilities that do not apply to traditional ML systems
- Recognize how LLMs create new attack surfaces through natural language interface and memory/context mechanisms
- Identify and categorise LLM threat types: data-based, model-based, system-based, and user-based
- Understand the realistic risks LLMs introduce in production systems

---

## Learning Objectives & Tasks

### Task 1 – Introduction
Sets the scene and introduces the four threat categories

### Task 2 – [Task Name]
- Training Data Extraction
- Membership Inference
- Prompt Leakage / System Prompt Exposure (LLM07)

### Task 3 – Model-Based Threats
- Model Extraction (Model Theft)
- Model Inversion

### Task 4 – System-Based Threats
- Prompt Injection
- Context Window / Memory issues
- Memory Poisoning

### Task 5 – User-Based Threats
- LLM-powered social engineering / phishing amplification
- Supply-chain style risks (malicious packages, etc.)

### Task 6 – Conclusion
Recap of the four threat categories and key defensive mindset.

---

## Practical Notes

- Prompts Are Not Security Boundaries: Never store sensitive keys or confidential data in system instructions; prompt leakage easily bypasses conversational guardrails, and persistent memory can be poisoned across sessions.

- Treat Output as Untrusted Input: Never route raw LLM responses directly into system shells, SQL queries, or backend APIs—enforce strict output sanitization, sandboxing, and least-privilege tool execution.

- Model and Data Exposure Risks: Attackers can systematically query public endpoints to extract proprietary training data, confirm user records (MIA), or clone model weights at low cost.

- Architecture Beats Prompt Rules: Blacklisting words or relying on model alignment fails against indirect injections; robust defense requires hard technical controls, input/output validation layers, and human-in-the-loop approval for high-risk actions.

---

## References

- TryHackMe room: https://tryhackme.com/room/llmsecurity
- OWASP LLM Top 10
- Garak & Lakera Gandalf: Practical testing platforms—Garak for automated CLI vulnerability scanning and Gandalf for manual prompt injection drills.
- NVIDIA NeMo Guardrails: Open-source architectural blueprint for enforcing programmable input/output rails and dialog safety layers outside the model.
