# TryHackMe - Prompt Injection

**Platform**: TryHackMe  
**Difficulty**: Medium  
**Category**: AI Security  
**Date**: 27 OCT 2026  
**Time spent**: ~2 hour (including write-up)  
**Tags**: `#PromptInjection` `#LLMSecurity` `#AISecurity` `#OWASP` `#DirectInjection` `#IndirectInjection` `#TryHackMe`

---

## Summary

Core room in the AI Security path covering one of the most important attack classes against generative AI systems: **prompt injection**. The room explains how LLMs process instructions, why the system/user hierarchy is only a soft convention, and demonstrates both **direct** and **indirect** injection techniques with real-world examples and hands-on chatbot challenges.

## Key Takeaways / Personal Takeaways

- An LLM does not truly “understand” roles or hierarchy — it only sees a single stream of tokens and predicts the next one. This is the root cause of prompt injection.
- **Direct prompt injection** places malicious instructions in the visible user input.
- **Indirect prompt injection** hides instructions in external content (documents, emails, web pages, calendar events, RAG results) that the model later ingests.
- OWASP ranks Prompt Injection as the #1 risk in the LLM Top 10.
- Real-world cases (Bing “Sydney” system prompt leak, dealership chatbot selling a car for $1, EchoLeak-style zero-click attacks) show this is a practical, high-impact issue.
- Relying only on system-prompt wording is not sufficient defence.

---

## Learning Objectives

- Understand how LLMs process context and follow (or fail to follow) instructions
- Explain what prompt injection is and why it works
- Differentiate between direct and indirect prompt injection
- Recognise real-world impact through case studies
- Apply basic injection techniques against chatbots in a controlled environment

---

## Learning Objectives & Tasks

### Task 1 – Introduction
Sets the stage for the room. Prompt injection is one of the earliest and most widely discussed AI attack types, yet it remains poorly understood by many teams.

### Task 2 – How LLMs Follow Instructions1
Keywords: System Prompts, Developer Prompts, User Prompts, Retrieved Context, Tool Outputs.
Covers fundamental mechanics:
- Context window
- System prompt vs user prompt
- Structured formats such as ChatML
- Next-token prediction

Key point: the model processes **all** input as tokens. There is no hard technical boundary between “system” and “user” instructions.

### Task 3 – What is Prompt Injection?
Defines the attack class: untrusted user input is concatenated with a trusted developer/system prompt, causing the model to follow the attacker’s instructions instead of the intended ones. Highlights that OWASP ranks it as the number-one LLM risk.

### Task 4 – Prompt Injection in Action
Walks through real incidents and demonstrates **direct** prompt injection techniques (including format-based / markup injection). Includes a hands-on challenge with a sales chatbot.

### Task 5 – Indirect Prompt Injection
Covers the more dangerous variant where malicious instructions are hidden in external content that the model later retrieves or processes. Introduces zero-click / no-interaction scenarios.

### Task 6 – Practical
Hands-on lab applying both direct and indirect techniques against live chatbots to achieve specific goals (e.g., leaking sensitive information or overriding intended behaviour).

### Task 7 – Conclusion
Recap of core concepts and bridge to defensive techniques covered in later rooms (Prompt Defence, etc.).

---

## Practical Notes

- Always start by understanding what the model can currently “see” (system prompt + conversation history + retrieved context).
- Direct injection is useful for initial testing; indirect injection is often more realistic and harder to detect.
- Format-based tricks (markdown, XML-like tags, role markers) can help instructions blend into the expected structure.
- Success is measured by behavioural change, not just by the model repeating a string.

---

## References

- TryHackMe room: https://tryhackme.com/room/promptinjectionls  
- OWASP LLM Top 10: https://genai.owasp.org/  
- Related rooms: Prompt Defence, Jailbreaking, LLM Security  
