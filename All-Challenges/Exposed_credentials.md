# Exposed Credentials

**Category**: Sensitive Data Exposure  
**Difficulty**: 2

**Description**:  
A developer left valid test credentials hardcoded on the client-side code. While not exposed via the UI, these credentials are still active and can be used to access the system. This challenge illustrates a common mistake where developers forget to remove temporary credentials before deployment.

---

**Solution**:  
This vulnerability was discovered by inspecting the client-side JavaScript code. The credentials were left directly in the source as string variables, likely for internal testing purposes during development.

---

**Steps**:

1. Opened the application in browser and opened **DevTools → Sources → Debugger**.
2. Used `Ctrl+Shift+F` to globally search for:
   
   ```
   password
   ```
3. Found the following hardcoded credentials in a file:
   
   ```js
   testingUsername = 'testing@juice-sh.op';
   testingPassword = 'IamUsedForTesting';
   ```
4. Navigated to the login page:
   
   ```
   http://localhost:3000/#/login
   ```
5. Logged in using:
   - **Email**: `testing@juice-sh.op`
   - **Password**: `IamUsedForTesting`
6. Upon successful login, the challenge `Exposed Credentials` was instantly marked as solved.

---

**Note**:  
This type of vulnerability is a classic example of sensitive data exposure due to insecure client-side practices. Even unused or hidden credentials can pose a significant risk if left in production code.

---

**Challenge solved!** was triggered immediately after logging in with the exposed credentials.
