
# Lab: Reflected DOM XSS

This README covers the reflection-based DOM Cross-Site Scripting (DOM XSS) vulnerability exploited in the PortSwigger Web Security Academy "Reflected DOM XSS" lab.

---

## Lab Overview

- The lab demonstrates a DOM XSS vulnerability where a payload reflected in the URL is read by client-side JavaScript and used in an unsafe way.
- The input is reflected back to the page dynamically without appropriate sanitization.
- The goal is to craft a URL that triggers JavaScript execution by injecting malicious code through the reflected parameter.

---

## Steps to Exploit

1. **Locate the Vulnerability**
   - Identify which URL parameter is reflected into the page DOM via JavaScript.
   - Observe how the parameter is incorporated in the page source or DOM.
  
    ![image](https://github.com/galvin10/Portswigger-labs/blob/76f3e4d8a6b905c7a5ca15a3be5ccef90e3cf9ca/DOM-XSS/Reflected%20Dom%20XSS/Screenshots/Screenshot%202025-10-04%20132605.png)

2. **Craft XSS Payload**
   - Create a payload that breaks out of the existing context to execute JavaScript.
   - Example payloads include:  
     ```
     xss\"-alert(1)}//
     ```
   - Or DOM XSS-specific payloads using elements like `xss\"-alert(1)}//`.

3. **Inject Payload in URL**
   - Append the payload to the vulnerable parameter in the URL query string.
   - For example:  
     ```
     https://<LAB-ID>.web-security-academy.net/?param=xss\"-alert(1)}//>
     ```

4. **Trigger the Payload**
   - Load the crafted URL in a browser.
   - Confirm that the alert box appears, indicating successful JS execution via DOM XSS.
![image](https://github.com/galvin10/Portswigger-labs/blob/76f3e4d8a6b905c7a5ca15a3be5ccef90e3cf9ca/DOM-XSS/Reflected%20Dom%20XSS/Screenshots/Screenshot%202025-10-04%20134126.png)
---

