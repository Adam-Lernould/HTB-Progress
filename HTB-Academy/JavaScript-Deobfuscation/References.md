# Reference for JavaScript Deobfuscation

## Tools and Websites

### **Code Beautification and Formatting**
- **Prettier**: A powerful code formatter for JavaScript and other languages.  
  [Website](https://prettier.io/playground/)
- **Beautifier**: Helps improve the readability of minified or obfuscated code.  
  [Website](https://beautifier.io/)
- **UnPacker**: Deobfuscates packed JavaScript code (e.g., `eval`-based obfuscation).  
  [Website](https://matthewfl.com/unPacker.html)

### **Code Obfuscation Tools**
- **BeautifyTools JavaScript Obfuscator**: A tool to create basic obfuscated JavaScript.  
  [Website](http://beautifytools.com/javascript-obfuscator.php)
- **Obfuscator.io**: Advanced obfuscation with options like Base64 string encoding.  
  [Website](https://obfuscator.io)

### **Encoding and Decoding**
- **Base64 Encoder/Decoder**:
  - Encoding: `echo "string" | base64`
  - Decoding: `echo "encoded_string" | base64 -d`
- **Hex Encoder/Decoder**:
  - Encoding: `echo "string" | xxd -p`
  - Decoding: `echo "encoded_string" | xxd -p -r`
- **Rot13 Encoder/Decoder**:
  - Encoding & Decoding: `echo "string" | tr 'A-Za-z' 'N-ZA-Mn-za-m'`

### **Encoding Identifier**
- **Cipher Identifier**: Automatically detects encoding types like Base64, Hex, Rot13, etc.  
  [Website](https://www.dcode.fr/cipher-identifier)

---

## Commands

### **HTML Source Code**
- Open page source in browser:  
  `CTRL+U`

### **cURL Commands**
- GET Request:  
  `curl http://SERVER_IP:PORT/`
- POST Request:  
  `curl -X POST http://SERVER_IP:PORT/`
- POST with Data:  
  `curl -X POST -d "param=value" http://SERVER_IP:PORT/`

---

## Notes
- **Obfuscation Techniques**:
  - Minification reduces readability but doesn't encode strings.
  - Packing uses functions like `eval` and encoded dictionaries.
  - Advanced tools like **Obfuscator.io** encode strings (e.g., Base64) and make execution more complex.

- **Deobfuscation Tips**:
  - Start with beautification to improve formatting.
  - Use tools like **UnPacker** to handle packed code.
  - Analyze execution logic manually for custom obfuscation.

- **Decoding Patterns**:
  - Base64: Look for `=` padding at the end of the string.
  - Hex: Contains only `0-9` and `a-f`.
  - Rot13: Can resemble scrambled text but often has recognizable patterns.

---

## Resources
- [JavaScript Console](https://jsconsole.com): Test and debug JavaScript code.
- [Hack The Box Labs](https://www.hackthebox.com/): Practice deobfuscation and other challenges.
