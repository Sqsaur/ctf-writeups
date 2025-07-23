# Security Policy

**Category**: Miscellaneous  
**Difficulty**: 2

**Description**:  
Behave like any “white-hat” should before getting into the action.

---

**Solution**:  
This challenge was solved by discovering and accessing the `.well-known/security.txt` file.

---

**Steps**:

1. I launched a directory brute-force scan using **Gobuster** with a filter to exclude common false positives:
   
   ```bash
   gobuster dir -u http://127.0.0.1:3000 -w /usr/share/seclists/Discovery/Web-Content/common.txt -o xxx.txt --exclude-length 80117
   The scan returned a valid entry:
   .well-known/security.txt
   I navigated to the discovered endpoint in the browser:
   http://127.0.0.1:3000/.well-known/security.txt
   ```

**"Challenge solved!"** popup confirmed that the challenge was completed.