# Data Encoding - Revision Notes

## What I Learned

Computers do not store letters or symbols directly. Everything is stored as numbers, and an **encoding** defines which number represents which character.

**Representation** refers to how data is stored as bits (0s and 1s), while **Encoding** is the mapping between those numbers and their meanings.

Using the wrong encoding can cause text to appear as unreadable or corrupted characters.

---

## ASCII

- ASCII stands for **American Standard Code for Information Interchange**.
- One of the earliest character encoding standards.
- Uses **7 bits**.
- Supports **128 characters**.
- Includes:
  - English letters (A-Z, a-z)
  - Numbers (0-9)
  - Basic symbols and punctuation
  - Control characters

### Common ASCII Values

| Character | Decimal |
|-----------|---------|
| A | 65 |
| a | 97 |
| 0 | 48 |
| @ | 64 |
| # | 35 |

### Key Point

ASCII is limited to English characters and cannot fully support many other languages.

---

## Extended ASCII

Extended ASCII standards were created to support additional European languages.

Examples:

- **ISO-8859-1 (Latin-1)** → Western European languages
- **ISO-8859-2 (Latin-2)** → Central and Eastern European languages

Different encoding standards can display characters differently if the wrong one is used.

---

## Unicode

Unicode was created to provide a universal character standard.

- Assigns a unique code point to each character.
- Supports characters from languages around the world.
- Allows multiple languages to be used within the same document.
- Solves many compatibility issues caused by older encoding standards.

### Examples

| Character | Unicode |
|-----------|----------|
| A | U+0041 |
| Ω | U+03A9 |
| あ | U+3042 |
| 龍 | U+9F8D |

---

## UTF Encodings

Unicode characters are stored using UTF encodings.

### UTF-8

- Most common encoding on modern systems and websites.
- Uses **1–4 bytes** per character.
- Compatible with ASCII.
- Efficient and widely used.

### UTF-16

- Uses **2 or 4 bytes** per character.
- Common characters usually require 2 bytes.

### UTF-32

- Uses **4 bytes** for every character.
- Simple but consumes more storage space.

---

## Key Concepts to Remember

- Representation = How data is stored as bits.
- Encoding = How numbers are mapped to characters.
- ASCII uses 7 bits and supports 128 characters.
- Unicode provides a universal character set.
- UTF-8 is the most widely used encoding.
- UTF-16 uses 2 or 4 bytes.
- UTF-32 always uses 4 bytes.
- Using the wrong encoding can result in unreadable text.

---

## Room Answers

- ASCII code for **@** = 64
- Character with ASCII code **35** = #
- ASCII code **7** = BEL (Bell)
- UTF-32 of 😌 = U+0001F60C
- UTF-16 of シ = U+30B7
- UTF-16 U+2615 = ☕
- UTF-16 U+2658 = ♘ (White Knight)

---

## Quick Revision

- Computers store text as numbers.
- ASCII is the basic character encoding standard.
- Unicode supports characters from almost all languages.
- UTF-8 is the most commonly used Unicode encoding.
- UTF-16 and UTF-32 are alternative Unicode encodings.
- Encoding ensures characters are displayed correctly across different systems.
