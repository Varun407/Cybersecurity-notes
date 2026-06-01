# Extending Your Network

## Port Forwarding

Port Forwarding allows external devices on the Internet to access services running inside a private network.

* Configured on a **router**.
* Forwards incoming traffic from a public port to a specific device and port inside the LAN.
* Commonly used for hosting websites, game servers, and remote access services.

### Example

```text
Internet → Router → Internal Device
```

---

## Firewalls

A firewall controls which traffic is allowed to enter or leave a network.

### OSI Layers

* Layer 3 (Network)
* Layer 4 (Transport)

### Types of Firewalls

| Type      | Description                                                           |
| --------- | --------------------------------------------------------------------- |
| Stateful  | Inspects the entire connection and keeps track of session information |
| Stateless | Inspects packets individually using predefined rules                  |

### Common Firewall Actions

* Allow
* Deny
* Drop

### Key Point

> Stateful firewalls understand connections, while stateless firewalls only examine individual packets.

---

## VPN (Virtual Private Network)

A VPN creates a secure connection over an untrusted network such as the Internet.

### Benefits

* Encrypts data
* Protects privacy
* Enables secure remote access

### VPN Technologies

| Technology | Purpose                                      |
| ---------- | -------------------------------------------- |
| PPP        | Authentication and encryption                |
| PPTP       | VPN tunneling protocol                       |
| IPSec      | Secures communication using the IP framework |

### Key Point

> IPSec is one of the most widely used VPN security technologies.

---

## Routers

A router connects different networks and forwards data between them.

### Routing

Routing is the process of determining the path that data takes between networks.

### Functions

* Connects networks
* Forwards packets
* Selects the best route for traffic

---

## Switches

Switches connect devices within a network.

### Switch Types

| Layer   | Function                                        |
| ------- | ----------------------------------------------- |
| Layer 2 | Uses MAC addresses                              |
| Layer 3 | Uses IP addresses and supports routing features |

### Key Point

> Layer 2 switches forward frames, while Layer 3 switches can perform routing functions.

---

## Network Communication

When data travels across a network:

1. Source device creates data.
2. Data is encapsulated into packets.
3. Switches and routers forward the packets.
4. Destination device receives and processes the data.

### TCP Communication

Before data transfer begins, TCP establishes a connection using the Three-Way Handshake:

```text
SYN → SYN/ACK → ACK
```

---

## Quick Revision

* Port Forwarding = Redirect traffic from router to internal device
* Router = Connects networks
* Routing = Forwarding packets between networks
* Switch = Connects devices within a network
* Layer 2 Switch = Uses MAC addresses
* Layer 3 Switch = Uses IP addresses
* Firewall = Controls network traffic
* Stateful Firewall = Tracks connections
* Stateless Firewall = Inspects individual packets
* VPN = Secure encrypted connection
* PPP = Authentication & encryption
* IPSec = VPN security using IP
