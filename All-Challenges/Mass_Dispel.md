# Mass Dispel

**Category**: Miscellaneous  
**Difficulty**: 1

**Description**:  
This challenge requires dismissing multiple "Challenge solved!" pop-up notifications at once. Juice Shop displays a toast notification in the upper-right corner each time a challenge is completed. Normally, these are dismissed one at a time, but this challenge rewards performing a "mass dismissal."

---

**Solution**:  
After solving several challenges in quick succession, multiple "Challenge solved!" toast notifications were displayed simultaneously. Instead of closing them individually, a combined dismissal was triggered.

Although the exact mechanism is not documented in the UI, the challenge was solved by clicking the close (X) button on one notification while holding the `Shift` key. This appeared to dismiss all remaining visible notifications in one go, triggering the challenge logic.

---

**Steps**:

1. Solved multiple challenges consecutively to accumulate several `Challenge solved!` notifications.

2. Waited until at least 3 notification toasts were visible at the same time.

3. Pressed and held the `Shift` key.

4. Clicked the `X` (close) button on one of the toasts while holding `Shift`.

5. All remaining notifications were dismissed together.

6. The application displayed:
   
   ```
   Challenge solved: Mass Dispel
   ```

---

**Note**:  
Although `Shift + click` was used successfully, it's possible that `Ctrl` or  combined with quick clicks may also trigger the same effect depending on the browser or operating system.

---

**Challenge solved!** appeared after dismissing multiple success toasts simultaneously.
