# TryHackMe — Prompt Engineering

**Platform**: TryHackMe  
**Difficulty**: Easy  
**Category**: AI Security  
**Date**: 12 OCT 2026  
**Time spent**: ~2 hours (including write-up)  
**Tags**: `#AI-models` `#MachineLearning` `#cybersecurity` `#black-box` `#PromptEngineering`

Room focused on the practical mechanics of driving LLMs: tokens, generation parameters, prompt structure, the system/user instruction hierarchy, and advanced techniques. Shifts from pure architecture/data concerns into how you actually control model behaviour — and where that control breaks for security.

## Overview

This room teaches how to get reliable, useful output from LLMs while highlighting the security implications of how those models actually work. The core security thread is the fragility of the system/user instruction hierarchy — the conceptual foundation for prompt injection that later rooms build on.

## Learning Objectives

- Explain tokenization and LLM nondeterminism (and why both matter for security testing)
- Tune generation parameters: temperature, max tokens, top-p
- Construct prompts using the four pillars
- Understand the system vs. user prompt hierarchy and its practical limits
- Apply few-shot and Chain-of-Thought techniques to security-relevant tasks

## Task Index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Sets objectives and vocabulary; assumes AI/ML Security Threats fundamentals |
| 2 | LLM Fundamentals | Tokenization, nondeterminism, temperature / max tokens / top-p, context window |
| 3 | The Anatomy of a Prompt | Four pillars: instruction, context, output format, constraints |
| 4 | System vs. User Prompts | Instruction hierarchy and why it is only probabilistic |
| 5 | Advanced Prompting Techniques | Shot spectrum, Chain-of-Thought, prompt templates |
| 6 | Challenge | Hands-on PromptSec graded exercise |
| 7 | Conclusion | Recap and bridge to later rooms |

## Key Concepts

**Tokenization**  
Tokens are the units LLMs actually process — roughly 3–4 characters each. English words are usually 1–2 tokens. Models convert text into numerical token IDs and then predict the next ID. Different models use different schemes (GPT = Byte-Pair Encoding, BERT = WordPiece), so the same sentence can produce different token counts. This directly affects cost and context budgeting.

**Nondeterminism**  
Unlike traditional software, the same input can produce different outputs. This is both intentional (controlled by temperature/top-p) and inherent. From a security perspective this is critical: a defence or filter that stops a malicious prompt once may fail on the next attempt. Adversarial testing therefore has to be probabilistic, not one-shot.

**Generation parameters**  
- **Temperature** (0.0–2.0): the randomness dial. Low = focused/precise; high = more adventurous.  
- **Max tokens**: hard length/cost ceiling.  
- **Top-p** (nucleus sampling): alternative randomness control — restrict or expand the shortlist of candidate tokens.  
Recommendation: adjust one or the other, not both. Temperature is usually enough; reach for top-p when you specifically need creativity.  

**Context window**  
The model’s working memory. Exceed it and earlier parts of the conversation are dropped. Modern models range from ~8k tokens up to 1M+.

**Four pillars of a prompt**  
1. Instruction / task (clear verb-driven command)  
2. Context (background, audience, domain details, tone)  
3. Output format (structure, length, language, code style)  
4. Constraints (rules, limits, what *not* to do)  

Specificity beats both vagueness and pure verbosity. Define inputs, checks, and expected outcome so the model has less room to guess.

**System vs. user hierarchy**  
System prompts set persistent role, tone, and hard rules. User prompts supply the actual task. In theory the model respects the hierarchy; in practice everything is just one undifferentiated token stream. That makes the boundary probabilistic rather than guaranteed — the root of prompt injection.

**Advanced techniques**  
- **Zero-shot**: task only, no examples.  
- **One-shot / Few-shot**: 1–5 examples so the model can pattern-match (in-context learning).  
- **Chain-of-Thought**: force intermediate reasoning steps (“Let’s think step by step”). Works best on larger models (~100B+ parameters). Smaller models often produce coherent-looking but incorrect chains.  
- **Prompt templates**: reusable structures for recurring tasks and team consistency.

## Skills & Mapping

tokenization · parameter tuning · prompt design · instruction hierarchy · few-shot / CoT

Useful role mappings:  
- Prompt engineer / AI app developer → parameters, four pillars, templates  
- AI red-teamer / LLM pentester → hierarchy fragility and nondeterminism  
- AI-augmented SOC analyst → CoT for log and incident triage

## Personal Takeaways

The “black box” nature of these models means we can influence behaviour through prompts and parameters, but we rarely fully understand the internal state. That same opacity creates security surface: nondeterminism, soft instruction boundaries, and the permanent embedding of training data (including PII or credentials that cannot be cleanly removed later). Fine-tuning inherits everything from the base model — biases, vulnerabilities, and weakened safety alignment — so evaluation and ongoing testing become essential rather than optional.

## References

- OWASP Top 10 for LLM Applications: https://genai.owasp.org/  
- Chain-of-Thought prompting paper: https://arxiv.org/abs/2201.11903
