# Error Handling

**Category**: Improper Error Handling  
**Difficulty**: 2.5

---

**Description**:  
Provoke an error that is not very gracefully handled.

---

**Solution**:  
While exploring hidden paths in the application, I stumbled upon an endpoint that triggered a raw server-side error message with a full stack trace.

---

**Steps**:  
1. I used **ffuf** to fuzz for potential hidden endpoints.  
   Command I ran:
   `ffuf -u http://localhost:3000/FUZZ -w /usr/share/wordlists/dirb/common.txt -mc 200,403,500`

2. During enumeration, I found the path `/rest/admin`.  
3. When I accessed this URL in the browser, it immediately returned a **500 Internal Server Error**.  
4. The page exposed the full internal error stack trace from the server.

---

**Result**:  
The moment the error page with the stack trace was displayed, the **"Challenge solved!"** popup appeared, confirming completion.
