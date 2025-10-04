
# Lab: DOM XSS in jQuery Anchor `href` Attribute Sink Using Source `location.search`

This lab focuses on a DOM-based cross-site scripting vulnerability in which untrusted data from `location.search` is used to set the `href` attribute of a jQuery anchor (`<a>`) element without proper sanitization, enabling script injection.

---

## Lab Summary

- The application reads the `ref` parameter from the URL query string (`location.search`).
- It then uses jQuery's `.attr()` to set the `href` attribute of an anchor element.
- Lack of validation allows an attacker to inject a malicious JavaScript payload via the `href` attribute.

---

## Exploitation Steps

1. **Identify Source and Sink**  
   - The `ref` parameter is extracted from the URL, e.g. `?ref=somevalue`.
   - jQuery sets the anchor's `href` attribute using this value directly.
  
![image](https://github.com/galvin10/Portswigger-labs/blob/b47a3bd3e2442d8af4cfc3f8e0554a181fe35220/DOM-XSS/DOM%20XSS%20in%20jQuery%20anchor%20href%20attribute%20sink%20using%20location.search%20source/screenshot/Screenshot%202025-10-04%20112456.png)

2. **Craft Payload**  
   - Inject a JavaScript URI payload such as:  
     ```
     ?ref=javascript:alert(document.cookie)
     ```
   - This makes the anchor's `href` a `javascript:` URI that triggers `alert(document.cookie)` when clicked.

3. **Execute Payload**  
   - Visit the URL with the payload.
   - Click the anchor element.
   - The alert box appears, proving the XSS vulnerability.
![image](https://github.com/galvin10/Portswigger-labs/blob/b47a3bd3e2442d8af4cfc3f8e0554a181fe35220/DOM-XSS/DOM%20XSS%20in%20jQuery%20anchor%20href%20attribute%20sink%20using%20location.search%20source/screenshot/Screenshot%202025-10-04%20112829.png)
---

## Vulnerable Code Example

