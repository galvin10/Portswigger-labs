
# Lab: DOM XSS in `document.write` Sink Using Source `location.search` Inside a Select Element

This README describes the exploitation steps and mitigation guidance for the PortSwigger Web Security Academy lab where a DOM-based XSS vulnerability exists in the use of `document.write` within a select element, sourced from `location.search` (specifically the `storeId` query parameter).

---

## Lab Scenario

- The web page features a stock checker where product page URLs include a `storeId` parameter.
- JavaScript receives this parameter from `location.search` and uses `document.write` to add a new `<option>` to a `<select>` element.
- The browser renders user-provided content inside the select element with no sanitization.

---

## Exploitation Steps

1. **Identify Reflection**
   - Find a product page URL, e.g.:
     ```
     /product?productId=1
     ```
![image](https://github.com/galvin10/Portswigger-labs/blob/f0566372d1d38cfbdcbdff928f342cf1fec9a87e/DOM-XSS/DOM%20XSS%20in%20%60document.write%60%20Sink%20Using%20Source%20%60location.search%60%20Inside%20a%20Select%20Element/screenshot/Screenshot%202025-10-04%20110033.png)
   - Add a `storeId` parameter:
     ```
     /product?productId=1&storeId=xyz
     ```
   - Confirm that `xyz` is reflected as an option in the dropdown.

2. **Craft an XSS Payload**
   - Inject a payload to break out of the `<option>` context and the `<select>` element:
     ```
     /product?productId=1&storeId="></select><img src=1 onerror=alert(1)>
     ```
   - This payload closes the `<option>` and `<select>`, then adds an `<img>` element with an `onerror` attribute to execute JavaScript.

3. **Exploit and Confirm**
   - Load the URL with the payload in a browser.
   - The alert box is triggered, confirming DOM XSS.
  
![image](https://github.com/galvin10/Portswigger-labs/blob/f0566372d1d38cfbdcbdff928f342cf1fec9a87e/DOM-XSS/DOM%20XSS%20in%20%60document.write%60%20Sink%20Using%20Source%20%60location.search%60%20Inside%20a%20Select%20Element/screenshot/Screenshot%202025-10-04%20110014.png)

---

