# Front End: Structure, Vulnerabilities & Best Practices

This document covers the essential aspects of the **Front End** in a Web Application:
- Structure and roles
- Major vulnerabilities with examples
- Security best practices

---

## 1. What is Front End?
The **Front End** is the visible and interactive part of a Web Application, executed in the browser.  
**Main Technologies:**
- **HTML**: Page structure.
- **CSS**: Styles and formatting.
- **JavaScript**: Interactivity and dynamism.

**Objective:** Provide a smooth user experience and manage the display of data from the Back End.

---

## 2. Front End Architecture
1. **HTML**: Defines the structure with tags (`<div>`, `<form>`, etc.).
2. **CSS**: Separates presentation from structure, avoids inline styles.
3. **JavaScript**: Manages events, modifies the DOM, communicates with the server via AJAX/Fetch.

**Common Frameworks:** React, Vue, Angular, jQuery.

---

## 3. Common Front End Vulnerabilities

### 3.1 Exposure of Sensitive Data
- **Description:** Critical information in plain text within the code.
- **Example:**
    ```html
    <script>
      const apiKey = "1234-SECRET-5678";
      console.log(apiKey);
    </script>
    ```
- **Prevention:** Never store secrets on the client side. Use secure server-side calls.

---

### 3.2 Cross-Site Scripting (XSS)
- **Description:** Inserting malicious scripts via unfiltered inputs.
- **Example:**
    ```html
    <p>Search: <?php echo $_GET['q']; ?></p>
    ```
    Input: `<script>alert('XSS');</script>`
- **Prevention:** Validate and encode data, use Content Security Policy (CSP).

---

### 3.3 HTML Injection
- **Description:** Injecting unwanted HTML content.
- **Example:**
    ```html
    <div id="result"></div>
    <script>
      document.getElementById('result').innerHTML = userInput;
    </script>
    ```
- **Prevention:** Filter and escape content, avoid unsecured `innerHTML`.

---

### 3.4 Cross-Site Request Forgery (CSRF)
- **Description:** Exploiting active user sessions for unauthorized actions.
- **Example:**
    ```html
    <img src="https://victime.com/delete-account?user=admin" style="display:none"/>
    ```
- **Prevention:** Use unique CSRF tokens, require additional confirmations.

---

## 4. Best Practices (Front End)
1. **Input Validation & Encoding:** Both client and server-side.
2. **Code Separation:** Keep HTML, CSS, JS distinct.
3. **Security Headers:** CSP, X-XSS-Protection, Strict-Transport-Security.
4. **Session Management:** Secure cookies (`Secure`, `HttpOnly`, `SameSite`).
5. **Library Updates:** Keep React, Vue, Angular, etc., up to date.

---

## 5. Recommended Resources
- **[MDN Web Docs](https://developer.mozilla.org/)**
- **[OWASP Top 10](https://owasp.org/www-project-top-ten/)**
- **[OWASP Cheat Sheets](https://cheatsheetseries.owasp.org/)**
    
