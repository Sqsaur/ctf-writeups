# Missing Encoding

**Category**: Improper Input Validation  
**Difficulty**: 1.5

**Description**:  
Retrieve the photo of Bjoern's cat in "melee combat-mode".

---

**Solution**:  
I managed to solve this by correcting a broken image link manually in the browser.

---

**Steps**:

1. I went to the **Photo Wall** page and noticed that one image wasn't loading — only `alt` text appeared.
2. I right-clicked the image placeholder and used **Inspect Element**.
3. The image source path contained an invalid character `#` in the filename — which is not allowed in URLs without proper encoding.
4. I copied the `src` value and replaced `#` with its encoded form `%23`, like:
   
   ```
   /assets/public/images/uploads/ᓚᘏᗢ-#zatschi-#whoneedsfourlegs-1572600969477.jpg
   ↓
   /assets/public/images/uploads/ᓚᘏᗢ-%23zatschi-%23whoneedsfourlegs-1572600969477.jpg
   ```
5. After pasting the fixed URL directly into the address bar, the image loaded correctly.

---

**Result**:  
Once the corrected image was accessed, a **"Challenge solved!"** popup confirmed completion.
