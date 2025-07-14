# Google XSS Game – Level 2: Stored XSS

---

## 🎯 Mission Description  
Web applications often keep user data in server-side and, increasingly, client-side databases and later display it to users.  
No matter where such user-controlled data comes from, it should be handled carefully.  
This level shows how easily XSS bugs can be introduced in complex apps.

---

## 🎯 Mission Objective  
Inject a script to pop up `alert(1)` in the context of the application.  
**Note:** The application saves your posts, so if you sneak in code to execute the alert, this level will be solved every time you reload it.

---

## 🧪 Steps (My Try)

### ✅ Tried:  
`flex0hi`  
→ Reflected here:  
```html
<blockquote>flex0hi</blockquote>
```
🔸 Just text, nothing happens.

---

### ✅ Tried:  
`hi">`  
→ Reflected here:  
```html
<blockquote>hi"></blockquote>
```
🔸 Breaks the attribute, but still no alert.

---

### ✅ Final payload:  
```html
<img src=x onerror="alert(1)">
```
💥 BOOM. Alert popped. Stored XSS confirmed.

---

## 🧠 Notes  
- The input is rendered inside a `<blockquote>` without escaping.
- `<script>` might be blocked, but tag-based injection like `<img>` with `onerror` works.
- Since the payload is stored, the alert runs every time you reload — that’s **Stored XSS**.

---

## ✅ Status: SOLVED 🎉
