
# Lab: Stored DOM XSS

This README documents the PortSwigger Web Security Academy lab demonstrating a stored DOM-based cross-site scripting vulnerability in the blog comment functionality.

---

## Lab Summary

- The lab contains a stored DOM XSS vulnerability where comments are stored on the server and later rendered unsafely in the browser DOM.
- Input sanitation uses JavaScript's `replace()` function but fails to fully encode all angle brackets, enabling bypass.
- This allows injection of HTML/JavaScript code that triggers arbitrary script execution when any user views the affected page.

---

## Exploitation Steps

1. **Submit Malicious Comment**  
   Post the following payload as a comment in the blog:
![image](https://github.com/galvin10/Portswigger-labs/blob/096e1a4ed856289a6b238ba0debd67f2d70abf4c/DOM-XSS/Stored%20DOM%20XSS/screenshot/Screenshot%202025-10-04%20140931.png)

<><img src=1 onerror=alert(1)>

- The first set of angle brackets `< >` are encoded by the filter (due to `replace()`), but subsequent angle brackets are not.
- This partial encoding bypasses the filter and allows active injection.

2. **Trigger the Stored XSS**  
- When any user visits the blog post page displaying the stored comments, the injected `<img>` element attempts to load the invalid image, triggering the `onerror` event.
- This event invokes `alert(1)` as JavaScript execution, proving the stored DOM XSS.

![image](https://github.com/galvin10/Portswigger-labs/blob/096e1a4ed856289a6b238ba0debd67f2d70abf4c/DOM-XSS/Stored%20DOM%20XSS/screenshot/Screenshot%202025-10-04%20140905.png)
---

## Vulnerable Code Explanation

- The client-side script processes stored comment data using unsafe DOM sinks such as `innerHTML` or `document.write`.
- Improper input filtering and encoding enables stored attacker-controlled HTML to execute scripts.

---

## Recommendations for Defense

- Perform robust input sanitization on the server side before storing any user input.
- Use proper output encoding and avoid dangerous DOM sinks when rendering stored data on the client.
- Implement Content Security Policy (CSP) headers to reduce impact of script injection attacks.

---

