# DNS (Domain Name System)

DNS translates human-readable domain names into IP addresses.

Instead of remembering:

```text
104.26.10.229
```

We can simply use:

```text
tryhackme.com
```

---

## Domain Hierarchy

### TLD (Top-Level Domain)

The rightmost part of a domain name.

Examples:

* `.com`
* `.org`
* `.edu`
* `.gov`
* `.co.uk`

### Types of TLDs

| Type  | Purpose                                       |
| ----- | --------------------------------------------- |
| gTLD  | Generic Top-Level Domain (.com, .org, .edu)   |
| ccTLD | Country Code Top-Level Domain (.uk, .ca, .in) |

---

### Second-Level Domain (SLD)

The main name registered under a TLD.

Example:

```text
tryhackme.com
^^^^^^^^^^
```

* Maximum length: **63 characters**
* Allowed characters: `a-z`, `0-9`, `-`

---

### Subdomain

A subdomain appears before the second-level domain.

Example:

```text
admin.tryhackme.com
```

* `admin` = Subdomain
* Maximum length: **63 characters**
* Cannot use `_`
* Full domain name length cannot exceed **253 characters**

### Example

```text
jupiter.servers.tryhackme.com
```

---

# Common DNS Record Types

## A Record

Maps a domain name to an **IPv4 address**.

Example:

```text
104.26.10.229
```

---

## AAAA Record

Maps a domain name to an **IPv6 address**.

Example:

```text
2606:4700:20::681a:be5
```

---

## CNAME Record

Points one domain name to another domain name.

Example:

```text
store.tryhackme.com
        ↓
shops.shopify.com
```

---

## MX Record

Specifies the mail server responsible for receiving emails.

### Features

* Used for email routing.
* Supports priority values.
* Backup mail servers can be configured.

---

## TXT Record

Stores text-based information.

Common uses:

* SPF records
* DMARC records
* Domain verification
* Email authentication

---

## Quick DNS Records Review

| Record | Purpose                  |
| ------ | ------------------------ |
| A      | IPv4 Address             |
| AAAA   | IPv6 Address             |
| CNAME  | Alias to another domain  |
| MX     | Mail Server              |
| TXT    | Text / Verification Data |

---

# DNS Resolution Process

When visiting a website, DNS follows a series of steps:

### 1. Local Cache

Your device checks whether the domain has been resolved recently.

### 2. Recursive DNS Server

Usually provided by your ISP.

* Checks its own cache.
* If not found, continues the lookup process.

### 3. Root DNS Server

Directs the request to the correct TLD server.

Example:

```text
.com
.org
.net
```

---

### 4. TLD Server

Knows which authoritative server manages the requested domain.

Example:

```text
tryhackme.com
```

---

### 5. Authoritative DNS Server

Contains the actual DNS records for the domain.

Returns records such as:

* A
* AAAA
* MX
* TXT
* CNAME

---

## DNS Lookup Flow

```text
Client
  ↓
Local Cache
  ↓
Recursive DNS Server
  ↓
Root Server
  ↓
TLD Server
  ↓
Authoritative DNS Server
  ↓
IP Address Returned
```

---

# TTL (Time To Live)

TTL determines how long a DNS response should be cached before a new lookup is required.

### Benefits

* Faster DNS lookups
* Reduced DNS traffic
* Improved performance

---

# Important Terms

| Term                 | Meaning                   |
| -------------------- | ------------------------- |
| DNS                  | Domain Name System        |
| TLD                  | Top-Level Domain          |
| SLD                  | Second-Level Domain       |
| Subdomain            | Child domain              |
| Recursive Server     | Performs DNS lookups      |
| Root Server          | Directs to TLD servers    |
| Authoritative Server | Stores actual DNS records |
| TTL                  | Cache lifetime            |

---

# Quick Revision

* DNS = Domain Name → IP Address
* TLD = `.com`, `.org`, `.co.uk`
* SLD = Main registered domain name
* Subdomain max length = 63 characters
* Maximum domain length = 253 characters
* A Record = IPv4
* AAAA Record = IPv6
* MX Record = Email server
* CNAME = Alias to another domain
* TXT Record = Verification / Text data
* Recursive DNS Server = Usually provided by ISP
* Authoritative DNS Server = Stores DNS records
* TTL = How long records remain cached
