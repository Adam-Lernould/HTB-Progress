# Commands for JavaScript Deobfuscation

## General Commands
- `CTRL+U`: View the HTML source code in Firefox.
- `CTRL+SHIFT+Z`: Open browser debugger in Firefox.
- `curl http://SERVER_IP:PORT/`: Send a GET request to a URL.
- `curl -s http://SERVER_IP:PORT/ -X POST`: Send a POST request to a URL.
- `curl -s http://SERVER_IP:PORT/ -X POST -d "param1=sample"`: Send a POST request with data.

## Encoding and Decoding
### Base64
- Encode: `echo "your_text" | base64`
- Decode: `echo "your_base64_string" | base64 -d`

### Hex
- Encode: `echo "your_text" | xxd -p`
- Decode: `echo "your_hex_string" | xxd -p -r`

### Rot13
- Encode/Decode: `echo "your_text" | tr 'A-Za-z' 'N-ZA-Mn-za-m'`

## JavaScript Beautification and Deobfuscation
### Tools
- **Prettier**: https://prettier.io/playground/
- **Beautifier**: https://beautifier.io/
- **UnPacker**: https://matthewfl.com/unPacker.html

### Example Commands
- `eval`: Used for executing obfuscated code (e.g., `eval(function(p,a,c,k,e,d){...})`).
- `console.log`: Useful for debugging and analyzing return values in obfuscated code.

## HTTP Requests
- Use `curl` to simulate requests:
  - `curl http://SERVER_IP:PORT/`: Basic GET request.
  - `curl -s http://SERVER_IP:PORT/serial.php -X POST`: Send an empty POST request.
  - `curl -s http://SERVER_IP:PORT/serial.php -X POST -d "param1=value"`: Send a POST request with parameters.
  - `curl -s http://SERVER_IP:PORT/serial.php -X POST -d "serial=decoded_value"`: Send decoded value as data.

## Tools for Identifying Encoding
- **Cipher Identifier**: Online tool to identify encoding types.
- **rot13**: Online tool for Rot13 encoding and decoding.

## Practical Workflow
1. View the source code: `CTRL+U`.
2. Identify external scripts and download them.
3. Use Prettier or Beautifier to format the script.
4. Use UnPacker or manual reverse engineering for further deobfuscation.
5. Decode encoded strings using the relevant encoding tools (Base64, Hex, Rot13, etc.).
6. Simulate HTTP requests with `curl` to understand server-side functionalities.

---
