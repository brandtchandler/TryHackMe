# TryHackMe - Neighbour

Platform: TryHackMe
Difficulty: Easy / Info
Category: Web Application Security
Target Vulnerability: Insecure Direct Object Reference (IDOR)
Author: cmnatic
Tags: #WebSecurity #IDOR #AccessControl #TryHackMe #Walkthrough

---

## Room Summary

Neighbour is a beginner-focused web challenge designed to demonstrate a classic Insecure Direct Object Reference (IDOR) vulnerability. The objective is to exploit a broken access control mechanism in a simple user portal to access an administrative profile and retrieve the hidden flag.

---

## Technical Details

| Metric | Detail |
| :--- | :--- |
| Vulnerability Class | Broken Object Level Authorization / IDOR |
| Attack Vector | HTTP GET Parameter Manipulation |
| Parameter | ?user= |
| Privilege Escalation | guest (low privilege) to admin (privileged) |

---

## Walkthrough

### 1. Initial Reconnaissance and Source Inspection

1. Navigate to the target web server:
   http://TARGET_IP
2. A minimalist login form is displayed with a hint prompting for shortcut (Ctrl+U).
3. This is normal text, but <span style="color: #e74c3c; font-weight: bold;">this alert is bright red</span>.
<span style="color: red;">3. View the HTML page source (Ctrl + U or right-click, then View Page Source). </span> 
[!IMPORTANT]4. Near the bottom of the HTML, an unremoved developer comment discloses testing credentials and user presence:  
   use guest:guest credentials until registration is fixed. "admin" user account is off limits!!!!!

### 2. Low-Privilege Authentication

1. Return to the login portal.
2. Enter the discovered credentials:
   - Username: *****
   - Password: *****
3. Upon authentication, the web application redirects to:
   http://TARGET_IP/profile.php?user=guest

### 3. Exploiting IDOR

1. The application relies entirely on the client-supplied query parameter user=guest rather than a server-side session variable or authorization token to decide which profile record to return.
2. Modify the URL parameter directly in the browser address bar:
   http://TARGET_IP/profile.php?user=admin
3. Submit the request. The server renders the administrator profile and displays the flag:
   flag{...}

---

## Key Takeaway

Authentication verifies who a user is; authorization enforces what that user can see or execute. Applications should never trust user-controllable GET/POST parameters to serve sensitive user-specific data without validating the requested object against the active authenticated session on the server side.
