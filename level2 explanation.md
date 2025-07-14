Level 2: Stored XSS - Sneaky Injection
📝 Mission Description:

    Web applications often store user input in databases (server-side or client-side) and then render it back into the page.
    This level demonstrates how easily XSS bugs can be introduced in such apps when input is not properly sanitized.

🎯 Mission Objective:

Inject JavaScript to trigger an alert() popup within the application’s context.
Note: Since the input is stored, the script will execute on every reload — this is a case of Stored XSS.
🔍 Vulnerability Type:

    Stored XSS

    HTML injection via user-submitted content

    Rendering without proper escaping

🔗 Test Cases Tried:
Attempt	Reflected As	Result
flex0hi	<blockquote>flex0hi</blockquote>	Not executed
hi">	<blockquote>hi"></blockquote>	Breaks attribute
<img src=x onerror="alert(1)">	✅ Injected & Executed	✅ Success
✅ Final Payload Used:

<img src=x onerror="alert(1)">

The onerror attribute triggers the alert when the image fails to load.
🔁 Persistence Check:

    After injecting the payload, refreshing the page still shows the alert.

    This proves it’s stored in the application’s state and replayed on load.

🧠 Explanation:

    The input is inserted inside a <blockquote> tag, and there's no sanitization.

    Closing the tag or breaking out with malformed attributes makes script injection possible.

    Using the img tag with a broken source and onerror is a classic, stealthy XSS method.

