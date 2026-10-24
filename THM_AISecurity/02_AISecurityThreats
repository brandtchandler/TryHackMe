# TryHackMe — AI Security Threats

**Platform**: TryHackMe  
**Difficulty**: Easy  
**Category**: AI Security  
**Date**: 11 OCT 2026  
**Time spent**: ~1 hour (including write-up)  
**Tags**: `#AI` `#MachineLearning` `#PromptEngineering` `#MITREATLAS` `#DefensiveAI` `#DataPoisoning` `#ISO27090` `#TryHackMe`

Entry-level room covering the fundamental building blocks of Artificial Intelligence and Machine Learning. Explores foundational ML mechanics, neural architectures, how modern Large Language Models operate, the main classes of AI-specific threats, AI-enhanced attacks, defensive uses of AI, and basic AI security hygiene.

## Overview

This room introduces the core concepts needed before diving deeper into AI security. It maps common AI vulnerabilities to the MITRE ATLAS framework, shows how attackers are already using AI to improve traditional attacks, demonstrates defensive applications of AI, and stresses that adopting AI expands your attack surface unless it is properly secured.

## Learning Objectives

- Understand the relationship between AI, Machine Learning, Neural Networks, and Large Language Models
- Identify the five primary AI model vulnerabilities (Prompt Injection, Data Poisoning, Model Theft, Privacy Leakage, Model Drift)
- Recognise how AI is enhancing existing attack techniques (deepfakes, phishing, malware generation)
- Explain the four main defensive uses of AI (analysis, prediction, summarisation, investigation)
- Apply basic AI security hygiene: access control, data protection, standards, and model monitoring

## Task Index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Room objectives and key vocabulary |
| 2 | Vulnerabilities in AI Models | Five core threats via MITRE ATLAS + Prompt Injection exercise against MENTOR |
| 3 | AI-Enhanced Attacks | Deepfakes, AI-powered phishing, and other accelerated attack methods |
| 4 | Defensive AI | Analysis, prediction, summarisation, investigation + AEGIS walkthrough |
| 5 | Securing AI | AI security hygiene, ISO/IEC 27090, monitoring tools (SHAP, LIME) |
| 6 | Practical | Graduation questions on modern generative LLMs |
| 7 | Conclusion | Recap and key points |

## Key Concepts

**AI Hierarchy**  
- Artificial Intelligence — broad field  
- Machine Learning — subfield of AI  
- Neural Networks — inspired by the human brain; more than three layers = Deep Learning  
- Large Language Models — specialised neural networks that predict token sequences based on learned patterns  

**Five Core AI Vulnerabilities** (MITRE ATLAS)  
1. **Prompt Injection** — input that bypasses system instructions or restrictions and forces the model outside its intended scope  
2. **Data Poisoning** — manipulation of training data before the model is trained, introducing defects or backdoors  
3. **Model Theft** — unauthorised access or extraction of a model (often via API querying) to replicate or misuse it  
4. **Privacy Leakage** — sensitive training data (PII, credentials, proprietary information) being regurgitated by the model  
5. **Model Drift** — performance degradation when the model falls behind real-world changes because its training data is outdated  

**AI-Enhanced Attacks**  
Traditional attacks become faster, cheaper, and more convincing:  
- Deepfakes (voice, video, image)  
- Highly fluent, context-aware phishing  
- AI-generated malware and attack tooling  

**Defensive AI**  
Organisations using AI for defence have been shown to identify and contain breaches significantly faster (IBM data cited a 108-day improvement). Four practical areas:  
- Analysis — pattern recognition at scale  
- Prediction — anticipating attacker techniques  
- Summarisation — distilling large volumes of logs and alerts  
- Investigation / threat hunting — spotting signals humans miss  

**AI Security Hygiene**  
- Secure the models themselves (RBAC, MFA)  
- Protect training and inference data (audit, minimise, encrypt)  
- Follow emerging standards (ISO/IEC 27090)  
- Continuously monitor models (tools such as SHAP and LIME for explainability)

## Skills & Mapping

vulnerability identification · MITRE ATLAS mapping · prompt injection basics · defensive AI use-cases · AI security hygiene

Useful role mappings:  
- Security analyst / SOC → defensive AI (analysis, summarisation, investigation)  
- Red team / AI pentester → prompt injection and model theft techniques  
- AI/ML engineer or AppSec → data poisoning awareness, model monitoring, ISO/IEC 27090 alignment

## Personal Takeaways

Adopting AI for security clearly reduces breach cost and response time, but only if the AI systems themselves are treated as high-value assets that need protecting. Leaving them unsecured simply expands the attack surface. MITRE ATLAS provides the threat landscape language; ISO/IEC 27090 is the guidance to start aligning with. Better to use the technology deliberately than get left behind.

## References

- MITRE ATLAS (Adversarial Threat Landscape for Artificial-Intelligence Systems)  
- ISO/IEC 27090 — guidance on AI cybersecurity risks
