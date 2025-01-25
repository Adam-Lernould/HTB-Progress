# Notes for JavaScript Deobfuscation

## Key Observations
1. **Source Code Analysis**:
   - HTML: Can be viewed using `CTRL+U` or DevTools.
   - JavaScript: Found internally or referenced externally (e.g., `<script src="secret.js"></script>`).
   - CSS: Can be internal or external (`<link rel="stylesheet" href="style.css">`).

2. **Code Obfuscation**:
   - **Minification**: Reduces readability by combining code into a single line.
   - **Packing**: Uses functions like `eval` and dictionary replacements (e.g., `function(p,a,c,k,e,d)`).
   - **Advanced Obfuscation**: Tools like Obfuscator.io replace strings with encoded versions (e.g., Base64).

3. **Deobfuscation**:
   - Use tools like Prettier, Beautifier, or UnPacker to improve readability.
   - Reverse engineer packed code by analyzing variables and execution flow.

4. **Decoding**:
   - Identify encoding types (Base64, Hex, Rot13) using patterns or tools like Cipher Identifier.
   - Decode strings with `base64 -d`, `xxd`, or `tr`.

---

## Examples
### **Code Obfuscation Example**:
Original code:
```
console.log('HTB JavaScript Deobfuscation Module');
```

Obfuscated code (using BeautifyTools):
```
eval(function(p,a,c,k,e,d){e=function(c){return c};if(!''.replace(/^/,String)){...});
```

Decoding Example:
```
Encoded string:
ZG8gdGhlIGV4ZXJjaXNlLCBkb24ndCBjb3B5IGFuZCBwYXN0ZSA7KQo=
```

Decoded output:
```
echo ZG8gdGhlIGV4ZXJjaXNlLCBkb24ndCBjb3B5IGFuZCBwYXN0ZSA7KQo= | base64 -d
```
result : 
```
7h15_15_a_s3cr37_m3554g3
```
Sending the result with a POST HTTP request : 
```
curl -s http://94.237.54.66:31871/serial.php -X POST -d "serial=7h15_15_a_s3cr37_m3554g3"
```
