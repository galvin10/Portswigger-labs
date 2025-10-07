
# Lab: Reflected XSS into Attribute with Angle Brackets HTML-Encoded

This README documents the solution for the PortSwigger Web Security Academy lab: **Reflected XSS into attribute with angle brackets HTML-encoded**.

---

## Lab Summary

- The lab presents a reflected cross-site scripting (XSS) vulnerability where user input is inserted into an HTML attribute value.
- Angle brackets (`<` and `>`) in the user input are HTML-encoded, making tag-based injection ineffective.
- The challenge is to inject an attribute-based event handler to trigger JavaScript execution.

---

## Steps to Exploit

1. **Initial Testing**
   - Enter a random string in the search box.
   - Observe via Burp Suite or browser inspection that the value appears inside a quoted HTML attribute, e.g.:
     ```
     <input value="userinput">
     ```

2. **Crafting the Payload**
   - Since angle brackets are encoded, inject a new attribute directly.
   - Payload to break out of the current attribute and create an event handler:
     ```
     " onmouseover="alert(1)
     ```
   - The input value is now:
     ```
     <input value="" onmouseover="alert(1)">
     ```
   - The `onmouseover` event handler will trigger `alert(1)` when hovered.

3. **Triggering the Payload**
   - Submit the payload in the search box or via the intercepted request.
   - Copy the resulting URL and open it in a browser.
   - Hover over the element to trigger the XSS payload and see the alert.

---

## Mitigation Guidance

- Properly validate and sanitize all user input before reflecting it in HTML attributes.
- Use suitable encoding for the HTML context, and prevent injection of extra attributes or event handlers.
- Utilize security headers such as Content Security Policy (CSP) to limit script execution.

---

Add a screenshot showing the alert triggered by your payload here:

