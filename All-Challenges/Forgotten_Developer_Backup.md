# Forgotten Developer Backup

**Category**: Sensitive Data Exposure  
**Difficulty**: 3.5
**Description**:  
Find and access a forgotten backup file containing potentially sensitive information.

---

**Solution**:  
While bypassing extension filtering for the Poison Null Byte challenge, I was able to access `package.json.bak`, a backup file that was not intended to be public.

---

**Steps**:

1. I discovered a `/ftp` directory using **Gobuster**, which revealed the existence of several `.bak` files.

2. Direct requests to these files resulted in a `403 Forbidden` response, due to an enforced extension filter that only allows `.md` and `.pdf` files:
403 Error: Only .md and .pdf files are allowed
3. Using **Burp Suite**, I intercepted the request to:
/ftp/package.json.bak
4. and modified the URL to:
/ftp/package.json.bak%2500.md

5. This double-encoded null byte (`%2500`) bypassed the file extension filter, and the server responded with the actual contents of the `.bak` file.
 
6. Accessing the backup file completed the **Forgotten Developer Backup** challenge.
