# TryHackMe - Fool's Mate

**Platform**: TryHackMe  
**Difficulty**: Easy  
**Category**: Web Exploitation  
**Date**: 28 OCT 2026  
**Time spent**: ~15–30 minutes (including write-up)  
**Tags**: `#ClientSideValidation` `#JavaScript` `#WebExploitation` `#BurpSuite` `#TryHackMe`

---

## Summary

Short web challenge themed around a chess “Endgame Trainer.” The board shows a clear mate-in-one position, but the application blocks the winning move with a fake warning. The room teaches a core web security lesson: **never trust client-side validation**.

## Key Takeaways / Personal Takeaways

- Security decisions made only in the browser can always be bypassed.
- Client-side checks (JavaScript) are useful for user experience, but they must never be the only control.
- Always inspect JavaScript source, network requests, and API endpoints.
- The correct way to enforce rules is on the server side.
- Common bypass techniques: modify/remove the client-side check, use browser DevTools, or send the request directly to the API (Burp Suite / curl).

---

## Learning Objectives

- Identify client-side validation logic
- Understand the difference between client-side and server-side enforcement
- Bypass JavaScript restrictions to interact directly with the backend
- Capture the flag by submitting a valid move that the client tries to block

---

## Learning Objectives & Tasks

### Task 1 – Fool's Mate

**High-level path:**

1. Open the web application and examine the chess board (mate-in-one position).
2. Attempt the obvious winning move → the application blocks it with a warning message.
3. Inspect the page source / JavaScript files (especially `app.js`). 
4. Go to the Network tab and observe what happens with you move the chess piece. 
5. Bypass the restriction using one of the following methods:
   - By right clicking on the post you can make certain edits, the allows me to test various moves.
   - You can send the correct response.
6. The server accepts the move, confirms checkmate, and returns the flag.

---

## Practical Notes

- Look for functions that evaluate moves locally before sending them to the server.
- Useful tools: Browser DevTools (Sources + Network tabs)
- Key lesson: If the restriction only exists in JavaScript, it does not exist for an attacker.

---

## References

- TryHackMe room: https://tryhackme.com/room/foolsmate
- Related rooms: https://tryhackme.com/room/axss, https://tryhackme.com/room/javascriptessentials, https://tryhackme.com/room/dombasedattacks
