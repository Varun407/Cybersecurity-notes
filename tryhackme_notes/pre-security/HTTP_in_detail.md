# HTTP in Detail

## HTTP & HTTPS

### HTTP (HyperText Transfer Protocol)

HTTP is the protocol used for communication between web browsers and web servers.

* Transfers web content such as HTML, images, videos, and files.
* Works on port **80** by default.
* Data is transmitted in plain text.

### HTTPS (HyperText Transfer Protocol Secure)

HTTPS is the secure version of HTTP.

* Encrypts data using SSL/TLS.
* Protects against eavesdropping and tampering.
* Verifies the identity of the website.
* Uses port **443** by default.

### Quick Comparison

| HTTP          | HTTPS       |
| ------------- | ----------- |
| Not encrypted | Encrypted   |
| Port 80       | Port 443    |
| Less secure   | More secure |

---

# URL (Uniform Resource Locator)

A URL specifies how and where to access a resource on the internet.

### URL Structure

```text
https://user:password@example.com:443/blog?id=1#section
```

| Part         | Purpose                     |
| ------------ | --------------------------- |
| Scheme       | Protocol (HTTP, HTTPS, FTP) |
| User         | Username for authentication |
| Host         | Domain name or IP address   |
| Port         | Service port number         |
| Path         | Resource location           |
| Query String | Additional parameters       |
| Fragment     | Specific section on a page  |

---

# HTTP Requests & Responses

## HTTP Request

A browser sends a request to a web server asking for a resource.

### Example

```http
GET / HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
```

### Components

* Method (GET, POST, etc.)
* Headers
* Optional body

---

## HTTP Response

The server returns the requested resource and status information.

### Example

```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 98
```

### Important Response Headers

| Header         | Purpose               |
| -------------- | --------------------- |
| Content-Type   | Type of returned data |
| Content-Length | Size of response      |
| Server         | Web server software   |
| Date           | Response timestamp    |

---

# HTTP Methods

HTTP methods define the action a client wants to perform.

| Method | Purpose              |
| ------ | -------------------- |
| GET    | Retrieve data        |
| POST   | Submit/Create data   |
| PUT    | Update existing data |
| DELETE | Remove data          |

### Common Usage

* View webpage → GET
* Submit login form → POST
* Update profile → PUT
* Delete account → DELETE

---

# HTTP Status Codes

Status codes indicate the result of a request.

## Status Code Categories

| Range   | Meaning       |
| ------- | ------------- |
| 100–199 | Informational |
| 200–299 | Success       |
| 300–399 | Redirection   |
| 400–499 | Client Errors |
| 500–599 | Server Errors |

---

## Common Status Codes

| Code | Meaning                    |
| ---- | -------------------------- |
| 200  | OK                         |
| 201  | Created                    |
| 301  | Moved Permanently          |
| 302  | Found (Temporary Redirect) |
| 400  | Bad Request                |
| 401  | Unauthorized               |
| 403  | Forbidden                  |
| 404  | Not Found                  |
| 405  | Method Not Allowed         |
| 500  | Internal Server Error      |
| 503  | Service Unavailable        |

### Examples

* New user created → **201**
* Page doesn't exist → **404**
* Login required → **401**
* Server overloaded → **503**

---

# HTTP Headers

Headers provide additional information during communication.

## Common Request Headers

| Header          | Purpose                               |
| --------------- | ------------------------------------- |
| Host            | Specifies the website being requested |
| User-Agent      | Browser and version information       |
| Content-Length  | Size of sent data                     |
| Accept-Encoding | Supported compression methods         |
| Cookie          | Stored user information               |

---

## Common Response Headers

| Header           | Purpose                   |
| ---------------- | ------------------------- |
| Set-Cookie       | Stores cookies in browser |
| Cache-Control    | Controls caching          |
| Content-Type     | Type of returned content  |
| Content-Encoding | Compression method used   |

### Important Headers

* **Host** → Identifies the website being requested.
* **User-Agent** → Identifies the browser.
* **Content-Type** → Specifies returned data format.
* **Set-Cookie** → Stores cookies on the client.

---

# Cookies

Cookies are small pieces of data stored in a user's browser.

Since HTTP is stateless, cookies help websites remember users between requests.

### Common Uses

* User authentication
* Session management
* User preferences
* Tracking visits

### Cookie Flow

```text
Server → Set-Cookie → Browser
Browser → Cookie → Server
```

### Important Headers

| Header     | Purpose                            |
| ---------- | ---------------------------------- |
| Set-Cookie | Saves cookie in browser            |
| Cookie     | Sends stored cookie back to server |

---

# Quick Revision

* HTTP = Web communication protocol
* HTTPS = Encrypted HTTP
* URL = Address of a web resource
* GET = Retrieve data
* POST = Submit data
* PUT = Update data
* DELETE = Remove data
* 200 = Success
* 201 = Resource created
* 401 = Unauthorized
* 403 = Forbidden
* 404 = Not Found
* 503 = Service Unavailable
* Host = Requested website
* User-Agent = Browser information
* Content-Type = Returned data type
* Cookies = Store user/session information
* Set-Cookie = Creates a cookie
