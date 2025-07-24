# Repetitive Registration

**Category**: Broken Logic  
**Difficulty**: 1.5

**Description**:  
This challenge involves registering the same user more than once, violating the DRY (Don't Repeat Yourself) principle. It tests whether the application properly handles duplicate user creation attempts.

---

**Solution**:  
The challenge was marked as solved after submitting a duplicate registration request for the same user. However, it is unclear which exact method triggered the solution. Multiple approaches were tested, including manual registration, Burp Repeater, and Burp Intruder (Sniper mode). Although each duplicate request was met with a `400 Bad Request` and the error message `"email must be unique"`, the challenge still appeared as completed in the scoreboard.

---

**Steps**:

1. Navigated to the registration page:
   
   ```
   http://localhost:3000/#/register
   ```

2. Registered a user with the following data:
   
   - Email: `repeatme@juice.local`
   - Password: `Test1234!`
   - Security answer: `repeat`

3. Attempted to register the same user again immediately after:
   
   - Manually via the web UI (by visiting the registration page again)
   - Using Burp Repeater to replay the exact same POST request
   - Using Burp Intruder in Sniper mode to send two near-simultaneous requests with the same email

4. All attempts returned the following response:
   
   ```
   HTTP/1.1 400 Bad Request
   {"message":"Validation error","errors":[{"field":"email","message":"email must be unique"}]}
   ```

5. Despite the validation error, the challenge was marked as solved.

---

**Note**:  
It is unclear which specific method triggered the challenge logic. It may simply require a duplicate registration attempt, regardless of whether the second user was actually created.
