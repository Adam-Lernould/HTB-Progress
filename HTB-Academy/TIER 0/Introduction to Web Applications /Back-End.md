# Back End: Servers, Databases & Security

This document covers the essential aspects of the **Back End** in a Web Application:
- Main Components
- Types of Databases
- Public Vulnerabilities
- Security Best Practices

---

## 1. Back End Servers

### Definition
The **Back End Server** hosts the applications necessary for the Web Application to function, integrating business logic and data access.

### Software Components
- **Web Server**: Manages HTTP traffic (Apache, NGINX, IIS).
- **Database**: Stores data (MySQL, PostgreSQL, MongoDB).
- **Development Framework**: Facilitates development (Laravel, Express, Django, Rails).

### Common Stacks
- **LAMP**: Linux, Apache, MySQL, PHP.
- **WAMP**: Windows, Apache, MySQL, PHP.
- **WINS**: Windows, IIS, .NET, SQL Server.
- **MAMP**: macOS, Apache, MySQL, PHP.
- **XAMPP**: Cross-Platform, Apache, MySQL, PHP/PERL.

---

## 2. Web Servers

### Definition
A **web server** handles HTTP requests from client browsers and serves the requested resources.

### Common HTTP Response Codes
| Code | Description |
|------|-------------|
| **200 OK** | Successful request. |
| **301 Moved Permanently** | Resource permanently moved. |
| **404 Not Found** | Resource not found. |
| **500 Internal Server Error** | Server error. |

### Examples of Web Servers
1. **Apache**
   - Popular and extensible via modules.
   - Used by Apple, Adobe, Baidu.
2. **NGINX**
   - Optimized for concurrent requests.
   - Used by Google, Facebook, Netflix.
3. **IIS**
   - Integrated with Windows Server.
   - Used by Microsoft, Office365, Dell.

**Example cURL Commands:**
```bash
# Check HTTP headers
curl -I https://academy.hackthebox.com

# Get page content
curl https://academy.hackthebox.com
```

## 3. Databases

### Types of Databases
1. **Relational (SQL)**
   - **Structure:** Tables, rows, columns.
   - **Examples:** MySQL, MSSQL, Oracle, PostgreSQL.
   - **Advantages:** Clear relationships, complex queries.

2. **Non-relational (NoSQL)**
   - **Structure:** Key-Value, Document-Based, Wide-Column, Graph.
   - **Examples:** MongoDB, ElasticSearch, Cassandra.
   - **Advantages:** Scalability, flexibility.

### Usage in Web Applications

#### Example
```php
// Connect to the database
$conn = new mysqli("localhost", "user", "pass");

// Create a new database
$sql = "CREATE DATABASE database1";
$conn->query($sql);

// Connect and execute a query
$conn = new mysqli("localhost", "user", "pass", "database1");
$query = "SELECT * FROM table_1";
$result = $conn->query($query);

// Display results
while($row = $result->fetch_assoc()) {
    echo $row["name"] . "<br>";
}
```

## 4. Common Back End Vulnerabilities

### 4.1 Broken Authentication/Access Control
- **Broken Authentication:** Bypassing authentication functions.
  - **Example:** Auth Bypass with `' or 0=0 #`.
- **Broken Access Control:** Unauthorized access to resources.
  - **Example:** Normal user accesses the admin panel.

### 4.2 Malicious File Upload
- **Description:** Uploading malicious scripts via unsecured file upload features.
  - **Example:** WordPress plugin "Responsive Thumbnail Slider 1.0" allows `shell.php.jpg`.

### 4.3 Command Injection
- **Description:** Injecting OS commands via unfiltered inputs.
  - **Example:** WordPress plugin "Plainview Activity Monitor" allows `| COMMAND....`.

### 4.4 SQL Injection (SQLi)
- **Description:** Injecting malicious SQL queries.
  - **Example:** SQLi authentication allowing access without credentials.



