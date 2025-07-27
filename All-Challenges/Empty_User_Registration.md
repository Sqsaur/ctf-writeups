# Empty User Registration

**Category**: Improper Input Validation  
**Difficulty**: 2

**Description**:  
The application should not allow registration of users with empty email or password fields. This challenge demonstrates a case where client-side validation prevents such input, but server-side validation is either insufficient or improperly enforced, allowing malformed input to bypass constraints.

---

**Solution**:  
The solution was achieved by intercepting the registration request and modifying the email and password fields to contain a single space character (`" "`). The server accepted this input as valid, likely due to the fact that the string was not technically empty. The frontend prevented submission with empty fields, but the backend lacked proper trimming or format validation in this edge case.

---

**Steps**:

1. Navigated to the registration page:
   
   ```
   http://localhost:3000/#/register
   ```

2. Filled out the form with dummy values to trigger a valid POST request:
   
   - Email: `dummy@juice-sh.op`
   - Password: `dummy`
   - Selected a security question and entered an answer

3. Captured the outgoing request using **Burp Suite**.

4. In **Burp Repeater**, modified the request payload:
   
   ```json
    {
      "email": " ",
      "password": " ",
      "passwordRepeat": " ",
      "securityQuestion": {
        "id": 5,
        "question": "Maternal grandmother's first name?",
        "createdAt": "...",
        "updatedAt": "..."
      },
      "securityAnswer": "222"
    }
   ```

5. Sent the request. The server responded with status `200 OK` and user account creation confirmation.

6. Navigated to the login page and successfully logged in using:
   
   - Email: `" "` (single space)
   - Password: `" "` (single space)

7. The challenge was immediately marked as solved.

---

**Note**:  
This demonstrates a classic validation gap: frontend enforces "non-empty" fields, but backend does not properly sanitize or reject trivial but invalid inputs. Always validate and sanitize inputs on the server side to prevent this type of logic flaw.

---

**Challenge solved!** was triggered after registering and logging in with `" "` as both email and password.
