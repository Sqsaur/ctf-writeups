# Score Board

**Category**: Miscellaneous  
**Difficulty**: 100  

**Description**:  
Access the score board. (Difficulty Level: 2)

---

**Solution**:  
This challenge can be completed by directly accessing the score board page, even though it isn’t linked in the UI. The route was discovered through analysis of the application's JavaScript files.

---

**Steps**:
1. Open Juice Shop at `http://localhost:3000`  
2. Open Developer Tools (F12), go to the **Network** tab  
3. Refresh the page  
4. Locate and open `main.js`  
5. Search for routes using `Ctrl + F` → look for `path:"xxxx"`, on main page of Juice shop we can also find it
6. Navigate manually to the following URL:http://localhost:3000/#/score-board
7. Once the page loads, the challenge will be marked as completed automatically.

---

**Result**:  
You should see a popup saying **"Challenge solved!"**, and the score board with challenge list will be displayed.

