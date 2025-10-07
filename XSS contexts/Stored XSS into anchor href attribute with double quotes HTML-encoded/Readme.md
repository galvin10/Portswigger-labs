# Lab: Stored XSS into Anchor `href` Attribute with Double Quotes HTML-Encoded

This README documents the solution and concepts for the PortSwigger Web Security Academy lab: **"Stored XSS into anchor href attribute with double quotes HTML-encoded."**

---

## Lab Overview

- The lab demonstrates a stored XSS vulnerability in the comment functionality.
- User input supplied in the "Website" field is stored and later reflected inside an anchor (`<a>`) tag's `href` attribute.
- Double quotes (`"`) are HTML-encoded, but the application does not validate or sanitize dangerous protocols like `javascript:` in URLs.

---

## Solution Steps

1. **Confirm Reflection Context**
   - Submit a comment with a random string in the "Website" field.
   - Check the resulting blog post: the input is reflected in the `href` attribute of the comment author's name.

2. **Craft a JavaScript URL Payload**
   - Input to use:
     ```
     javascript:alert(1)
     ```
   - This utilizes the `javascript:` protocol in the `href` to trigger code execution when the link is clicked.

3. **Trigger XSS**
   - After submitting the comment, view the post as any user.
   - Click the author name above your comment.
   - An alert should appear, proving that the stored XSS in the anchor `href` was successful.

---

## Vulnerable Code Explanation

- User-provided "Website" input is stored and used directly in the `href` attribute.
- Double quotes are HTML-encoded, but the `javascript:` protocol is not filtered.
- Clicking the link causes the browser to execute the JavaScript payload.

---

## Mitigation Recommendations

- Disallow `javascript:` and other dangerous protocols in URLs supplied by users.
- Validate and sanitize all user input, especially for URL-based attributes.
- Consider using allow-lists for safe protocols (e.g., `http`, `https`).

---



