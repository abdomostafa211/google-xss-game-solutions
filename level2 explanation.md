Google XSS Game – Level 2: Stored XSS

Level Type: Stored XSS – Inside blockquote HTML tag
Difficulty: Beginner
🔗 Level URL

https://xss-game.appspot.com/level2/frame
🧪 Steps (My Approach)

    ✅ Typed flex0hi → reflected as:

<blockquote>flex0hi</blockquote>

❌ Not executable – just plain text

✅ Tried breaking the tag using:

hi">

→ Output:

<blockquote>hi"></blockquote>

❌ Still nothing triggered – but it showed we can break out of attributes

✅ Injected XSS via <img> tag:

    <img src=x onerror="alert(1)">

    🎉 Success! Alert triggered and XSS was stored in the page

✅ Final Payload

<img src=x onerror="alert(1)">

This payload is stored and executed every time the page is loaded → proves it’s a Stored XSS.
🛠 Tools

    Manual testing in browser

    Checked source using DevTools

    Used classic tag-based injection (img + onerror)

🎯 Goal

Trigger a JavaScript alert using stored XSS inside a blockquote element.
🧠 Notes

    Application reflects input inside:

    <blockquote>[USER_INPUT]</blockquote>

    No filtering on tags like <img>

    Using onerror is a safe bypass when <script> is blocked

    Closing tags not required in this level

✅ Status: Solved
