# Data Representation - Revision Notes

## Why Data Representation Matters

* Computers only understand **0 and 1**.
* Everything (numbers, colors, text, images) is stored using binary.
* Understanding binary and hexadecimal is important in cybersecurity.

---

# Bits and Bytes

## Bit

* Short for **Binary Digit**.
* Can only be:

  * `0`
  * `1`

## Byte

* 8 bits = 1 byte
* Also called an **octet**.

Examples:

```text
1 bit  = 2 states
8 bits = 256 states
```

---

# Computer Colors

Computers create colors using:

* Red (R)
* Green (G)
* Blue (B)

This is called the **RGB color model**.

---

## 8-Color System

Each color can be:

* ON (1)
* OFF (0)

Total colors:

```text
2 × 2 × 2 = 8 colors
```

Examples:

| Binary | Color   |
| ------ | ------- |
| 000    | Black   |
| 001    | Blue    |
| 010    | Green   |
| 100    | Red     |
| 011    | Cyan    |
| 101    | Magenta |
| 110    | Yellow  |
| 111    | White   |

---

## 24-Bit Colors

Modern systems use:

```text
8 bits Red
8 bits Green
8 bits Blue
```

Total:

```text
24 bits = 3 bytes
```

Possible colors:

```text
256 × 256 × 256
= 16,777,216 colors
```

---

# Hexadecimal

Hexadecimal (Base-16) is a shorter way to represent binary.

Uses:

```text
0 1 2 3 4 5 6 7 8 9 A B C D E F
```

Where:

```text
A = 10
B = 11
C = 12
D = 13
E = 14
F = 15
```

---

## Binary ↔ Hex Conversion

| Hex | Binary |
| --- | ------ |
| 0   | 0000   |
| 1   | 0001   |
| 2   | 0010   |
| 3   | 0011   |
| 4   | 0100   |
| 5   | 0101   |
| 6   | 0110   |
| 7   | 0111   |
| 8   | 1000   |
| 9   | 1001   |
| A   | 1010   |
| B   | 1011   |
| C   | 1100   |
| D   | 1101   |
| E   | 1110   |
| F   | 1111   |

---

## Important Facts

* 1 Hex digit = 4 bits
* 2 Hex digits = 1 byte
* FF = 255
* FFFFFF = 16,777,215

---

# Hex Color Codes

Examples:

```text
#FF0000 → Red
#00FF00 → Green
#0000FF → Blue
#FFFFFF → White
#000000 → Black
```

Format:

```text
#RRGGBB
```

Example:

```text
#3BC81E
```

* Red = 3B
* Green = C8
* Blue = 1E

---

# Number Systems

## Decimal (Base 10)

Used by humans.

Digits:

```text
0 - 9
```

Example:

```text
213
```

---

## Binary (Base 2)

Used by computers.

Digits:

```text
0 and 1
```

Examples:

| Binary | Decimal |
| ------ | ------- |
| 0000   | 0       |
| 0001   | 1       |
| 0010   | 2       |
| 0011   | 3       |
| 1001   | 9       |
| 1111   | 15      |

---

## Quick Binary Values

Remember:

```text
128 64 32 16 8 4 2 1
```

Example:

```text
11111111
```

= 128+64+32+16+8+4+2+1

= 255

---

## Octal (Base 8)

Uses digits:

```text
0 - 7
```

Each octal digit represents:

```text
3 bits
```

Example:

```text
357₈ = 239₁₀
```

Less common today but still appears in Linux permissions.

---

# Cybersecurity Relevance

You will frequently see:

* IP addresses
* MAC addresses
* Memory addresses
* File signatures
* Packet captures
* Hash values
* Color values in web development

Most are displayed using:

* Binary
* Hexadecimal

Understanding hex and binary makes analysis much easier.

---

# Quick Revision

### Key Terms

```text
Bit  = 1 binary digit
Byte = 8 bits
```

### Number Systems

```text
Decimal = Base 10
Binary = Base 2
Octal = Base 8
Hex     = Base 16
```

### Useful Facts

```text
1 Hex digit = 4 bits
2 Hex digits = 1 byte
FF = 255
FFFFFF = 16,777,215
24-bit color = 16.7 million colors
```

### RGB Color Format

```text
#RRGGBB
```

Example:

```text
#FF0000 = Red
#00FF00 = Green
#0000FF = Blue
```
