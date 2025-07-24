# Web3 Sandbox

**Category**: Security Misconfiguration  
**Difficulty**: 1.5

**Description**:  
This challenge requires discovering an accidentally deployed Web3 smart contract sandbox intended for internal development use. The page exposes functionality for writing or deploying smart contracts and should not be publicly accessible.

---

**Solution**:  
The vulnerability lies in a misconfigured frontend route that exposes a development sandbox. This route is defined in the client-side JavaScript and not listed in the navigation or public interface. By manually browsing or reviewing the SPA router configuration, it is possible to find and access the hidden editor.

---

**Steps**:

1. Navigated to the Juice Shop application:
   
   ```
   http://localhost:3000
   ```
2. Opened browser Developer Tools → **Debugger**, and used `Ctrl+Shift+F` to search for:
   
   ```
   path:
   ```
3. Discovered a hidden route in the frontend Angular router:
   
   ```js
   path: 'web3-sanbox'
   ```
4. Manually navigated to the hidden page:
   
   ```
   http://localhost:3000/#/web3-sandbox
   ```
5. The page displayed a smart contract sandbox/editor interface.
6. Visiting this route was sufficient to trigger the challenge logic.

---

**Note**:  
This route is not detectable via directory brute-force tools, as it is implemented in client-side routing. Static fuzzing (e.g., with ffuf or gobuster) will return the default page for all non-existent paths.

---

**Challenge solved!** appeared in the scoreboard after visiting the hidden sandbox route.
