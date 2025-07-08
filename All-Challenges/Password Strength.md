# Password Strength

**Category**: Broken Authentication  
**Difficulty**: 2.5

**Description**:  
Log in with the administrator's user credentials without previously changing them or applying SQL Injection.

---

**Solution**:  
This challenge was completed by logging in with the default administrator credentials that hadn’t been changed.

---

**Steps**:  
Started by inspecting `main.js` and running LinkFinder to identify interesting routes and endpoints. While reviewing JWT tokens in Local Storage after a regular login, it became clear how user session data is handled.

A quick test using common default credentials — `admin@juice-sh.op` / `admin123` — gave access to the administrator account without any need for password reset or injection techniques.

Also confirmed that a SQL injection like `' or 1=1--` works on the login form, although it's not required to solve this particular challenge.

---

**Result**:  
Successfully logged in as the administrator. The app confirmed the solution with a **"Challenge solved!"** notification.
