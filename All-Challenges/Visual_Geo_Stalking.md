# Visual Geo Stalking

**Category**: Broken Authentication  
**Difficulty**: 1

**Description**:  
This challenge demonstrates how seemingly harmless uploaded images can leak sensitive information. By analyzing a photo uploaded by a user (Emma), it's possible to determine the answer to her security question and reset her password via the "Forgot Password" functionality.

---

**Solution**:  
The solution involved visually inspecting a photo uploaded by Emma to the public Photo Wall. The challenge relied on performing open-source intelligence (OSINT) against visual elements in the image. At first, it appeared that the security question might relate to a location (due to a recognizable landmark), but further inspection revealed the true answer embedded more subtly in the image.

---

**Steps**:

1. Navigated to the Photo Wall:
   
   ```
   http://localhost:3000/#/photo-wall
   ```

2. Identified a photo uploaded by **Emma**.

3. Analyzed the image carefully:
   
   - Used Google Images and reverse search to confirm the landmark location. The building appeared to be in **Kenaupark, Haarlem, Netherlands**.
   - At first, assumed the security question would relate to this location (e.g., city of birth or park name).
     
     

4. Proceeded to the "Forgot Password" page

5. ```
      Email: emma@juice-sh.op
   ```

6. The security question displayed was:
   
   ```
   Company you first work for as an adult?
   ```

7. Upon zooming in on the image, discovered a subtle **"ITsec"** logo or text inside a window of the photographed building.

8. Used **`ITsec`** as the answer to the security question.

9. Successfully reset Emma’s password and completed the challenge.

---

**Note**:  
This challenge emphasizes the risks of unintentionally leaking sensitive personal data through uploaded media. Even partial company names, logos, or building identifiers can lead attackers to deduce private information.

---

**Challenge solved!** was triggered after answering the security question correctly and resetting Emma's password using clues from the uploaded image.
