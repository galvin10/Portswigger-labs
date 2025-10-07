# Lab: Stored XSS into `onclick` Event with Angle Brackets and Double Quotes HTML-Encoded and Single Quotes and Backslash Escaped

This README documents the solution for the PortSwigger Web Security Academy lab: **"Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped."**

---

## Lab Overview

- The vulnerability involves stored Cross-Site Scripting (XSS) in the `onclick` event handler of an element.
- The application HTML-encodes angle brackets (`<`, `>`) and double quotes (`"`), and escapes single quotes (`'`) and backslashes (`\`).
- Despite these protections, an attacker can craft a payload that breaks out of the encoded context and executes JavaScript.

---

## Payload Details

- The payload used to exploit this lab is:
  
http://das?&apos;-alert(1)-&apos;


- This payload effectively:
- Closes the existing string or attribute context using the escaped single quote (`&apos;`).
- Injects JavaScript code to call `alert(1)`.
- Uses dash (`-`) characters to prevent syntax errors.
- Ends with another escaped single quote to balance the string.
  ![image](https://github.com/galvin10/Portswigger-labs/blob/0ca0a24e00301b876fdc6ea8ad264c0722692482/XSS%20contexts/Stored%20XSS%20into%20onclick%20event%20with%20angle%20brackets%20and%20double%20quotes%20HTML-encoded%20and%20single%20quotes%20and%20backslash%20escaped/Screenshots/Screenshot%202025-10-07%20114159.png)

---

## Exploitation Steps

1. **Submit a Comment or Input using the Payload**
 - Provide the payload as part of the input that is stored and later rendered inside an `onclick` attribute.

2. **Stored Injection**
 - The comment or input is stored on the server without proper sanitization.

3. **Trigger the XSS**
 - When any user views the stored input, the malicious `onclick` event executes the `alert(1)` function.
 - The attack executes without requiring direct script tags due to clever escaping and encoding bypass.
![image](https://github.com/galvin10/Portswigger-labs/blob/0ca0a24e00301b876fdc6ea8ad264c0722692482/XSS%20contexts/Stored%20XSS%20into%20onclick%20event%20with%20angle%20brackets%20and%20double%20quotes%20HTML-encoded%20and%20single%20quotes%20and%20backslash%20escaped/Screenshots/Screenshot%202025-10-07%20114310.png)
---

## Explanation of Vulnerable Code

- User input is injected inside an `onclick` event handler attribute.
- Angle brackets and double quotes are encoded to HTML entities, while single quotes and backslashes are escaped.
- This partially prevents classic injections but can be bypassed using the crafted payload.

---

## Mitigation Recommendations

- Sanitize and encode user input carefully, considering the context (HTML attributes, JavaScript).
- Avoid injecting untrusted input directly into event handler attributes.
- Utilize Content Security Policy (CSP) to limit script execution scope.

---
