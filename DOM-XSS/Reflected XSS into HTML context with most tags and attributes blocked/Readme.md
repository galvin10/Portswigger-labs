
# Reflected XSS into HTML Context with Most Tags and Attributes Blocked

This repository documents the solution and key concepts for the PortSwigger Web Security Academy lab **"Reflected XSS into HTML context with most tags and attributes blocked."**

---

## Lab Overview

This lab demonstrates a reflected cross-site scripting (XSS) vulnerability mitigated by a Web Application Firewall (WAF) that blocks the majority of standard HTML tags and event handler attributes. The challenge is to enumerate allowed HTML elements and attributes and then craft a payload that bypasses these restrictions to execute `print()` without user interaction.

---

## Exploitation Steps

1. **Testing Allowed Tags**
    - Use different HTML tags in the search parameter to identify which are not filtered by the WAF.
    - Example:
      ```
      ?search=<body>
      ```
    - Monitor the response to see which tags are allowed into the HTML.
      ![image]()

2. **Testing Allowed Attributes**
    - Test attributes, particularly event handlers, to determine what executes.
    - Example:
      ```
      ?search=<body onresize=print()>
      ```
    - If successful, the browser will invoke the `print()` function when the event is triggered.

3. **Crafting and Delivering the Payload**
    - The payload that bypasses WAF and triggers the print dialog is:
      ```
      <body onresize="print()">
      ```
    - Use the exploit server or deliver a crafted URL containing this payload to trigger the vulnerability.

---

## Key Takeaways

- **WAF Evasion:** Automated or manual enumeration is needed to find allowed tags/attributes when standard XSS payloads are blocked.
- **Event Handler Use:** Certain event handlers like `onresize` may still be allowed and leveraged for automatic code execution.
- **No User Interaction:** The solution must trigger `print()` without needing the victim to click or take other actions.

---
