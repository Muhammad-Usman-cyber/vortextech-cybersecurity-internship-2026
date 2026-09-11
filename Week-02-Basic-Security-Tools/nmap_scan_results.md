# Nmap Port Scan — Test Results

## Overview
Nmap was used to perform a basic port scan against an authorized Windows 10 virtual machine in my local cybersecurity lab environment.

* **Target System:** Windows 10 Virtual Machine
* **Target IP:** `192.168.56.103`
* **Scanner:** Kali Linux
* **Environment:** VirtualBox Host-Only Lab Network

> [!IMPORTANT]
> The scan was performed strictly within an isolated laboratory environment against a system that I own and control.

---

## Scan Scope

| Parameter | Details |
| :--- | :--- |
| **Target** | Windows 10 Virtual Machine |
| **Scanner** | Kali Linux |
| **Network** | VirtualBox Host-Only Lab Network |
| **Target IP** | `192.168.56.103` |

---

## Scan Execution & Results

### 1. Basic Nmap Scan
The initial default scan was executed to locate open TCP ports:

```bash
nmap 192.168.56.103
