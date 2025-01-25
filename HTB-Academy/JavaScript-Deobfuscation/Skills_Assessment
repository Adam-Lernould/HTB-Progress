# GitLab Report: JavaScript Deobfuscation Skills Assessment

## **Overview**

During a penetration test, we encountered a web server containing obfuscated JavaScript and APIs. This report outlines the methodology used to analyze, deobfuscate, and replicate the functionality of the JavaScript code to uncover sensitive information and flags.

---

## **Tasks and Results**

### **Task 1: Identifying the JavaScript File**

- **Objective**: Analyze the HTML code to locate the referenced JavaScript file.
- **Method**:
  - Viewed the HTML source code using browser developer tools (`CTRL+U`).
  - Found the `<script>` tag referencing the JavaScript file `api.min.js`.
- **Result**: Identified JavaScript file: `api.min.js`.

---

### **Task 2: Executing the JavaScript Code**

- **Objective**: Test the JavaScript file to observe its functionality.
- **Method**:
  - Accessed the `api.min.js` file directly in the browser.
  - Observed that the code was obfuscated using packing techniques (`eval` and encoded variables).
  - Executed the obfuscated script in the browser console.
- **Result**: The script revealed the flag: `HTB{j4v45cr1p7_3num3r4710n_15_k3y}`.

---

### **Task 3: Deobfuscating the JavaScript Code**

- **Objective**: Deobfuscate the JavaScript code to retrieve the `flag` variable.
- **Method**:
  - Used the **UnPacker** tool to simplify the obfuscated script.
  - Manually refined the code by removing unnecessary concatenation (`+`) for better readability.
  - Analyzed the deobfuscated code to extract the `flag` variable.
- **Result**: Retrieved the flag: `HTB{n3v3r_run_0bfu5c473d_c0d3!}`.

---

### **Task 4: Analyzing and Replicating the JavaScript Functionality**

- **Objective**: Understand and replicate the main functionality of the JavaScript code.
- **Method**:
  - Analyzed the deobfuscated script:
    - The `apiKeys` function sends a `POST` request to `/keys.php` with `null` as the payload.
    - The server responds with a key.
  - Recreated this functionality using `cURL`:
    ```bash
    curl -s http://94.237.54.116:58764/keys.php -X POST -d "null"
    ```
- **Result**: Retrieved the key: `4150495f70336e5f37333537316e365f31355f66756e`.

---

### **Task 5: Decoding the Key and Retrieving the Final Flag**

- **Objective**: Decode the key and use it to retrieve the final flag.
- **Method**:
  - Determined the encoding method using **Cipher Identifier**:
    - The key was encoded in **hexadecimal**.
  - Decoded the key using the `xxd` command:
    ```bash
    echo 4150495f70336e5f37333537316e365f31355f66756e | xxd -p -r
    ```
    Decoded key: `API_p3n_73571n6_15_fun`.
  - Sent the decoded key as a `POST` parameter:
    ```bash
    curl -s http://94.237.54.116:58764/keys.php -X POST -d "key=API_p3n_73571n6_15_fun"
    ```
- **Result**: Retrieved the final flag: `HTB{r34dy_70_h4ck_my_w4y_1n_2_HTB}`.

---

## **Summary of Results**

1. **JavaScript File Identified**: `api.min.js`.
2. **Initial Flag from Obfuscated Code**: `HTB{j4v45cr1p7_3num3r4710n_15_k3y}`.
3. **Deobfuscated Code Flag**: `HTB{n3v3r_run_0bfu5c473d_c0d3!}`.
4. **Retrieved Key**: `4150495f70336e5f37333537316e365f31355f66756e`.
5. **Decoded Key**: `API_p3n_73571n6_15_fun`.
6. **Final Flag**: `HTB{r34dy_70_h4ck_my_w4y_1n_2_HTB}`.

---

## **Key Learnings**

- Obfuscated JavaScript often uses packing techniques (e.g., `eval`, dictionary replacements) to hide functionality.
- Tools like **UnPacker** and manual code analysis are essential for deobfuscation.
- Encoding methods such as Base64 and Hex are frequently used and can be decoded with tools like `xxd` and `base64`.
- Reproducing the script’s functionality with tools like `cURL` is critical for understanding server-side behavior.
