# OSI Model

The **OSI (Open Systems Interconnection) Model** is a framework that explains how data travels between devices on a network.

It consists of **7 layers**, where each layer has a specific responsibility.

## Mnemonic

**A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing

| Layer | Name         |
| ----- | ------------ |
| 7     | Application  |
| 6     | Presentation |
| 5     | Session      |
| 4     | Transport    |
| 3     | Network      |
| 2     | Data Link    |
| 1     | Physical     |

**Encapsulation** is the process of adding information to data as it moves down the OSI layers.

---

## Layer 7 - Application

* Closest layer to the user.
* Provides services for applications to communicate over a network.
* Contains protocols such as DNS, HTTP, HTTPS, SMTP, etc.
* Users interact through a **GUI (Graphical User Interface)**.

**Key Idea:** User interaction with network services.

---

## Layer 6 - Presentation

* Acts as a **translator** between applications and the network.
* Ensures data is presented in a readable format.
* Handles **encryption** and **decryption**.
* Responsible for data formatting.

**Key Idea:** Translation and encryption.

---

## Layer 5 - Session

* Establishes, manages, and terminates connections between devices.
* Creates a **session** before communication begins.
* Splits data into smaller chunks called **packets**.

**Key Idea:** Managing communication sessions.

---

## Layer 4 - Transport

Responsible for end-to-end data delivery.

### TCP (Transmission Control Protocol)

* Reliable and connection-oriented.
* Performs error checking.
* Guarantees packet delivery and correct order.

**Used for:**

* Web browsing
* Email
* File transfers

### UDP (User Datagram Protocol)

* Fast but unreliable.
* No error checking.
* No guarantee of delivery.

**Used for:**

* Video streaming
* VoIP
* Online gaming

**Key Idea:** TCP = Reliability, UDP = Speed.

---

## Layer 3 - Network

* Handles routing and packet forwarding.
* Uses **IP Addresses**.
* Determines the best path for data.

### Routing Protocols

* **OSPF** – Open Shortest Path First
* **RIP** – Routing Information Protocol

### Layer 3 Device

* Router

**Key Idea:** Routing using IP addresses.

---

## Layer 2 - Data Link

* Handles physical addressing.
* Uses **MAC Addresses**.
* Adds sender and receiver MAC addresses to frames.
* Works closely with the Network Interface Card (NIC).

### Layer 2 Device

* Switch

**Key Idea:** Communication using MAC addresses.

---

## Layer 1 - Physical

* Lowest layer of the OSI model.
* Deals with physical hardware and transmission media.
* Transfers data as electrical signals (0s and 1s).

### Examples

* Ethernet cables
* Network connectors
* Hubs

**Key Idea:** Physical transmission of binary data.

---

## Quick Revision

| Layer        | Main Function            |
| ------------ | ------------------------ |
| Application  | User interaction         |
| Presentation | Translation & Encryption |
| Session      | Session management       |
| Transport    | TCP / UDP                |
| Network      | Routing & IP Addresses   |
| Data Link    | MAC Addresses            |
| Physical     | Cables & Signals         |

### Devices by Layer

| Layer     | Device      |
| --------- | ----------- |
| Network   | Router      |
| Data Link | Switch      |
| Physical  | Hub / Cable |

### Important Terms

* **OSI** = Open Systems Interconnection
* **Encapsulation** = Adding information to data
* **TCP** = Reliable communication
* **UDP** = Fast communication
* **IP Address** = Logical address
* **MAC Address** = Physical address
* **NIC** = Network Interface Card
