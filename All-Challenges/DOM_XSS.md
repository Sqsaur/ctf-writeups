# DOM XSS

**Category**: Cross-Site Scripting (XSS)  
**Difficulty**: 2

**Description**:  
Perform a **DOM** XSS attack with ``<iframe src="javascript:alert(`xss`)">``. 

---

**Solution**:  
This challenge was solved by identifying that the application takes the value of the `q` parameter from the `location.hash` fragment and directly inserts it into the DOM, specifically into an iframe's `src` attribute. By injecting a JavaScript URI into that iframe, we successfully executed an alert in the browser context.

---

**Steps**:

1. Navigated to the application at:
   
   ```
   http://localhost:3000
   ```

2. Triggered a search through the interface to observe how parameters are used. Confirmed that the URL changes to:
   
   ```
   http://localhost:3000/#/search?q=test
   ```

3. Opened **Firefox Developer Tools**, went to the **Debugger**, and searched globally for:
   
   ```
   location.hash
   ```
   
   Found multiple references in `vendor.js` and `jquery.min.js` indicating usage of hash-based routing and parameter handling.

4. Hypothesized that the value of `q` is parsed from the hash and injected into the DOM.

5. Crafted the following payload and appended it to the URL:
   
   ```
   #/search?q=<iframe src="javascript:alert(1)">
   ```

6. Reloaded the page and observed that the iframe was rendered with the `javascript:` source, resulting in a popup:
   
   ```
   alert(1)
   ```

7. Verified that this behavior completes the DOM XSS challenge, as the alert executes in the browser without any server interaction.

---

**"Challenge solved!"** popup confirmed that the challenge was completed.

To ensure the challenge is marked as solved in the scoreboard, the alert must contain the string **xss**.
