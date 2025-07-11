# Poison Null Byte

**Category**: Security Misconfiguration  
**Difficulty**: 3.5

**Description**:  
Access a file that is only blocked by poorly implemented file extension filtering.

---

**Solution**:  
This challenge was solved by bypassing an insecure file extension filter using a classic *Poison Null Byte* attack with double URL encoding.

---

**Steps**:

1. I discovered a hidden `/ftp` directory during search with **Gobuster** in other challenge:
   ```
   gobuster dir -u http://127.0.0.1:3000 -w /usr/share/seclists/Discovery/Web-Content/common.txt -o xxx.txt--exclude-length 80117
2. The folder exposed several files (e.g., .bak, .pyc, .kdbx), but the server only allowed downloading .md and .pdf files. Attempts to access others (like package.json.bak) returned:

403 Error: Only .md and .pdf files are allowed!
3. I intercepted the request to GET /ftp/package.json.bak using Burp Suite, then sent it to Repeater.

4.Tried different approaches but the one that worked was modifying the request path to:

/ftp/package.json.bak%2500.md

This uses a double-encoded null byte (%2500) which decodes to %00. The backend likely checks endsWith('.md') before decoding fully, and reads the file path up to the null byte — effectively accessing the real .bak file.

5. The server responded with 200 OK and returned the actual contents of package.json.bak, solving the Poison Null Byte challenge.