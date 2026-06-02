# Cryptography - Revision Notes

## Why Cryptography Matters

Cryptography helps protect:

* **Confidentiality** → Prevents unauthorized access to data.
* **Integrity** → Detects unauthorized modifications to data.

It converts readable information into unreadable data so only authorized users can access it.

---

# Basic Terms

## Plaintext

Readable, original data.

**Example:**

```
HELLO
```

## Ciphertext

Encrypted and unreadable version of data.

**Example:**

```
KHOOR
```

## Key

A secret value used during encryption and decryption.

## Algorithm

A set of rules used to encrypt and decrypt data.

### Encryption Process

```
Plaintext + Algorithm + Key = Ciphertext
```

### Decryption Process

```
Ciphertext + Algorithm + Key = Plaintext
```

---

# Caesar Cipher

One of the simplest encryption techniques.

### How It Works

Each letter is shifted by a fixed number of positions.

**Key = 3**

```
A → D
B → E
C → F
```

Example:

```
HELLO → KHOOR
```

To decrypt, shift letters backward by the same key.

### Important

* Algorithm is public.
* Key is secret.
* Used only for learning purposes.
* Not secure for real-world use.

---

# Symmetric Encryption

Uses **one shared key** for both encryption and decryption.

## Features

* Same key locks and unlocks data.
* Fast and efficient.
* Suitable for large amounts of data.
* Used for:

  * Files
  * Hard drives
  * Network traffic

## Problem

### Key Distribution Problem

Both parties need the same secret key.

If the key is intercepted during sharing, all encrypted data becomes exposed.

---

# Asymmetric Encryption

Uses **two keys**:

## Public Key

* Can be shared openly.
* Used for encryption.

## Private Key

* Must remain secret.
* Used for decryption.

### Rule

```
Public Key Encrypts
Private Key Decrypts
```

---

# Advantages of Asymmetric Encryption

* Solves the key distribution problem.
* No need to share a secret key beforehand.
* Provides secure communication over public networks.

---

# HTTPS and Encryption

When visiting secure websites:

1. Browser requests the website's public key.
2. Website sends its public key through a certificate.
3. Browser and website securely create a shared secret key.
4. Symmetric encryption is then used for the rest of the session.

---

# Digital Certificates

A certificate contains:

* Website identity
* Public key
* Certificate Authority (CA) signature
* Validity dates

Certificates help verify that you are communicating with the legitimate website.

---

# Symmetric vs Asymmetric Encryption

| Feature      | Symmetric       | Asymmetric           |
| ------------ | --------------- | -------------------- |
| Keys Used    | One Key         | Public + Private Key |
| Speed        | Fast            | Slower               |
| Key Sharing  | Difficult       | Easy                 |
| Main Purpose | Encrypting data | Secure key exchange  |
| Example Use  | Files, VPNs     | HTTPS Handshake      |

---

# Real-World Usage

Modern systems combine both:

1. **Asymmetric Encryption**

   * Securely exchanges a secret key.

2. **Symmetric Encryption**

   * Encrypts the actual communication.

This hybrid approach is used in:

* HTTPS
* VPNs
* Secure messaging applications
* Online banking

---

# Key Takeaways

* Cryptography protects confidentiality and integrity.
* Plaintext is readable; ciphertext is encrypted.
* Keys are secret; algorithms are generally public.
* Symmetric encryption uses one shared key.
* Asymmetric encryption uses public and private keys.
* Asymmetric encryption solves the key distribution problem.
* HTTPS combines asymmetric and symmetric encryption.
* Digital certificates verify website authenticity.
* Most secure systems use both encryption methods together.
