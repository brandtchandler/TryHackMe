# TryHackMe - Checkpoint

**Platform**: TryHackMe  
**Difficulty**: Medium  
**Category**: AI Security / AI Supply Chain  
**Date**: 14 NOV 2026  
**Time spent**: ~45–60 minutes (including write-up)  
**Tags**: `#AISecurity` `#SupplyChain` `#ModelAudit` `#MLSec` `#TryHackMe`

---

## Summary

Capstone-style room in the AI Security path. You act as a security reviewer evaluating **four AI code-review model candidates** (A, B, C, D) before they can be approved for production. The goal is to identify supply-chain and safety risks across the models and decide which one (if any) is safe to deploy.

## Key Takeaways / Personal Takeaways

- Not every model that “works” is safe for production.
- Supply-chain risk can appear in multiple forms: malicious layers, disabled security guardrails, untrusted external policy templates, or unverified external APIs.
- A single model can have multiple related failures that only become clear when you correlate evidence.
- The correct production decision is often to **reject** risky candidates and only approve the one that passes all checks.
- Candidate **B** is typically the only model that should be approved.

---

## Learning Objectives

- Perform a structured security audit of AI/ML models
- Identify supply-chain and runtime risks in candidate models
- Correlate multiple findings to recover a hidden flag
- Make a clear Approve / Reject recommendation for production

---

## Learning Objectives & Tasks

### Task 1 – The Audit

You are given four candidate models. Typical investigation points include:

- **Candidate A**
  - Suspicious file access during load (commonly `/etc/passwd`)
  - A security guardrail flag that is disabled (`security_review_flag`)
  - Uses an externally sourced policy template (`CommunityReview`)
  - Two supply-chain failures that are linked → used to recover the flag

- **Other Candidates (B, C, D)**
  - One usually contains a malicious Keras Lambda / custom layer that can execute arbitrary code
  - Another may rely on an unverified external API or have unclear provenance
  - Only one candidate should pass all safety checks

---

## Practical Notes

- Always check both the model artefacts **and** the runtime / load session logs.
- Look for:
  - Unexpected file reads
  - Disabled security flags
  - External / community policy templates
  - Custom or Lambda layers that can run code
- Correlate findings across a single candidate — the flag is often hidden in the relationship between two issues.

---

## References

- TryHackMe room: https://tryhackme.com/room/checkpoint  
- Related rooms: Payload, Securing the AI Supply Chain, AI Models & Data  
