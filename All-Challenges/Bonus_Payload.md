# DOM XSS (Bonus Payload via Search Field)

**Category**: Cross-Site Scripting (XSS)  
**Difficulty**: 2

**Description**:  
This challenge extends the original DOM-based XSS by requiring a more interactive and entertaining payload. Instead of using a traditional script-based alert, the payload involves embedding an external SoundCloud audio player, which plays music directly in the browser via an unsanitized DOM injection.

---

**Solution**:  
The application accepts unfiltered input from the search field and reflects it directly into the DOM without any sanitization. By injecting a full HTML `<iframe>` element with autoplay enabled, it is possible to embed a SoundCloud player that starts playing automatically. This action completes the bonus DOM XSS challenge.

---

**Steps**:

1. Confirmed that the original DOM XSS challenge was already completed.

2. Navigated to the main page of the Juice Shop application:
   
   ```
   http://localhost:3000
   ```

3. Focused the search field in the header.

4. Pasted the following payload directly into the search input:
   
   ```html
   <iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay"
   src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&color=%23ff5500&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>
   ```

5. Pressed Enter or clicked the search icon.

6. Observed that the SoundCloud player was injected into the page and music began playing automatically.

7. Juice Shop displayed the confirmation message:
   
   ```
   Challenge solved!
   ```

---

**Note**:  
Challenge purely solved using scoreboard. Ensure that the browser allows autoplay for media content. Interaction with the page may be necessary to trigger audio playback. The payload must be inserted exactly as specified into the search field to meet the challenge’s criteria.
