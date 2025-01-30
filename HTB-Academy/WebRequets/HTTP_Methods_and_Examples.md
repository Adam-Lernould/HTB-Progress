# 5. HTTP Methods & Codes

## 5.1 Common HTTP Methods
- **GET**: Retrieve a resource (parameters are placed in the URL).  
- **POST**: Send data (forms, files) in the request *body*.  
- **HEAD**: Retrieve only headers (without the body).  
- **PUT**: Update/create a resource on the server.  
- **DELETE**: Delete a resource.  
- **OPTIONS**: Get the methods allowed by the server.

## 5.2 Status Codes
- **2xx (Success)**: e.g. `200 OK`, `201 Created`  
- **3xx (Redirection)**: e.g. `301 Moved Permanently`, `302 Found`  
- **4xx (Client Error)**: e.g. `400 Bad Request`, `403 Forbidden`, `404 Not Found`  
- **5xx (Server Error)**: e.g. `500 Internal Server Error`

---

# 6. GET

## 6.1 Principes
- Paramètres directement dans l’URL (ex. `?search=flag`).  
- **HTTP Basic Auth** :  
  - `http://user:pass@host/`  
  - ou `curl -u user:pass http://host/`

## 6.2 Exemples
```bash
# GET avec authentification Basic
curl -u admin:admin http://<SERVER_IP>:<PORT>/
```

# 7. POST
## 7.1 Principles
1. Sends data in the body (form, JSON, etc.).
2. Less visible than GET (not stored in the URL).
3. Supports uploading large files.
## 7.2 Examples
Login form:
```bash
curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/
```
Authentication cookie:
```bash
curl -i -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/
# => Set-Cookie: PHPSESSID=xyz
```
Reuse the cookie:
```bash
curl -b 'PHPSESSID=xyz' http://<SERVER_IP>:<PORT>/
```
Send JSON:
```bash
curl -X POST -d '{"search":"london"}' \
     -H 'Content-Type: application/json' \
     -b 'PHPSESSID=xyz' \
     http://<SERVER_IP>:<PORT>/search.php
```
# 8. CRUD API

## 8.1 Definition

**CRUD**: *Create, Read, Update, Delete*.

**URL Example**:  

- **GET**: Read  
- **POST**: Create  
- **PUT**: Update  
- **DELETE**: Delete  

---

## 8.2 Command Examples

### Read

```bash
curl http://<SERVER_IP>:<PORT>/api.php/city/london

```

With a more readable JSON format:
```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq
```
Create : 
```bash
curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ \
     -d '{"city_name":"HTB_City","country_name":"HTB"}' \
     -H 'Content-Type: application/json'
```
Update : 
```bash
curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london \
     -d '{"city_name":"New_HTB_City","country_name":"HTB"}' \
     -H 'Content-Type: application/json'
```
Delete : 
```bash
curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City
```
# Flags & Key Exercises
- HTTP : HTB{64$!c_cURL_u$3r}
- HTTP Headers : HTB{p493_r3qu3$t$_m0n!t0r}
- GET : HTB{curl_g3773r}
- POST : HTB{p0$t_r3p34t3r}
- CRUD API : HTB{crud_4p!_m4n!pul4t0r}























