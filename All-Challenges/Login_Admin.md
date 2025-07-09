# Zero Stars

**Category**: Broken Validation  
**Difficulty**: 2

**Description**:  
Submit feedback with a rating of zero stars.

---

**Solution**:  
This challenge was solved by manipulating a legitimate feedback submission request and forcing the rating to be `0`, even though the UI does not allow such input.

---

**Steps**:
1. I navigated to the **"Customer Feedback"** section of the application.
2. Filled out a basic comment and selected a valid rating (e.g., 3 stars) to allow the form to submit.
3. Intercepted the request using **Burp Suite**.
4. The request body contained a `"rating"` field, which I manually changed to `0` before forwarding:
   ```json
   {
     "UserId": 23,
     "captchaId": 3,
     "captcha": "23",
     "comment": "123123 (***@123)",
     "rating": 0
   }