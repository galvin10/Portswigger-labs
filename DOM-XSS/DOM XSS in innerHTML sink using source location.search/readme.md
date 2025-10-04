# Lab: DOM XSS in `innerHTML` Sink Using Source `location.search`

This lab demonstrates a DOM-based cross-site scripting vulnerability where the value from `location.search` is assigned directly to the `innerHTML` of a `div` element, enabling execution of attacker-supplied JavaScript.

---

## Lab Summary

- The search functionality takes input from the URL query string (`location.search`).
- The input is directly assigned to a `div` using `.innerHTML` without sanitization.
- This allows injection of malicious HTML/JavaScript, resulting in DOM XSS.

---

## Solution Steps

1. **Locate Input Reflection**  
   - Access the page and enter a search term in the search box.
   - Observe that the search term is inserted into the page inside a `div` with `.innerHTML`.
  ![image](https://github.com/galvin10/Portswigger-labs/blob/c2f68c00047b8d07e53865e568e8669710b11a39/DOM-XSS/DOM%20XSS%20in%20innerHTML%20sink%20using%20source%20location.search/Screenshot/Screenshot%202025-10-04%20111215.png)

2. **Inject XSS Payload**  
   - Use the following payload as the search input:  
     ```
     <img src=1 onerror=alert(1)>
     ```
   - When the page loads, the browser tries to load an invalid image which triggers the `onerror` event.
   - The `onerror` event calls `alert(1)`, demonstrating successful XSS.

3. **Trigger the Attack**  
   - Enter the payload as the search term and click “Search”.
   - The alert box should appear, confirming code execution.
  
  ![image](https://github.com/galvin10/Portswigger-labs/blob/c2f68c00047b8d07e53865e568e8669710b11a39/DOM-XSS/DOM%20XSS%20in%20innerHTML%20sink%20using%20source%20location.search/Screenshot/Screenshot%202025-10-04%20111249.png)

---


