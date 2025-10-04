
# DOM XSS in `document.write` Using `location.search`

This README documents the solution for the PortSwigger Web Security Academy lab: **DOM XSS in document.write sink using source location.search**.

---

## Lab Summary

The lab demonstrates DOM-based XSS where user input from the URL query (`location.search`) is dynamically written to the page with `document.write`, leading to JavaScript execution.

---

## Solution Steps

1. **Input Reflection**
   - Enter a search term using the URL's `search` parameter.
   - Observe that the input is reflected in an HTML element created via `document.write`.
  
     ![image alt](https://github.com/galvin10/Portswigger-labs/blob/e6cb488b85be656ac1536cbb4c766c4e84938565/DOM-XSS/DOM%20XSS%20in%20document.write%20sink%20using%20source%20location.search/Screenshot/Screenshot%202025-10-04%20093952.png)

2. **Crafting the XSS Payload**
   - The sink is `document.write`, and the source is directly attacker-controlled: `location.search`.
   - Payload to break out of the attribute and inject JavaScript:  
     ```
     ?search="><svg onload=alert(1)>
     ```
   - This closes the preceding tag and injects a new element which triggers the `alert()`.

3. **Execution**
   - The payload executes, showing the alert dialog and successfully exploiting the lab.

![image alt](https://github.com/galvin10/Portswigger-labs/blob/e6cb488b85be656ac1536cbb4c766c4e84938565/DOM-XSS/DOM%20XSS%20in%20document.write%20sink%20using%20source%20location.search/Screenshot/Screenshot%202025-10-04%20094148.png)

## Vulnerable Code Description

- Source: `location.search` (URL query string)
- Sink: `document.write` (directly writes user input to HTML)
- Impact: Unsanitized, attacker-supplied input is parsed and executed as markup/JavaScript.

![image alt](https://github.com/galvin10/Portswigger-labs/blob/e6cb488b85be656ac1536cbb4c766c4e84938565/DOM-XSS/DOM%20XSS%20in%20document.write%20sink%20using%20source%20location.search/Screenshot/Screenshot%202025-10-04%20094026.png)

## References

- PortSwigger Web Security Lab documentation
- XSS payload examples and cheat sheet

---
