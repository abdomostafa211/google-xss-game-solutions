🔰 Level 1: Reflected XSS - Basic Injection
📝 Mission Description:

    This level demonstrates a common cause of Cross-Site Scripting (XSS), where user input is directly included in the page without proper escaping.

Your goal is to inject JavaScript that causes a alert() popup.
🎯 Mission Objective:

Inject a script that pops up an alert() box in the frame.
Once you succeed, you can proceed to the next level.
🔍 Vulnerability Type:

    Reflected XSS

    Unsanitized input directly rendered into the HTML response.

🔗 Test Cases Tried:
Attempt	Result
?query=x	Reflected as: <b>x</b>
?query=X">x	Reflected as: <b>X">x</b> — shows input inside a tag
?query=<script>alert(1)</script>	✅ JavaScript executed, level completed
✅ Final Payload Used:

<script>alert(1)</script>

URL:

https://xss-game.appspot.com/level1/frame?query=<script>alert(1)</script>

🧠 Explanation:

    The input is inserted inside the page using innerHTML, without escaping.

    The script tag is interpreted by the browser and executed.

    No filters or encoding are applied in this level, making it the easiest form of XSS.
