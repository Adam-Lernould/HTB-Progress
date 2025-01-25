# JavaScript Deobfuscation - HTB Academy

## Overview
This module provides an introduction to JavaScript deobfuscation, covering the basics of code analysis, obfuscation techniques, and decoding methods. The goal is to understand how obfuscated JavaScript works, analyze its functionality, and reverse its effects to uncover its original purpose.

---

## Key Questions and Answers
1. **What is the secret flag found in the HTML source?**
   - **Answer**: `HTB{4lw4y5_r34d_7h3_50urc3}`

2. **What is the flag after deobfuscating `secret.js`?**
   - **Answer**: `HTB{1_4m_7h3_53r14l_g3n3r470r!}`

3. **What is the flag after decoding the response from `serial.php`?**
   - **Answer**: `HTB{ju57_4n07h3r_r4nd0m_53r14l}`

---

## Key Concepts and Insights
### **Code Obfuscation**
- Obfuscation is used to make code difficult to read while retaining functionality.
- It is often achieved via packing, minification, or encoding techniques like Base64 or Hex.
- Commonly used in JavaScript due to its client-side nature.

### **Code Analysis**
- **Tools**:
  - Browser DevTools: Inspect and pretty-print code.
  - Online platforms: BeautifyTools, Prettier, and Beautifier for formatting.
- **Process**:
  - Examine variables, functions, and HTTP requests to understand functionality.

### **Decoding Techniques**
- **Base64**:
  - Easily identified by padding (`=`) and alphanumeric characters.
  - Encode: `echo "text" | base64`
  - Decode: `echo "encoded_text" | base64 -d`
- **Hex**:
  - Encode: `echo "text" | xxd -p`
  - Decode: `echo "hex_string" | xxd -p -r`
- **Rot13**:
  - Encode/Decode: `echo "text" | tr 'A-Za-z' 'N-ZA-Mn-za-m'`

---

## Tools and References
- **Deobfuscation Tools**:
  - [JS Console](https://jsconsole.com)
  - [Prettier](https://prettier.io)
  - [Beautifier](https://beautifier.io)
  - [UnPacker](https://matthewfl.com/unPacker.html)
- **Encoding Detection**:
  - [Cipher Identifier](https://www.dcode.fr/cipher-identifier)
