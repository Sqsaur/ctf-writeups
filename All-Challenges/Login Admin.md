# Login Admin

**Category**: Authentication  
**Difficulty**: 2

**Description**:  
Log in with the administrator's user account.

---

**Solution**:  
I managed to log in using two different methods:  
1. Default credentials  
2. SQL Injection

---

**Steps**:

### Method 1: Default Credentials  
1. I tested if the default admin login was still enabled.  
2. I used:
- **Email**: `admin@juice-sh.op`
- **Password**: `admin123` (ppl still use this as a password really)
3. This successfully logged me in as the administrator.

### Method 2: SQL Injection  
1. Attempted a basic SQL injection on the login form to bypass authentication.  
2. Used the following input:
- **Email**: `' OR 1=1--`  
- **Password**: `anything`
3. This also resulted in a successful login — I was granted access without valid credentials.

---

**Result**:  
In both cases, a **"Challenge solved!"** popup confirmed that the challenge was completed.

