# TryHackMe — AI Forensics

**Platform**: TryHackMe  
**Difficulty**: Medium  
**Category**: AI Security  
**Date**: 14 OCT 2026  
**Time spent**: ~2 hours (including write-up)  
**Tags**: `#AIForensics` `#DFIR` `#MachineLearning` `#AISecurity` `#LinuxForensics` `#scikit-learn` `#AnomalyDetection` `#TryHackMe`

Room 5 of the TryHackMe AI Security path (AI1). Explores how AI and machine learning can accelerate Digital Forensics and Incident Response while introducing new limitations, risks, and legal/ethical considerations.

## Overview

DFIR investigations are slow, data-heavy, and time-sensitive. This room examines where AI genuinely helps (anomaly detection, triage, timeline correlation, malware classification), where it falls short (non-determinism, precision/recall trade-offs, GIGO), and the legal/ethical constraints that come with using AI-processed evidence. The practical puts the theory to work with scikit-learn scripts against a Linux host that suffered a targeted breach at RobbCo.

## Learning Objectives

- Identify the day-to-day challenges DFIR teams face and where AI can help
- Understand how specific AI techniques (CNNs, NLP/transformers, unsupervised anomaly detection) map to forensic tasks
- Recognise the limitations of AI models in forensics (non-determinism, precision vs. recall, black-box behaviour)
- Evaluate the legal and ethical implications of AI-generated or AI-processed evidence (Daubert, chain of custody, bias, explainability)
- Apply AI-assisted tools in a practical investigation while validating every finding with human analysis

## Task Index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Scope, prerequisites, learning objectives; frames the question “does DFIR need AI?” |
| 2 | The AI Forensics Landscape | Data processing & scalability, anomaly detection/UEBA, alert triage, timeline correlation; key limitations (precision vs. recall, non-determinism, GIGO) |
| 3 | AI & DFIR | CNNs for image/video forensics, NLP/transformers for phishing & communications analysis, timeline reconstruction from time-sequenced data, static vs. dynamic malware analysis |
| 4 | AI Legal & Ethical Implications | Daubert test, black-box models, facial recognition bias, federated learning, explainability, accountability, chain of custody for AI-processed evidence, privacy |
| 5 | Practical: The Digital Trail | Hands-on Linux forensics lab using scikit-learn scripts (`classify_logs.py`, `file_anomalies.py`) to reconstruct a RobbCo breach: phishing → privilege escalation → persistence → exfiltration |
| 6 | Conclusion | Recap — AI is a guiding light, not a verdict; human validation remains essential |

## Key Concepts

**Why AI in DFIR?**  
Investigations generate massive volumes of logs, files, and telemetry. AI excels at scale, pattern recognition, and prioritisation — turning “needle in a haystack” problems into manageable leads.

**Core AI applications in forensics**  
- **Anomaly detection / UEBA** — unsupervised models (e.g. Isolation Forest) learn normal behaviour and flag deviations  
- **Phishing & communications analysis** — NLP models (BERT-style transformers) detect urgency, impersonation, and malicious intent  
- **Image / video forensics** — Convolutional Neural Networks (CNNs) learn spatial patterns  
- **Timeline reconstruction** — correlation of time-sequenced data across sources  
- **Malware analysis** — static feature classification and dynamic behaviour modelling (API call sequences, etc.)

**Model limitations that matter in court and operations**  
- **Precision vs. Recall** — high precision reduces false positives; high recall reduces missed threats. Forensic work usually prioritises precision.  
- **Non-determinism** — the same input can produce different outputs across runs.  
- **GIGO** — models are only as good as the data they were trained on.  
- **Black-box problem** — many models cannot easily explain *why* they flagged something.

**Legal & ethical constraints**  
- **Daubert standard** — U.S. test for admissibility of scientific/expert testimony  
- **Chain of custody** — must still be maintained when AI processes evidence  
- **Bias** — facial recognition and other models have demonstrated demographic bias  
- **Federated learning** — privacy-preserving approach that trains models without centralising sensitive data  
- Explainability, accountability, and the requirement for human oversight

**Practical takeaway from the RobbCo case**  
AI scripts rapidly surfaced anomalous logins and suspicious files on a Linux host. Human analysis was still required to reconstruct the full kill chain (phishing email → credential use → SSH key planting → source-code exfiltration via `/dev/shm`).

## Skills & Mapping

anomaly detection · UEBA concepts · precision/recall trade-offs · CNN & NLP applications in forensics · timeline correlation · static vs. dynamic malware analysis · Daubert / chain-of-custody awareness · scikit-learn assisted triage · Linux artifact analysis

**Role mappings**  
- DFIR analyst / incident responder → AI-assisted triage and validation  
- SOC analyst → anomaly detection and alert prioritisation  
- Forensic examiner → legal/ethical constraints on AI-processed evidence  
- Threat hunter → using ML outputs as leads rather than conclusions

## Personal Takeaways

AI is genuinely useful for speed and scale, but it is not a replacement for investigative judgement. Every high-confidence AI finding in the practical still needed human confirmation. Treat model output as a strong hypothesis generator, not as evidence that stands on its own.

## References

- TryHackMe room: https://tryhackme.com/room/aiforensics  
- NIST SP 800-61 Rev. 2 — Computer Security Incident Handling Guide  
- Daubert standard (U.S. Supreme Court)  
- scikit-learn documentation: https://scikit-learn.org/  
