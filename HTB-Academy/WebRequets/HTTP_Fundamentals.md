# 1. HTTP Fundamentals

## 1.1 Definition
- **HTTP (HyperText Transfer Protocol)** is an application-layer protocol for exchanging resources (web pages, data, etc.) between a client (web browser, cURL, etc.) and a server (webserver).  
- The default port is **80**, though other ports may be used.

## 1.2 URL Structure

- **Scheme**: `http://` or `https://`  
- **Host**: Domain name or IP address (e.g., `www.hackthebox.com`)  
- **Port**: Optional (default: 80 for HTTP, 443 for HTTPS)  
- **Path**: Resource path (e.g., `/index.html`)  
- **Query String**: Parameters in the format `?param=value`  
- **Fragment**: Anchor (`#section`) to point to a specific page section

## 1.3 Basic cURL Commands
- `curl <url>`: Fetches the page in raw text (unrendered HTML).  
- `curl -O <url>`: Downloads the remote file using its original name.  
- `curl -o <filename> <url>`: Downloads the file with a custom name.  
- `curl -s <url>`: Silent mode (no progress/output).  
- `curl -v <url>`: Verbose mode (displays detailed request/response headers).

---

# 2. HTTPS (Hypertext Transfer Protocol Secure)

## 2.1 Principles
- **HTTPS** encrypts communication between clients and servers to counter *Man-In-The-Middle (MITM)* attacks.  
- Default port: **443**.  
- Browsers often display a padlock icon or enforce HTTP → HTTPS redirects for security purposes.

## 2.2 cURL and Certificates
- By default, cURL verifies SSL certificate validity.  
- To bypass certificate verification (for self-signed certs, local labs, etc.):
  ```bash
  curl -k https://<url>
  ```
# 3. HTTP Requests & Responses

## 3.1 HTTP Request Structure
1. **Request Line**: Method URI Version  
   Example: `GET /index.html HTTP/1.1`
2. **Headers**: Host, User-Agent, Cookie, etc.
3. **Body**: Primarily used for POST requests (or other data-submission methods).

## 3.2 HTTP Response Structure
1. **Status Line**: HTTP/1.1 Status_Code (e.g., `HTTP/1.1 200 OK`)
2. **Headers**: Server, Set-Cookie, Content-Type, etc.
3. **Body**: Returned content (HTML, JSON, etc.).

## 3.3 Viewing Requests/Responses
1. **cURL**: Use `-v` (verbose) or `-i` (include headers) for detailed output.  
2. **Browser DevTools**: Network tab (F12/Ctrl+Shift+I) to inspect individual requests.

# 4. HTTP Headers

## 4.1 Main Categories
- **General Headers**: Common to both requests and responses (e.g., `Date`, `Connection`).  
- **Entity Headers**: Describe content characteristics (e.g., `Content-Type`, `Content-Length`).  
- **Request Headers**: Sent by clients (e.g., `Host`, `User-Agent`, `Cookie`).  
- **Response Headers**: Sent by servers (e.g., `Server`, `Set-Cookie`).  
- **Security Headers**: Enhance security (e.g., `Content-Security-Policy`, `Strict-Transport-Security`).  

## 4.2 Useful Examples with cURL  
Display only response headers:  
```bash
curl -I http://<url>
```
Display headers + content :
```bash
curl -i http://<url>
```
Add a custom header :
```bash
curl -H "Nom-Header: valeur" http://<url>
```



