# TryHackMe - AI Threat Modelling Assessment

**Platform**: TryHackMe  
**Difficulty**: Easy  
**Category**: AI Security  
**Date**: 21 OCT 2026  
**Time spent**: ~15–30 minutes (including write-up)  
**Tags**: `#AIThreatModelling` `#AISecurity` `#OWASP` `#ATLAS` `#TryHackMe`

---

## Summary

Interactive assessment room that tests the skills learned in the preceding AI Threat Modelling and Secure AI Systems content. You complete a two-phase challenge inside a web-based application: first answering guided scenario questions about AI vulnerabilities and components, then placing defensive “shields” on an architecture diagram to mitigate specific attacks. No machine is required — everything runs in the browser.

## Key Takeaways / Personal Takeaways

- Reinforces the ability to quickly identify which AI component is most exposed to a given attack (e.g., LLM Agent for prompt injection, Retrieval System for embedding leakage).
- Strengthens mapping of real-world scenarios to OWASP LLM Top 10 categories and appropriate controls.
- Highlights that correct placement of defences (rate limiting, anomaly detection, output filtering, etc.) on the right architectural layer is more important than knowing the attack name alone.
- Short but effective validation of the full threat-modelling workflow learned earlier in the path.

---

## Learning Objectives

- Apply AI threat modelling knowledge to realistic scenarios
- Correctly identify vulnerable components and vulnerability types
- Select appropriate preventative controls for common AI attacks
- Practise mapping defences onto an AI system architecture diagram

---

## Learning Objectives & Tasks

### Task 1 – Assessment

The entire room consists of a single interactive assessment with two phases:

**Phase 1 – Guided Questions**  
Multiple-choice / scenario-based questions that test:
- Component identification (e.g., which component is most exposed to a prompt injection attempt)
- Vulnerability classification (e.g., Sensitive Information Disclosure, Data Poisoning)
- Selection of the best preventative control (rate limiting, anomaly detection, output filtering, etc.)

Common scenarios include:
- Prompt injection attempts targeting the LLM Agent
- Leakage of internal data via model responses or retrieval
- Manipulation of recommendations through fake user behaviour
- High-volume scraping / Denial-of-Wallet style abuse
- Training-data poisoning

**Phase 2 – Attack Simulation**  
Interactive architecture diagram. You must place defensive shields on the correct components to stop specific incoming attacks (prompt injection, data leakage, data poisoning, etc.).

Architecture typically follows the flow:  
**User Input → API Gateway → Prompt Construction → LLM Agent → Retrieval → Database**

---

## Practical Notes

- Read each scenario carefully — the correct component is usually the one that directly processes or acts on the malicious input.
- For Phase 2, place shields on the layer where the attack can be most effectively stopped (not just the final victim component).
- Completing both phases awards the two flags.

---

## References

- TryHackMe room: https://tryhackme.com/room/aithreatmodellingassessment  
- Related rooms: AI Threat Modelling, Securing AI Systems  
- OWASP LLM Top 10 (2025): https://genai.owasp.org/  
- MITRE ATLAS: https://atlas.mitre.org/
