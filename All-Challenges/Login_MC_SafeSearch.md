# Login MC SafeSearch

**Category**: Broken Access Control
**Difficulty**: 2

**Description**:  
The goal of this challenge is to log in as the user "MC SafeSearch" using their **original credentials**, without using SQL injection, brute-force, or reset password functionality. The challenge requires discovering the correct combination of email and password that were originally assigned to the user.

---

**Solution**:  
Instead of attempting technical bypasses, the solution relied on creative OSINT techniques and logical reasoning about the user "MC SafeSearch." The hint lies in pop culture.

"MC SafeSearch" is a fictional character in a video produced by the Juice Shop project itself. In the video, he mentions his dog's name as **Mr. Noodles**. Based on that, I deduced the password might be related to this name.

After several trial combinations, the correct credentials were:

- **Email**: `mc.safesearch@juice-sh.op`  
- **Password**: `Mr. N00dles`

This variation included a capitalized first letter, a period, and two zeros (`00`) in place of the double "o" – a common obfuscation style used in passwords.

---

**Steps**:

1. Searched online for references to **MC SafeSearch**.

2. Found the video

3. In the video, the character mentions his dog's name: **Mr. Noodles**.

4. Guessed multiple password variations manually, trying combinations like:
   
   - `Mr.Noodles`
   - `Mr.N00dles`
   - `Mr. N00dles`  - Correct

5. Logged in using:
   
   ```
   Email:    mc.safesearch@juice-sh.op
   Password: Mr. N00dles
   ```

6. Challenge was immediately marked as solved.

---

**Note**:  
This challenge demonstrates how user details, especially those based on personal or semi-public information (e.g. names of pets, children, favorite places), can lead to credential compromise — especially when weak or guessable passwords are used.

---

**Challenge solved!** was triggered upon successful login using the original credentials of MC SafeSearch.
