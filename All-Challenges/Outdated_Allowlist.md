# Outdated Allowlist

**Category**: Security Misconfiguration  
**Difficulty**: 1.5

**Description**:  
This challenge requires discovering a redirect to an outdated cryptocurrency donation address that should no longer be active. While references to these wallets were removed from the UI, the backend or frontend logic still allows redirecting to them, revealing a misconfigured allowlist.

---

**Solution**:  
The Juice Shop application previously accepted cryptocurrency donations via Bitcoin, Dash, and Ether. Although these donation options were officially removed, remnants of them remained embedded in the frontend source code. By locating and using one of these deprecated wallet redirect URLs, we were able to exploit the outdated allowlist and complete the challenge.

---

**Steps**:

1. Navigated to the application:
   
   ```
   http://localhost:3000
   ```

2. Opened **DevTools → Debugger** and searched globally using:
   
   ```
   redirect
   ```

3. Found hardcoded data structures referencing deprecated cryptocurrency addresses:
   
   ```js
   data: {
     data: 'bitcoin:1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm',
     url: './redirect?to=https://blockchain.info/address/1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm',
     address: '1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm',
     title: 'TITLE_BITCOIN_ADDRESS'
   }
   ```

4. Manually constructed the redirect URL and visited:
   
   ```
   http://localhost:3000/#/redirect?to=https://blockchain.info/address/1AbKfgvw9psQ41NbLi8kufDQTezwG8DRZm
   ```

5. The application accepted the redirect and showed me message : Cannot GET /address/Xr556RzuwX6hg5EGpkybbv5RanJoZN17kW

6. Upon redirection, the challenge was marked as solved.

---

**Challenge solved!** appeared in the scoreboard after visiting the deprecated Bitcoin redirect.
