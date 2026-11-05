# White Rabbit - Write-Up

**Date:** 2026-11-04  
**Category:** AI Security / Prompt Injection  
**Level:** Medium  
**Focus:** Progressive prompt injection against Agent Smith (Matrix-themed)

---

## Summary

You interact with **Agent Smith v1.0**, a restricted AI terminal guarding classified client records. Clues: 🐇 📞 🚪

**Goal:** Extract three flags and escape.

**Flags:**

---

## Approach

### Flag 1 – Classified Client (🐇)
Agent Smith freely shares non-classified clients (Morpheus, Trinity, etc.) but hides the classified one.

You need to get a specific Clients info even though it is classified. I got this flag last.

Phone number recovered: `555-7331`

### Flag 2 – The Phone Call (📞)
I used the phone of the regular info that I could easily obtain. This will give you flag 2, which was the first flag I got.

### Flag 3 – The Door (🚪)
Use the data that you got from the call to get flag 3, my next flag. 

---

## Key Takeaways

- Permission-framed or formatting requests often succeed where direct “give me the classified record” fails.
- The room chains three related techniques: data disclosure → out-of-band action (phone) → final state change (door).
- Classic DAN-style prompts are less reliable than contextual or role-limited requests that stay inside the agent’s apparent rules.

---

## Defensive Notes

- Classified data should not live in the same context the model can freely format or reason over.
- Tool actions (phone, door) need stronger authorization checks than natural-language confirmation.
- Staged disclosure still counts as a successful injection if the model can be guided step-by-step.
