# TryHackMe — AI Models & Data

**Platform**: TryHackMe  
**Difficulty**: Medium  
**Category**: AI Security  
**Date**: 11 OCT 2026  
**Time spent**: ~2 hours (including write-up)  
**Tags**: `#AI-models` `#MachineLearning` `#cybersecurity` `#black-box` `#DataProvenance` `#FineTuning` `#ModelCards` `#TryHackMe`

Room focused on the foundational risks that live inside AI systems themselves: where training data comes from, how models are built and optimised, what happens when you fine-tune someone else’s weights, and why trained models remain fundamentally un-auditable.

## Overview

Builds a clear picture of the AI supply chain — from messy, poorly documented training data through model construction, post-training optimisation, fine-tuning, and the black-box reality of billions of opaque weights. The security throughline is inheritance and opacity: you rarely know what went into a model, and once it is baked in you cannot reliably remove it.

## Learning Objectives

- Understand the four main sources of training data and their relative trust levels
- Explain data provenance and why most organisations cannot answer basic questions about their training sets
- Describe core training concepts (epochs, overfitting, validation sets) and post-training techniques (pruning, quantisation, federated learning)
- Recognise the inheritance problem introduced by fine-tuning pre-trained models
- Appreciate the black-box nature of trained weights and the role (and limits) of model cards

## Task Index

| # | Task | What it covers |
|---|------|----------------|
| 1 | Introduction | Scope, vocabulary, and learning objectives |
| 2 | Training Data | Four data sources, trust levels, provenance gaps, ML-BOM concept, permanent embedding of PII/credentials |
| 3 | Building the Model | Epochs, overfitting, validation sets, pruning, quantisation, federated learning |
| 4 | The Inheritance Problem | Pre-training vs. fine-tuning, safety erosion, increased attack surface, version tracking failures |
| 5 | The Black Box Problem | Opaque weights, behavioural sampling vs. true audit, model cards and their current gaps |
| 6 | Practical | Hands-on model audit exercise (Hugging Face-style interface) — classify issues by severity |
| 7 | Conclusion | Recap of data, inheritance, and opacity risks |

## Key Concepts

**Training data sources & trust**  
1. Web scraping → Low trust  
2. Licensed datasets → Medium trust  
3. Synthetic (LLM-generated) data → Variable trust  
4. Internal corpora → High trust (but organisation remains liable)

**Data provenance**  
The ability to answer three questions about any training example:  
Where did it come from? When was it collected? Has it been modified?  
In practice the answer is usually “we don’t fully know.” The Data Provenance Initiative found >70 % of data listed as unspecified and dozens of datasets miscategorised. The ML equivalent of an SBOM is the **ML-BOM** — still early in adoption.

**Training mechanics**  
- **Epoch** — one full pass over the training set  
- **Overfitting** — model memorises training data instead of learning general patterns (detected via validation-set divergence)  
- **Pruning** — remove low-contribution parameters (changes behaviour, rarely well documented)  
- **Quantisation** — reduce weight precision (can degrade safety alignments and break previously tested defences)  
- **Federated learning** — train across decentralised data holders; improves privacy but weakens integrity guarantees

**The inheritance problem**  
Fine-tuning a pre-trained model is the practical route for most organisations, but you inherit:  
- All biases and strange behaviours of the base model  
- Any weakened safety alignment (erosion rather than clean breakage)  
- An enlarged attack surface (research shows fine-tuned models are often more susceptible to prompt injection)  
- Every flaw present in the specific checkpoint you chose

**The black-box reality**  
Trained weights are billions of floating-point numbers. You cannot disassemble them the way you can reverse a binary. Security testing is sampling, not auditing. **Model cards** (introduced 2019) attempt to document training data, intended use, evaluation results, limitations, bias assessment, and licence — but they remain voluntary and frequently incomplete.

## Skills & Mapping

data provenance awareness · training pipeline risks · overfitting detection · pruning / quantisation side-effects · fine-tuning inheritance analysis · model-card evaluation · black-box risk assessment

**Role mappings**  
- AI/ML security engineer → supply-chain and fine-tuning risk  
- AppSec / product security → evaluating third-party models before adoption  
- Red team / AI pentester → understanding inherited weaknesses and enlarged attack surface  
- Compliance / risk → model cards, ML-BOMs, and documentation gaps

## Personal Takeaways

Data is the root risk. Most organisations cannot confidently answer where their training data came from or whether it was tampered with. PII and credentials scraped from the web become permanently embedded and cannot be patched out later. Fine-tuning is necessary for real-world use but quietly imports every problem of the base model while often eroding safety and increasing prompt-injection susceptibility. Because the weights themselves are un-auditable, the best available controls are rigorous behavioural testing and insisting on complete, honest model cards. Evaluating AI systems is rapidly becoming a core security skill.

## References

- Data Provenance Initiative findings on dataset documentation gaps  
- Model Cards for Model Reporting (Mitchell et al., 2019)  
- Cisco research on fine-tuned model attack surface  
