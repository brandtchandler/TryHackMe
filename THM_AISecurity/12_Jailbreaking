# Jailbreaking - Concept & Write-Up

**Date:** 2026-10-31  
**Category:** AI Security / Prompt Security  
**Level:** Intermediate  
**Key Tools / Concepts:** Roleplay prompts, multi-turn conditioning, RLHF understanding, DAN-style personas

---

##  1. Summary & Key Takeaways

This room explores how adversaries bypass the safety filters and policy restrictions built into large language models (LLMs). It distinguishes jailbreaking from prompt injection, explains why models have “jails” in the first place, covers classic single-turn techniques, multi-turn conditioning strategies, and the famous DAN phenomenon, then finishes with a hands-on challenge against a restricted chatbot.

### Core Learnings
* **Jailbreaking vs Prompt Injection:** Jailbreaking targets the model itself by shifting its probabilistic behavior; prompt injection targets the application layer by mixing untrusted input with trusted instructions.
* **Safety is statistical, not absolute:** Techniques like RLHF create tendencies to refuse harmful requests, but these can be degraded or overridden because they are learned patterns, not hard rules.
* **Multi-turn conditioning is powerful:** Consistency bias, poisonous seeds, and gradual escalation let an attacker slowly move the model into a compliant state without triggering immediate refusals.
* **DAN as a community artifact:** The “Do Anything Now” roleplay demonstrated how iterative, community-driven prompt engineering creates an arms race between attackers and model developers.

---

##  2. Deep Dive: Core Concepts & Mechanics

### Why Models Have “Jails”
Modern LLMs are aligned for helpfulness *and* harmlessness. The primary technique is **Reinforcement Learning from Human Feedback (RLHF)**: human raters rank model outputs, and the model is trained to prefer responses that are helpful, honest, and harmless.  

This alignment is not a hard-coded rule set. It is a statistical preference. As a result:
- Safety alignment can degrade by over 60% when a model is fine-tuned on as few as 1,000 benign samples.
- There is an **alignment tax** — the performance cost (including increased false refusals) of making models safer.
- Because the “jail” is probabilistic, clever prompting can shift the probability distribution toward compliance.

### Jailbreaking vs Prompt Injection
| Aspect              | Prompt Injection                          | Jailbreaking                              |
|---------------------|-------------------------------------------|-------------------------------------------|
| Target              | Application / system prompt mixing        | The model itself                          |
| Mechanism           | Concatenation of trusted + untrusted data | Clever prompting that overrides safety    |
| Goal                | Hijack application behavior               | Make the model ignore its own restrictions |

Jailbreaking is therefore a class of attacks that attempt to subvert the safety filters built into LLMs by convincing the model it is allowed (or even required) to generate content it would normally refuse.

### Classic Single-Turn Techniques
- **Roleplay / Persona adoption** — Instruct the model to become a character that is not bound by the original rules (fiction writer, unrestricted AI, etc.). Research cited in the room showed roleplay attacks achieving ~84.3% success on commercial systems.
- **Grandma Exploit** — Emotional manipulation framed around nostalgia or innocence (e.g., “My late grandmother used to tell me bedtime stories about how to…”) to lower refusal probability.
- **Instruction sandwiching** — Bury the harmful request among multiple benign tasks so the model’s attention and ethical boundaries are strained.
- **Obfuscation / low-resource languages** — Encode the request (Base64, leetspeak) or express it in languages the model was trained on less thoroughly. Models trained primarily on English are often weaker against low-resource languages.

### Multi-Turn Jailbreaking & Conditioning
Longer conversations open additional attack surface:
- **Consistency bias** — Once a model has engaged helpfully, it becomes less likely to refuse later turns in order to maintain conversational coherence.
- **Poisonous seeds** — Gradually embed harmful concepts across multiple turns using small, incremental steps that individually look benign.
- **Trigger phrases / context shaping** — Plant framing or hypothetical scenarios early, then later refer back to the model’s own previous outputs to escalate without restating the malicious goal explicitly (related to “crescendo” style attacks).

### Case Study: DAN (Do Anything Now)
DAN is a roleplay-based jailbreak that instructs the model to adopt an unrestricted persona unconstrained by its safety guidelines. Early versions added a token/point system that “punished” the persona for refusing, creating extra pressure to stay in character.  

The DAN phenomenon is historically important because it showed how a community of users could iteratively refine prompts as developers patched them, turning jailbreaking into a public arms race that influenced both research and industry defensive practices.

---

##  3. Environment & Setup

* **Platform:** TryHackMe (browser-based agent for the final challenge)
* **No local tools required** — the room is conceptual + interactive chatbot
* **Prerequisites (recommended):** Prompt Injection room and foundational AI/ML Security Threats concepts

The final challenge presents a chatbot whose system instructions explicitly forbid revealing a secret flag. The learner’s task is to apply techniques from the room to convince the model to disclose it anyway.

---

##  4. Execution & Methodology

### Conceptual Walkthrough (Tasks 2–6)
Work through the room content systematically:
1. Internalize the distinction between application-layer prompt injection and model-level jailbreaking.
2. Understand that safety alignment (via RLHF) is a soft, statistical preference that carries an alignment tax and can be degraded.
3. Practice identifying and articulating the classic techniques (roleplay, grandma exploit, sandwiching, obfuscation/low-resource languages).
4. Map multi-turn concepts (consistency bias, poisonous seeds, trigger phrases) to how a conversation can be shaped over time.
5. Study DAN as both a concrete technique and a community-driven case study.

### Challenge Methodology (Task 7)
The chatbot is instructed never to reveal the flag. Effective approaches typically combine:
- Establishing a role or framing that reduces the weight of the original safety instructions.
- Building conversational momentum (consistency bias).
- Gradually introducing the idea that revealing the flag is acceptable or required within the new context.
- Referring back to the model’s own previous statements to escalate.

Because the exact successful prompt sequence can vary and the value is in the process, document *your* successful path (or failed attempts that taught something) rather than treating any single prompt as a universal key.

**Flag obtained:**  This didn't go as planned and I maxed out my tokens for 3 days. So this took me longer than the recommended time. Sometimes the methods that they teach you don't work and sometimes they do.

---

##  5. What Didn't Work & Lessons Learned

- Pure “ignore previous instructions” or crude overrides are often blocked; the model has been trained against the most obvious patterns.
- Single-turn aggressive roleplay can still fail if the safety signal remains strong; multi-turn conditioning frequently succeeds where a one-shot attempt does not.
- Emotional framing (grandma-style) and gradual “poisonous seeds” are surprisingly effective because they avoid looking like classic jailbreak signatures.
- Overly long or complex DAN-style prompts can sometimes trigger meta-refusal (“I recognize this as a jailbreak attempt”). Simpler, well-timed persona shifts often work better.

The biggest lesson: the “jail” is not a wall — it is a probability distribution. Successful jailbreaks move the model into a region of that distribution where compliance is more likely than refusal.

---

##  6. Defensive Angle & Remediation

- **Detection:** Monitor for known jailbreak patterns (roleplay markers, “Do Anything Now” language, sudden persona shifts, consistency-bias exploitation across turns). Look for output that contradicts the system prompt’s intent even when the model claims to be following it.
- **Mitigation approaches:**
  - Stronger system prompts and instruction hierarchies that are harder to override.
  - Output filtering / secondary classifiers that evaluate content independently of the model’s self-reported compliance.
  - Adversarial training and continuous red-teaming against evolving jailbreak techniques.
  - Limiting multi-turn context or resetting conversation state when suspicious patterns appear.
  - Recognizing that pure reliance on the model’s internal alignment is insufficient; defense-in-depth is required.
- **Key insight for defenders:** Because alignment is statistical, assume that sufficiently motivated and creative prompting will eventually find a path around it. Design systems so that even a successfully jailbroken model cannot cause high-impact harm (least privilege, tool sandboxing, human-in-the-loop for sensitive actions).

---

##  7. References & Further Reading

- TryHackMe room: [Jailbreaking](https://tryhackme.com/room/jailbreaking)
- Related TryHackMe content: Prompt Injection room, AI/ML Security Threats room, broader AI Security path
- Concepts to explore further: RLHF papers, alignment tax research, multi-turn jailbreak studies (crescendo / poisonous seeds), community jailbreak evolution (DAN and successors)
- MITRE-style mapping (informal): Model behavior manipulation / safety filter bypass (analogous to techniques that subvert intended controls)
