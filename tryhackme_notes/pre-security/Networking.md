# What is Networking?

## Network
A network is a group of connected devices or systems that communicate with each other.

---

## Real-Life Examples of Networks
- Friendship circles
- Public transportation systems
- Postal systems
- National power grids

---

## Networks in Computing

In computing, networks connect devices such as:
- Computers
- Phones
- Servers
- Security cameras
- Traffic lights
- Smart devices

A network can contain:
- 2 devices
- Millions or billions of devices

---

## Importance of Networking in Cybersecurity

Networking is important because modern systems rely heavily on networks.

Examples:
- Internet communication
- Weather systems
- Electricity distribution
- Smart traffic systems

Understanding networking is essential in cybersecurity.

---

# The Internet

## What is the Internet?

The Internet is a massive global network made up of many smaller networks connected together.

It is often called:
- A network of networks

---

## Example Concept

Imagine:
- Alice can communicate with Bob and Jim
- Alice can also communicate with Zayn and Toby

Since Alice understands both sides, she acts as a messenger between them.

Similarly, networks communicate through interconnected devices and systems.

---

# History of the Internet

## ARPANET
- Created in the late 1960s
- Funded by the United States Department of Defense
- First documented computer network

---

## World Wide Web (WWW)

- Invented in 1989 by Tim Berners-Lee
- Allowed people to store, access, and share information through the Internet

---

# Types of Networks

## Private Network
A network used internally within homes, schools, or organizations.

### Examples
- Home Wi-Fi
- School network
- Office network

---

## Public Network
Networks that connect private networks together.

### Example
- The Internet

---

# Identifying Devices on a Network

Devices on a network need identifiers to communicate properly.

Humans can be identified using:
- Names
- Fingerprints

Similarly, devices use:
- IP Address
- MAC Address

---

# IP Address

IP stands for:
- Internet Protocol

An IP address identifies a device on a network.

IP addresses:
- Can change over time
- Cannot be used by two devices simultaneously on the same network
- Follow networking protocols

---

## IPv4 Address Structure

IPv4 addresses contain:
- Four octets
- Separated by dots

Example:

192.168.1.1

Each section is called an octet.

---

# Types of IP Addresses

## Private IP Address

Used inside local/private networks.

### Examples
- Home networks
- School networks
- Company networks

Example:

192.168.1.77

Devices inside the same network use private IPs to communicate.

---

## Public IP Address

Used to identify devices on the Internet.

Assigned by:
- ISP (Internet Service Provider)

Example:

86.157.52.21

Multiple devices inside the same home network can share one public IP address while accessing the Internet.

---

# IPv4 vs IPv6

## IPv4
- Older addressing system
- Uses 32-bit addressing
- Supports around 4.29 billion addresses

Example:

192.168.1.1

---

## IPv6
- Newer addressing system
- Uses 128-bit addressing
- Supports a huge number of addresses
- More efficient than IPv4

Example:

2001:0db8:85a3:0000:0000:8a2e:0370:7334

---

# MAC Address

MAC stands for:
- Media Access Control

A MAC address is a unique physical address assigned to a device's network interface card (NIC).

Example:

a4:c3:f0:85:ac:2d

---

## MAC Address Structure

- 12 hexadecimal characters
- Split into pairs using colons

### First 6 Characters
Identify the manufacturer.

### Last 6 Characters
Unique device identifier.

---

# MAC Spoofing

MAC spoofing is the process of changing or faking a MAC address.

Attackers may spoof MAC addresses to:
- Bypass restrictions
- Impersonate trusted devices
- Gain unauthorized access

---

# Real-World Example

Hotels and cafes may use MAC filtering for paid Wi-Fi access.

Only approved MAC addresses can access the Internet.

If someone copies a valid MAC address:
- The network may mistakenly allow access.

---

# Ping

Ping is a basic networking tool used to test connectivity between devices.

Ping uses:
- ICMP (Internet Control Message Protocol)

It helps determine:
- Whether a connection exists
- Whether the connection is reliable
- The response time between devices

---

# How Ping Works

Ping sends:
- ICMP Echo Request packets

The target device responds with:
- ICMP Echo Reply packets

The time taken for the communication is measured in milliseconds (ms).

---

# Basic Ping Syntax

## Ping an IP Address

```bash
ping 192.168.1.254

---

Ping a Website

ping google.com

---

Example

ping 8.8.8.8

8.8.8.8 is Google's public DNS server.

---

Sample Output

64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=14.2 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=117 time=13.8 ms

---

Important Information in Ping Results

Time

- Measured in milliseconds (ms)
- Lower time means faster response

---

Packet Loss

Shows whether packets failed to reach the destination.

Example:

- 0% packet loss = stable connection

---

TTL (Time To Live)

Limits how long packets can travel across networks before being discarded.

---

Uses of Ping

- Test connectivity
- Troubleshoot network problems
- Check whether a device is online
- Measure network latency
- Verify communication between devices

---

ICMP (Internet Control Message Protocol)

ICMP is a protocol used for:

- Error reporting
- Diagnostics
- Network troubleshooting

Ping relies on ICMP for communication.

---

Key Points

- Ping tests connectivity between devices
- Ping uses ICMP packets
- Lower ping time means better connection
- Ping works with both IP addresses and websites
