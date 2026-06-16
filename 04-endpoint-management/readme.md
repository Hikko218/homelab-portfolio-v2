# 04. Endpoint Management

## Overview

This section documents the Group Policy and endpoint management configuration used within the HomeLab environment.

Implemented policies include security baselines, endpoint hardening, Windows Update management, certificate deployment, and department-specific client settings.

---

## Table of Contents

- [GPO Structure](#gpo-structure)
- [Client Baseline Policy](#client-baseline-policy)
  - [Purpose](#purpose)
  - [Link Location](#link-location)
  - [Configuration Examples](#configuration-examples)
- [Endpoint Hardening](#endpoint-hardening)
- [Cryptography Hardening](#cryptography-hardening)
- [RDP Hardening](#rdp-hardening)
- [Windows Update Policy](#windows-update-policy)
- [Department Workstation Policies](#department-workstation-policies)
  - [Desktop Wallpaper](#desktop-wallpaper)
  - [Drive Mapping](#drive-mapping)
  - [Browser Configuration](#browser-configuration)
- [Certificate Auto Enrollment](#certificate-auto-enrollment)
- [Security Benefits](#security-benefits)

# GPO Structure

```text
home.lab
│
├── Default Domain Policy
├── Certificate Auto Enrollment
│
├── Client Baseline Policy
├── Endpoint Hardening
├── Cryptography Hardening
├── Windows Update Policy
├── RDP Hardening
│
├── HR Workstation Policy
├── IT Workstation Policy
└── Finance Workstation Policy
```

---

# Client Baseline Policy

## Purpose

Provides common security and operating system settings for all Windows clients.

## Link Location

```text
Lab
├── HR
│   └── Clients
├── IT
│   └── Clients
└── Finance
    └── Clients
```

## Configuration Examples

### Account Security

Path:

```text
Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Local Policies
→ Security Options
```

Settings:

- Disable Guest Account
- Disable Anonymous SID Enumeration
- Enable UAC

---

### Audit Logging

Path:

```text
Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Advanced Audit Policy Configuration
```

Enable:

- Logon Events
- Account Logon
- Account Management
- Policy Change
- Object Access

---

### Windows Defender

Path:

```text
Computer Configuration
→ Administrative Templates
→ Windows Components
→ Microsoft Defender Antivirus
```

Settings:

- Real-Time Protection Enabled
- Cloud Protection Enabled
- Tamper Protection Enabled

---

### Windows Firewall

Path:

```text
Computer Configuration
→ Windows Settings
→ Security Settings
→ Windows Defender Firewall
```

Settings:

- Firewall Enabled
- Inbound Connections Blocked by Default

---

# Endpoint Hardening

## Purpose

Reduce attack surface and improve endpoint security.

## Link Location

```text
HR\Clients
IT\Clients
Finance\Clients
```

## Configuration Examples

### SMB Hardening

Path:

```text
Computer Configuration
→ Administrative Templates
→ Network
→ Lanman Workstation
```

Settings:

- Disable SMBv1

---

### WinRM Hardening

Path:

```text
Computer Configuration
→ Administrative Templates
→ Windows Components
→ Windows Remote Management
```

Settings:

- Disable Basic Authentication
- Disable Unencrypted Traffic

---

### PowerShell Logging

Path:

```text
Computer Configuration
→ Administrative Templates
→ Windows Components
→ Windows PowerShell
```

Settings:

- Enable Module Logging
- Enable Script Block Logging

---

### SmartScreen

Path:

```text
Computer Configuration
→ Administrative Templates
→ Windows Components
→ File Explorer
```

Settings:

- Enable SmartScreen

---

# Cryptography Hardening

## Purpose

Disable legacy cryptographic protocols and weak cipher suites.

## Link Location

```text
HR\Clients
IT\Clients
Finance\Clients
Infrastructure\Servers
```

## Configuration Method

Path:

```text
Computer Configuration
→ Preferences
→ Windows Settings
→ Registry
```

## Disable Legacy Protocols

- SSL 2.0
- SSL 3.0

---

## Disable Weak Ciphers

- DES
- RC2
- RC4
- 3DES

---

## Disable Weak Hashing

- MD5

---

## Preferred Protocols

- TLS 1.2
- TLS 1.3 (where supported)

---

# RDP Hardening

## Purpose

Secure Remote Desktop access to administrative systems.

## Link Location

```text
Infrastructure
└── Servers
```

## Path

```text
Computer Configuration
→ Administrative Templates
→ Windows Components
→ Remote Desktop Services
```

## Configuration

### Security Layer

- Require SSL

### Authentication

- Require Network Level Authentication (NLA)

### Encryption

- High Encryption Level

### RPC Security

- Require Secure RPC Communication

---

# Windows Update Policy

## Purpose

Centralized Windows Update configuration.

## Link Location

```text
HR\Clients
IT\Clients
Finance\Clients
```

## Path

```text
Computer Configuration
→ Administrative Templates
→ Windows Components
→ Windows Update
```

## Configuration

- Configure Automatic Updates
- Scheduled Installation
- Automatic Restart Management
- Microsoft Update Enabled

---

# Department Workstation Policies

## Purpose

Department-specific user configuration.

Examples:

- HR Workstation Policy
- IT Workstation Policy
- Finance Workstation Policy

## Link Location

```text
HR\Users
IT\Users
Finance\Users
```

---

## Desktop Wallpaper

Path:

```text
User Configuration
→ Policies
→ Administrative Templates
→ Desktop
```

---

## Drive Mapping

Path:

```text
User Configuration
→ Preferences
→ Windows Settings
→ Drive Maps
```

Example:

```text
H: → \\FILE01\HR
I: → \\FILE01\IT
F: → \\FILE01\Finance
```

---

## Browser Configuration

Examples:

- Company Homepage
- Managed Favorites
- Security Settings

---

# Certificate Auto Enrollment

## Purpose

Automatically deploy certificates issued by Active Directory Certificate Services (AD CS).

## Link Location

```text
Domain Level
```

## Path

```text
Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Public Key Policies
```

Settings:

- Enable Certificate Auto Enrollment
- Renew Expired Certificates
- Update Pending Certificates

---

# Security Benefits

This GPO design provides:

- Centralized Configuration Management
- Consistent Security Baselines
- Reduced Attack Surface
- Cryptographic Hardening
- Secure Remote Administration
- Improved Audit Visibility
- Enterprise-Inspired Administration Practices

The structure demonstrates practical Active Directory and Group Policy management concepts commonly used in enterprise Windows environments.