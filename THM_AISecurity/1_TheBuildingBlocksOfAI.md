# TryHackMe - The Building Blocks of AI

**Platform**: TryHackMe  
**Difficulty**: Easy  
**Category**: AI Security  
**Date**: 10 OCT 2026  
**Time spent**: ~1 hour (including write-up)  
**Tags**: `#AI` `#MachineLearning` `#PromptEngineering`

---

## Summary

This is an entry-level room covering the fundamental building blocks of Artificial Intelligence and Machine Learning. You explore foundational ML mechanics, neural architectures, and how modern Large Language Models (LLMs) operate and consume structured data.

## Key Takeaways

- **Pattern recognition and syntax match are critical**: LLMs do not "think" like humans; they track probabilistic weightings and structural cues. Adhering closely to expected formatting prevents prompt drifting and hallucinations.
- **Learn model-friendly markup**: Structuring prompts and classification inputs using standardized encoding—such as clean Markdown headers, delimiter tags (`###`, `---`), or schemas like JSON/YAML—significantly improves model parsing reliability, token boundary comprehension, and response accuracy.

---

## AI Agents

Each agent has a specific operational workflow:

- Target IP / hostname
- AI Agent interaction
- Natural language interface that adapts and presents escalating resistance through each tier
- 8 tasks in total

---

## Learning Objectives & Tasks

### Task 1 – Intro
Sets the overall scope and foundational goals for the course.

### Task 2 – Introducing THM’s AI Agent Platform
Explains the challenge infrastructure and interactive agent workflow.

### Task 3 – What is AI and Machine Learning
- **Machine Learning (ML)** is a subfield of Artificial Intelligence. Software identifies patterns, learns relationships from sample data, and generates predictions without hardcoded logic.
- **Overfitting**: Occurs when a model memorizes its training distribution so tightly that it fails to generalize to unseen data.

### Task 4 – Machine Learning Algorithms
ML models systematically optimize objective metrics through an iterative loop:

1. Decision Process
2. Error Function (Loss computation)
3. Model Optimisation Process (Gradient updates)

**Four main categories of ML algorithms**:
- Supervised Learning
- Unsupervised Learning
- Semi-supervised Learning
- Reinforcement Learning

### Task 5 – Neural Networks and Deep Learning
Deep Learning uses multilayered artificial neural networks inspired by biological synapses.

**Key architectural components**:
- Input Layer
- Hidden Layers
- Weights and Biases
- Output Layer

Deep Learning models contain multiple hidden processing layers (typically greater than three), eliminating manual feature engineering by deriving features directly from raw input.

### Task 6 – Large Language Models (LLMs)
Modern generative LLMs are scaled transformer architectures that predict token sequences based on learned multi-dimensional patterns.

| Concept | Description |
| :--- | :--- |
| **Pre-Training** | Unsupervised ingestion of web-scale text corpora to build broad language representations. |
| **Parameters** | The adjustable weights distributed across layers that store the model's linguistic and factual knowledge. |
| **Backpropagation** | Computes the loss gradient across layers to adjust parameter weights during training. |
| **Transformers** | Architectures utilizing self-attention mechanisms to process tokens simultaneously rather than sequentially. |
| **Attention** | Dynamically calculates contextual relevance scores between disparate tokens in a sequence. |
| **RLHF** | Fine-tunes model behavior using human ranking and preference scoring. |

### Task 7 – Practical
Hands-on application and interaction against the live THM agents.

### Task 8 – Conclusion
Wrap-up of fundamental principles and introduction to subsequent modules.

---

## Practical Walkthrough – Neuron-1

**Goal**: Train and guide the agent toward accurate classification by supplying structured, consistent training points.

### Steps

1. **Pick a domain-specific problem**: Spam / Scam Email Classification.
2. **Standardize the schema**: Supply structured inputs with clear delimiters, label definitions, and features.
3. **Iterate on edge cases**: Refine inputs when ambiguous phishing hooks cause misclassifications.
4. **Retrieve completion flag**: Extract the validation flag once target accuracy is reached.

> **Warning**: Use original training examples and data points. Hardcoded or duplicated examples undermine the exercise.

### Example Data Used

**Topic**: Spam / Scam Email Classification

**Input Example**: Debt Relief! We are here to be your partner in debt relief, Join us for Immediate relief.Get the FREEDOM you deserve, contact us NOW!

**Extracted Features**:
- All-caps words: `"NOW"`, `"FREEDOM"`
- Multiple exclamation marks (`!`)
- Urgency language: `"Immediate"`, `"NOW"`
- Call to action: `"contact us NOW"`
- Repetition: `"debt relief"` ×2, `"relief"` ×3
- No company name, no salutation, no verifiable details
- Poor punctuation / spacing: `"relief, Join"`, `"relief.Get"`

**Recognized Patterns**:

| Pattern | Description |
|---------|-------------|
| Pattern 1 | All-caps emphasis → Shouting effect; low-effort manipulation |
| Pattern 2 | Excessive punctuation → Manufactured excitement / urgency |
| Pattern 3 | Urgency pressure → Forces action before the reader can verify |
| Pattern 4 | Direct CTA → Single immediate action, no alternative |
| Pattern 5 | Emotional bait → Appeals to desire / entitlement, not logic |
| Pattern 6 | Keyword stuffing → Repetition fills space; signals template / bulk content |
| Pattern 7 | Poor grammar / spacing → No human proofreading; automated or low-quality |

**Classification**:  
Spam / Scam (lead-generation type, **not** credential-stealing phishing).  
Goal is to harvest contact information from financially distressed recipients.
