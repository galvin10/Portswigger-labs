
# DOM-Based Cross-Site Scripting (DOM XSS)

DOM-based XSS is a variant of cross-site scripting where untrusted user input is processed by client-side JavaScript and written back to the browser’s DOM, leading to arbitrary code execution. Unlike reflected or stored XSS, the payload never travels to the server—it is entirely handled on the client side.

---

## How DOM XSS Works

The fundamental mechanism is:
- The attacker places a payload within a controllable part of the page (such as the URL or hash)
- JavaScript retrieves that data from a client-side source (like `location.search`, `location.hash`, `document.URL`, or similar)
- The script then injects it into a dangerous DOM sink (for example, `document.write`, `element.innerHTML`, `eval`), causing unintended code execution

If a user visits  
`https://victimsite.com/?<img src=x onerror=alert(1)>`,  
the browser writes the malicious HTML directly into the page, executing JavaScript.

---

## Attack Flow

1. **Identify Source:** Any attacker-controlled input read by JavaScript (URL, referrer, window.name, etc.)
2. **Find Sink:** DOM functions that interpret input as HTML or JavaScript (`innerHTML`, `document.write`, `eval`, etc.)
3. **Exploit:** Craft a payload in source so that when it is reflected via a sink, JavaScript is executed in the victim’s browser.

---

## Impact

DOM XSS can:
- Hijack user sessions
- Steal sensitive information (cookies, credentials)
- Deface web pages or inject malware
- Perform actions on behalf of the user using their privileges

---

## Differences from Classic XSS

| Classic XSS                       | DOM-Based XSS                       |
| ---------------------------------- | ----------------------------------- |
| Payload is sent to server          | Payload stays on client/browser     |
| Vulnerability in server-side code  | Vulnerability in client-side JS     |
| Attack detectable in HTTP traffic  | Attack only visible in browser DOM  |
| Defense: server-side sanitization  | Defense: client-side sanitization   |

---

## Preventing DOM-Based XSS

- **Validate and Sanitize:** Always treat client-side input as untrusted. Use libraries and strict whitelisting before writing data to the DOM.
- **Avoid Dangerous Sinks:** Do not use `document.write`, `element.innerHTML`, `eval`, or similar with unsanitized input.
- **Use Secure APIs:** Manipulate text with safe APIs, such as `textContent` or setting attributes with dedicated methods.
- **Content Security Policy (CSP):** Enforce CSP to limit script sources and reduce exploit scope.
