# Packets and Frames

## Packets

A **packet** is a unit of data transmitted across a network.

* Contains the actual data and routing information.
* Operates at the **Network Layer (Layer 3)**.
* Uses **IP addresses** to identify source and destination.
* Large data is divided into multiple packets before transmission.

### Key Point

> Packet = Data + IP Addressing Information

---

## Frames

A **frame** is a packet wrapped with additional information used by the Data Link Layer.

* Operates at the **Data Link Layer (Layer 2)**.
* Contains **MAC addresses** for local delivery.
* Used to send data between devices on the same network segment.
* Provides error detection mechanisms.

### Key Point

> Frame = Packet + Data Link Layer Information

---

## Packet vs Frame

| Packet                           | Frame                             |
| -------------------------------- | --------------------------------- |
| Layer 3 (Network)                | Layer 2 (Data Link)               |
| Uses IP Addresses                | Uses MAC Addresses                |
| Handles routing between networks | Handles delivery on local network |

---

# TCP/IP

## TCP (Transmission Control Protocol)

TCP is a **connection-oriented** protocol designed for reliable communication.

### Features

* Establishes a connection before sending data.
* Performs error checking.
* Guarantees packet delivery.
* Maintains packet order.
* Retransmits lost packets.

### Common Uses

* Web browsing (HTTP/HTTPS)
* Email
* File transfers

### Important Header Fields

| Field                 | Purpose                |
| --------------------- | ---------------------- |
| Source Port           | Sending application    |
| Destination Port      | Receiving application  |
| Source IP             | Sender address         |
| Destination IP        | Receiver address       |
| Sequence Number       | Maintains packet order |
| Acknowledgment Number | Confirms received data |
| Checksum              | Error detection        |
| Flags                 | Connection control     |

### Checksum

Used to verify data integrity and detect transmission errors.

---

## TCP Three-Way Handshake

TCP establishes a connection using a three-step process:

```text
SYN → SYN/ACK → ACK
```

### Steps

1. **SYN** → Client requests connection.
2. **SYN/ACK** → Server acknowledges and responds.
3. **ACK** → Client confirms connection.

After this process, data transfer begins.

### Common TCP Flags

| Flag | Purpose                   |
| ---- | ------------------------- |
| SYN  | Start connection          |
| ACK  | Acknowledge received data |
| FIN  | Close connection          |
| RST  | Reset connection          |

---

# UDP/IP

## UDP (User Datagram Protocol)

UDP is a **connectionless (stateless)** protocol.

### Features

* No handshake.
* No error checking.
* No delivery guarantee.
* Faster than TCP.
* Lower overhead.

### Common Uses

* Video streaming
* Voice calls (VoIP)
* Online gaming
* DNS queries

### Key Point

> TCP prioritizes reliability.
> UDP prioritizes speed.

---

## TCP vs UDP

| TCP                 | UDP                                 |
| ------------------- | ----------------------------------- |
| Connection-oriented | Connectionless                      |
| Reliable            | Unreliable                          |
| Error checking      | Minimal error checking              |
| Slower              | Faster                              |
| File transfers      | Streaming & real-time communication |

### Rule of Thumb

* File transfer → TCP
* Email → TCP
* Web browsing → TCP
* Video call → UDP
* Live streaming → UDP

---

# Ports

A **port** identifies a specific service or application running on a device.

A device can have one IP address but multiple open ports.

### Examples

| Port | Service |
| ---- | ------- |
| 80   | HTTP    |
| 443  | HTTPS   |
| 21   | FTP     |
| 22   | SSH     |
| 25   | SMTP    |

### Key Point

> IP Address identifies the device.
> Port identifies the service running on the device.

---

# Quick Revision

* Packet = Data + IP Address
* Frame = Packet + MAC Address
* TCP = Reliable, connection-oriented
* UDP = Fast, connectionless
* Checksum = Error detection
* Three-Way Handshake = SYN → SYN/ACK → ACK
* Port = Identifies a service
* IP Address = Identifies a device
* MAC Address = Physical device address
