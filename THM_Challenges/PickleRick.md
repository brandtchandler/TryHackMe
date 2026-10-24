# TryHackMe - Pickle Rick

**Platform**: TryHackMe  
**Difficulty**: Easy  
**Category**: Web / CTF  
**Date**: 23 OCT 2026  
**Time spent**: 1.5 hours (including write-up)  
**Tags**: `#PickleRick` `#WebExploitation` `#CommandInjection` `#CTF` `#RickAndMorty` `#TryHackMe`

---

## Summary

Classic beginner-friendly CTF room themed around *Rick and Morty*. Rick has turned himself into a pickle again and needs three secret ingredients to create a potion that will turn him back into a human. You must exploit a vulnerable web server to find all three ingredients.

## Key Takeaways / Personal Takeaways

- Using tools like nmap used to find key information.
- Check page source — credentials and useful hints are frequently left there.
- Directory enumeration (Gobuster / dirb / ffuf) is essential on web challenges.
- Restricted command execution panels often block common tools (`cat`, `head`, etc.). Alternative commands such as `less`, `more`, `tac`, or `strings` frequently work.
- check `sudo -l` (or simply try `sudo`) once you have a shell or command execution — misconfigured sudo is a common privilege escalation path.
- The room is short but covers a clean progression: recon → foothold → privilege escalation.

---

## Learning Objectives

- Perform basic port and directory enumeration
- Analyse web page source and robots.txt for credentials/hints
- Exploit a restricted command execution interface
- Escalate privileges using sudo misconfigurations
- Locate and retrieve the three required ingredients

---

## Learning Objectives & Tasks

### Task 1 – Pickle Rick

Single-task room with three questions (the three ingredients).

**High-level path:**

1. **Reconnaissance**
- Nmap scan reveals open ports (typically 22 and 80)
- Browse the website and view page source → find username
- Check `/robots.txt` → find password

2. **Foothold**
- Log in to the command panel (`/login.php` → `/portal.php`) using the discovered credentials
- Gain access to a restricted web-based command execution interface

3. **First Ingredient**
- List files in the web root
- Read the ingredient file using an allowed command (`less`, `tac`, `strings`, etc.) because `cat` is blocked

4. **Second Ingredient**
- Navigate the filesystem (`/home/rick/`)
- Read the second ingredient file (again using allowed commands)

5. **Third Ingredient (Privilege Escalation)**
- Discover that the current user can run commands as root via `sudo` without a password
- Use `sudo` to read the final ingredient file located in `/root`

---

## Practical Notes

- Useful commands when `cat` is blocked: `less`, `more`, `tac`, `strings`, `nl`, `od`
- Check for sudo privileges early: `sudo -l` or simply try `sudo ls /root`
- Keep notes of every file and directory you discover — the ingredients are often named in an obvious way once you find them

---

## References

- TryHackMe room: https://tryhackme.com/room/picklerick
