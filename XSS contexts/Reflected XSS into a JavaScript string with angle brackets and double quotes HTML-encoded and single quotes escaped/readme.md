
# Lab: Reflected XSS into JavaScript String with Angle Brackets and Double Quotes HTML-Encoded and Single Quotes Escaped

This README documents the solution and explanation for the PortSwigger Web Security Academy lab: **"Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped."**

---

## Lab Overview

- This lab demonstrates a reflected XSS vulnerability in a JavaScript string context.
- Angle brackets (`<` and `>`), and double quotes (`"`) are HTML-encoded by the application.
- Single quotes (`'`) are escaped as `\'` in the injected JavaScript code.
- The goal is to break out of the string context and execute JavaScript using an effective payload.

---

## Solution Steps

1. **Analyze the Output Context**
   - Submit a test value in the vulnerable input.
   - Inspect the rendered JavaScript to confirm that:
     - Angle brackets and double quotes are encoded (preventing direct tag/script injection).
     - Single quotes are escaped using a backslash.

2. **Craft the Payload**
   - To break out of the single-quoted string, use a payload like:
     ```
     \';-alert(1)-//
     ```
   - Explanation:
     - The first `\'` escapes the closing quote, ending the string.
     - `;-alert(1)-` is standalone JavaScript that will be executed.
     - `//` comments out the rest of the line/code to prevent syntax errors.
    
       ![image](https://github.com/galvin10/Portswigger-labs/blob/672786cff201d62ed5e0ae406d1f32e4b2ffb9c2/XSS%20contexts/Reflected%20XSS%20into%20a%20JavaScript%20string%20with%20angle%20brackets%20and%20double%20quotes%20HTML-encoded%20and%20single%20quotes%20escaped/screenshot/Screenshot%202025-10-07%20105538.png)

3. **Inject and Trigger**
   - Place the payload in the input.
   - Load the page and observe that the `alert(1)` function runs, demonstrating successful XSS.
![image](https://github.com/galvin10/Portswigger-labs/blob/672786cff201d62ed5e0ae406d1f32e4b2ffb9c2/XSS%20contexts/Reflected%20XSS%20into%20a%20JavaScript%20string%20with%20angle%20brackets%20and%20double%20quotes%20HTML-encoded%20and%20single%20quotes%20escaped/screenshot/Screenshot%202025-10-07%20105512.png)
---
