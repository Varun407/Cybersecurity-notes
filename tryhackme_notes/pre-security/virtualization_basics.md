# Virtualization Basics – Quick Notes

## Overview

Virtualization allows multiple applications and operating systems to share the same physical hardware efficiently.

### Why Virtualization Was Needed

Previously, the common approach was:

> One Server = One Application

This created several problems:

- High hardware and maintenance costs
- Low resource utilization (often only 5–20% used)
- Slow deployment of new services
- Difficult scalability

Virtualization solved these issues by allowing multiple virtual systems to run on a single physical server.

---

## Virtualization

Virtualization enables multiple independent virtual computers to share a single physical server.

### Benefits

- Better hardware utilization
- Reduced costs
- Faster deployment
- Easier scalability
- Improved flexibility

### Key Components

| Component | Description |
|------------|------------|
| Physical Server | Actual hardware |
| Hypervisor | Software that manages virtualization |
| VM (Lab Machine) | Virtual computer running on the server |

---

## Hypervisor

A **Hypervisor** is the software responsible for creating and managing virtual machines.

### Responsibilities

- Allocates CPU, RAM, and storage
- Isolates VMs from each other
- Starts, stops, pauses, and clones VMs
- Manages virtual resources

### Hypervisor Types

#### Type 1 (Bare Metal)

Runs directly on physical hardware.

**Best For**
- Production servers
- Databases
- Data centers
- Enterprise environments

#### Type 2 (Hosted)

Runs on top of an existing operating system.

**Best For**
- Learning labs
- Software testing
- Kali Linux practice
- Home environments

### Common Type 2 Hypervisors

- Oracle VirtualBox
- VMware Workstation

---

## Virtual Machines (VMs)

A **Virtual Machine (VM)**, also called a **Lab Machine**, is a virtual computer created by a hypervisor.

### Features

- Virtual CPU
- Virtual RAM
- Virtual Storage
- Virtual Network Adapter

### Advantages

- Runs its own operating system
- Isolated from other VMs
- Easy to create and remove
- Safe for testing and experimentation

### Common Use Cases

- Running Kali Linux
- Malware analysis
- Software testing
- Learning new operating systems

---

## Containers

Containers are lightweight environments used to run applications and their dependencies.

### Characteristics

- Share the host operating system kernel
- Start very quickly
- Use fewer resources than VMs
- Isolated from other containers

### Benefits

- Fast deployment
- Efficient resource usage
- Consistent application behavior
- Easy scalability

### Limitation

Containers must use the same OS family as the host.

**Example**
- Linux container → Linux host
- Windows container → Windows host

---

## Docker

**Docker** is the most popular platform for containerization.

### Functions

- Builds containers
- Deploys containers
- Runs applications consistently across systems

---

## VM vs Container

| Feature | VM | Container |
|-----------|----|-----------|
| Includes Full OS | ✅ | ❌ |
| Resource Usage | Higher | Lower |
| Startup Time | Slower | Faster |
| Isolation | Strong | Moderate |
| Scalability | Good | Excellent |

### Simple Analogy

- **VM = Apartment**
- **Container = Room inside the apartment**

VMs provide maximum separation, while containers focus on speed and efficiency.

---

## Virtualization Management

Organizations often use management platforms to monitor and control virtualization environments.

### Common Tasks

- Monitor VM health
- Restart failed VMs
- Create new VMs
- Allocate resources
- Track host performance

### VM States

- Running
- Stopped
- Paused
- Error

---

## Physical Hosts

A **Host** is the physical server running the hypervisor and VMs.

### Monitoring Metrics

- CPU usage
- Memory usage
- Storage utilization
- Number of hosted VMs
- Host availability

Proper host monitoring helps prevent resource exhaustion and downtime.

---

## Key Takeaways

- Virtualization allows multiple systems to share a physical server.
- Hypervisors create and manage virtual machines.
- Type 1 hypervisors run on hardware; Type 2 run on an operating system.
- VMs provide complete operating system isolation.
- Containers are lightweight and share the host kernel.
- Docker is widely used for container deployment.
- Virtualization improves efficiency, scalability, and cost savings.
- Hosts and VMs should be continuously monitored for performance and availability.
