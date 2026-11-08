# TryHackMe - Securing AI Systems

**Platform**: TryHackMe  
**Difficulty**: Medium  
**Category**: AI Security  
**Date**: 15 OCT 2026  
**Time spent**: ~1–2 hours (including write-up)  
**Tags**: `#AISecurity` `#OWASP` `#ATLAS` `#TrustBoundaries` `#MLSecOps` `#LeastPrivilege` `#TryHackMe`

---

## Summary

Room 6 in the AI Security path. Moves up one layer from model-level risks to the full production architecture of an AI system. You act as the security architect reviewing **TryAssist** (an AI-powered code review assistant) before it goes live. The focus is mapping components, identifying trust boundaries, classifying risks with OWASP LLM Top 10 (2025) and MITRE ATLAS, and applying secure design patterns.

## Key Takeaways / Personal Takeaways

- **AI security is architecture security** — the model is only one component. The real attack surface lives in the data flows between users, the LLM, tools, vector stores, and external systems.
- **Every trust boundary is a potential attack surface** — especially User-to-system, System-to-LLM, and LLM-to-tools.
- **Five system-level OWASP risks matter most at design time**: Improper Output Handling (LLM05), Excessive Agency (LLM06), System Prompt Leakage (LLM07), Sensitive Information Disclosure (LLM02), and Unbounded Consumption (LLM10).
- **Least privilege + human approval for high-risk actions** are non-negotiable when an LLM can trigger tools or change production state.
- **MLSecOps** (monitoring, observability, and incident response integrated into the ML lifecycle) is the operational counterpart to traditional SecOps.

---

## Learning Objectives

- Identify the core components of a production AI system and the data flows between them
- Identify the OWASP LLM Top 10 (2025) and MITRE ATLAS as the primary frameworks for AI threat classification
- Explain five system-level threat categories: improper output handling, excessive agency, system prompt leakage, unbounded consumption, and sensitive information disclosure
- Apply secure design patterns including defence in depth, least privilege, and monitoring to AI system architectures

---

## Learning Objectives & Tasks

### Task 1 – Introduction
Introduces TryAssist (AI code-review assistant connected to docs, repos, APIs, and CI/CD). Highlights how adding AI expands the attack surface far beyond traditional web apps. Sets the role: security architect performing a pre-deployment review.

### Task 2 – Anatomy of an AI System
Maps the nine core components of a production AI system and the five trust boundaries.

**Key Components**:
- User Interface
- API Gateway
- Orchestration Layer
- Prompt Construction (combines system prompt + user input + retrieved context)
- LLM
- Tool Layer
- Output Processing
- Logging and Monitoring
- Vector Store (RAG)

**Five Trust Boundaries**:
| Boundary                  | Data Crossing                                      |
|---------------------------|----------------------------------------------------|
| User-to-system            | Untrusted natural language enters the system       |
| System-to-LLM             | Constructed prompt sent to the model               |
| LLM-to-tools              | Model output triggers database/API/file actions    |
| System-to-external-data   | Retrieved documents enter the prompt               |
| System-to-user            | Generated response delivered to the user           |

### Task 3 – The AI Attack Surface
Introduces the three primary frameworks:
- **OWASP LLM Top 10 (2025)** — vulnerability classification
- **MITRE ATLAS** — adversary tactics & techniques for AI/ML systems
- **NIST AI RMF** — organisational risk management (Govern, Map, Measure, Manage)

Focuses on the five architecture-level OWASP categories relevant to pre-deployment review.

### Task 4 – System-Level Threats
Deep dive into the five key risks:

- **LLM05 – Improper Output Handling**: LLM output used to execute injection attacks (e.g., SQL) against downstream systems
- **LLM06 – Excessive Agency**: Three dimensions — Excessive Functionality, Excessive Permissions, Excessive Autonomy
- **LLM07 – System Prompt Leakage**: Exposure of internal instructions, API endpoints, or configuration
- **LLM10 – Unbounded Consumption**: Resource exhaustion / denial-of-wallet via long or high-volume requests
- **LLM02 – Sensitive Information Disclosure**: Leakage of PII, secrets, or internal data

### Task 5 – Secure Design Patterns
Practical controls:
- Defence in depth at every trust boundary
- **Least Privilege** for every component
- Human approval for high-risk actions
- Input and output validation
- Rate limiting and cost ceilings
- **MLSecOps** — security integrated into the ML lifecycle (monitoring, observability, incident response)

### Task 6 – Auditing TryAssist
Hands-on audit of the live TryAssist system. Key findings typically include:
- Automatic actions without human approval (e.g., merging pull requests)
- Over-privileged database role (e.g., `db_admin`)
- Conversation logging without PII filtering

### Task 7 – Conclusion
Securing AI requires looking at the whole system:  
**User → Application → LLM → Tools → Data → External Systems**

Traditional application security is necessary but insufficient. The new components create risks that firewalls and WAFs alone cannot address.

---

## Practical Notes – Auditing TryAssist

When auditing an AI assistant, systematically check:

1. **Capabilities** — What tools and data sources can it reach?
2. **Autonomy** — Which actions can it take without human approval?
3. **System instructions** — Do they contain secrets or internal endpoints?
4. **Data retention & logging** — Is PII filtered? Is the audit trail complete?
5. **Permissions** — Does every component run with least privilege?

---

## References
 
- TryHackMe room: https://tryhackme.com/room/securingaisystems 
- OWASP LLM Top 10 (2025): https://genai.owasp.org/  
- MITRE ATLAS: https://atlas.mitre.org/  
- NIST AI Risk Management Framework  
