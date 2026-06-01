# Introduction to LAN

## LAN (Local Area Network)

A LAN connects devices within a limited area such as a home, office, or school. The term **topology** refers to the layout or design of a network.

---

## Network Topologies

### Star Topology

* Devices connect to a central **switch** or **hub**.
* Most common topology used today.
* Easy to expand and manage.
* Failure of the central device affects the entire network.
* More expensive due to additional cabling and hardware.

### Bus Topology

* All devices share a single **backbone cable**.
* Cheap and easy to set up.
* Performance decreases as network traffic increases.
* Failure of the backbone cable brings down the whole network.

### Ring Topology

* Devices form a circular loop.
* Data travels through devices until it reaches its destination.
* Less prone to traffic bottlenecks.
* A single cable or device failure can disrupt the entire network.

| Topology | Main Component | Major Drawback                |
| -------- | -------------- | ----------------------------- |
| Star     | Switch/Hub     | Central device failure        |
| Bus      | Backbone Cable | Backbone cable failure        |
| Ring     | Circular Loop  | Any break affects the network |

---

## Switches

* Connect multiple devices within a LAN.
* Forward data only to the intended destination.
* Reduce unnecessary network traffic.
* More efficient than hubs.
* Available with different port capacities (4, 8, 16, 24, etc.).

---

## Routers

* Connect different networks together.
* Responsible for **routing**, the process of moving data between networks.
* Enable communication with external networks such as the Internet.

**Remember:**
Switch → Connects devices
Router → Connects networks

---

## Subnetting

Subnetting divides a large network into smaller networks (subnets).

### Benefits

* Better organization
* Improved security
* Easier management
* Efficient use of IP addresses

A subnet mask:

* Is 32 bits long.
* Consists of 4 octets.
* Uses values from 0–255 in each octet.

### Important Addresses

**Network Address**

* Identifies the network itself.
* Example: `192.168.1.0`

**Host Address**

* Identifies a device within the network.
* Example: `192.168.1.100`

**Default Gateway**

* Sends traffic to other networks.
* Commonly uses `.1` or `.254`.

---

## ARP (Address Resolution Protocol)

ARP maps an **IP address** to a **MAC address**.

### Process

1. ARP Request (broadcast).
2. ARP Reply (response from target device).
3. Mapping stored in the ARP Cache.

**Key Point**

* IP Address = Logical Address
* MAC Address = Physical Address

---

## DHCP (Dynamic Host Configuration Protocol)

DHCP automatically assigns IP addresses to devices joining a network.

### DORA Process

| Step | Meaning     |
| ---- | ----------- |
| D    | Discover    |
| O    | Offer       |
| R    | Request     |
| A    | Acknowledge |

**Flow:**
Discover → Offer → Request → ACK

---

## Quick Revision

* LAN = Local Area Network
* Topology = Network layout/design
* Star = Central switch/hub
* Bus = Single backbone cable
* Ring = Circular connection
* Switch = Connects devices
* Router = Connects networks
* Subnetting = Divides networks into smaller networks
* ARP = IP Address → MAC Address
* DHCP = Automatically assigns IP addresses using DORA
