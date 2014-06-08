
===========================================================
Multilingual email address validation with jQuery and RegEx
===========================================================

I have some jQuery and RegEx code that works great validating email addresses...as long as the address is based on simple Latin characters. However, when we plug in more complex multilingual email addresses, our checks fail using both native HTML5 validation and validation based on a Regular Expression.

Here's the Chinese email address we're using for testing:

伊昭傑@郵件.商務

And here's the JS validation code (I haven't bothered to strip out namespaces and internal utility methods). We have a hidden HTML5 input control of type "email", and we pass the email address to that control and let the browser work its magic. Otherwise, we use a regular expression.

What are our options? Seem like using native (e.g. browser-based) validation just won't work.
```js
um.utils.isValidEmail = function (sEmail) {
    var r = false;
    var $emailTester = {};
    var emailRegex;
    //-----

    if (Modernizr.inputtypes.email === true) {
        // Defer to native HTML5 email validation using a hidden <input type='email'> control
        $emailTester = $("#idEmailTester");
        um.utils.assertSize($emailTester);

        $emailTester.val(sEmail);
        r = $emailTester[0].checkValidity();
    } else {
        // Use a regular expression to do email validation
        // Attribution http://www.regular-expressions.info/email.html
        emailRegex = /^[a-zA-Z0-9.!#$%&'*+\/=?\^_`{|}~\-]+@[a-zA-Z0-9](?:[a-zA-Z0-9\-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9\-]{0,61}[a-zA-Z0-9])?)*$/;
        r = emailRegex.test(sEmail);
    }

    return r;
};
```
======
Answer
======
There is a very simple method to apply all you **RegEx logic**(that one can apply easily in English) for any Language using Unicode.

For matching a **range of Unicode Characters** like *all Alphabets* **[A-Za-z]** we can use
**[\u0041-\u005A]** where **\u0041** is **Hex-Code** for **A** and **\u005A** is **Hex Code** for **Z**

```js
'matchCAPS leTTer'.match(/[\u0041-\u005A]+/g)
//output ["CAPS", "TT"]
```
In the same way we can use other Unicode characters or their equivalent **Hex-Code** according to their Hexadecimal Order (eg: \u0A10 to \u0A1F) provided by unicode.org

**Try: [电-触]**

It will **match all characters between 电 and 触** if provided by unicode.org in this order