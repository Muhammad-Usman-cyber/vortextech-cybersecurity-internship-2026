# Week 2 — Hands-On with Basic Security Tools

## Overview

This project was completed as part of Week 2 of the Vortex Tech Cyber
Security Internship 2026.

The objective of this week is to move from theoretical security concepts
into practical security tooling by building and using two foundational
security tools:

1. A Python-based password strength evaluator
2. Nmap for basic local network port scanning

All testing is performed only on systems and networks that I own or have
explicit permission to test.

---

## Objectives

- Build a simple password strength evaluation script using Python.
- Evaluate passwords based on length and character variety.
- Identify extremely common passwords.
- Assign password strength ratings based on multiple checks.
- Use Nmap to identify open ports on an authorized system/network.
- Identify the services commonly associated with discovered ports.
- Understand the security risks associated with weak passwords and
  unnecessarily exposed network services.
- Document practical security observations and findings.

---

## Tools Used

- Python 3
- Nmap
- Kali Linux
- GitHub

---

## Project Components

### 1. Password Strength Evaluator

A Python script will evaluate passwords based on:

- Minimum password length
- Uppercase characters
- Lowercase characters
- Numbers
- Special characters
- Common-password checks

The script will provide a strength rating:

- Weak
- Medium
- Strong

It will also provide feedback explaining how the password could be improved.

### 2. Nmap Port Scanning

Nmap will be used to perform a basic port scan against an authorized
local system/network.

The scan results will be documented, including:

- Open ports
- Port numbers
- Likely services
- Security implications

---

## Ethical Scope

All network scanning performed as part of this project is limited to
systems and networks that I own or have explicit permission to test.

No third-party systems or networks are intentionally scanned.

---

## Project Status

**Completed — Week 2**

The password strength evaluator was implemented and tested with multiple test cases.

An authorized Nmap scan was also performed against the Windows 10 virtual machine in the local VirtualBox cybersecurity lab.

The project results, observations, and supporting screenshots have been documented in this repository.

---

## How to Run

### Password Strength Evaluator

1. Make sure Python 3 is installed.
2. Run:
   ```bash
   python3 password_checker.py
   ```
3. Enter a test password when prompted.
4. The program will display a strength rating and feedback.

---

### Nmap

1. Install Nmap on a supported system and run the scan against an authorized target.

   **Example:**
   ```bash
   nmap 192.168.56.103
   ```
2. **For service detection:**
   ```bash
   nmap -sV 192.168.56.103
   ```

> **Warning:** Only scan systems and networks that you own or have explicit permission to test.
