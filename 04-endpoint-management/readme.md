# 04. Endpoint Management

## Overview

This section documents the Group Policy and endpoint management configuration implemented within the HomeLab environment.

Policies are used to provide centralized configuration management, security baselines, endpoint hardening, certificate deployment, and department-specific workstation settings.

---

## Table of Contents

- [GPO Structure](#gpo-structure)
- [Client Baseline Policy](#client-baseline-policy)
- [Endpoint Hardening](#endpoint-hardening)
- [Cryptography Hardening](#cryptography-hardening)
- [Server Baseline Policy](#server-baseline-policy)
- [Server Hardening](#server-hardening)
- [RDP Hardening](#rdp-hardening)
- [Windows Update Policy](#windows-update-policy)
- [Browser Policy](#browser-policy)
- [Client Local Administrators](#client-local-administrators)
- [Department Workstation Policies](#department-workstation-policies)
- [Certificate Auto Enrollment](#certificate-auto-enrollment)
- [Security Benefits](#security-benefits)

---

## GPO Structure

```text
home.lab
│
├── Default Domain Policy
├── Certificate Auto Enrollment
│
├── Cryptography Hardening
│
├── Infrastructure
│   ├── Server Baseline Policy
│   ├── Server Hardening
│   └── RDP Hardening
│
├── Workstations
│   ├── Client Baseline Policy
│   ├── Endpoint Hardening
│   ├── Browser Policy
│   ├── Windows Update Policy
│   └── Client Local Administrators
│
├── Users
│   ├── Finance Workstation Policy
│   ├── HR Workstation Policy
│   └── IT Workstation Policy
```

---

## Client Baseline Policy

### Purpose

Provides common security and operating system settings for all Windows clients.

### Configuration Examples

#### Account Security

- Disable Guest Account
- Disable Anonymous SID Enumeration
- Enable User Account Control (UAC)

#### Audit Logging

- Logon Events
- Account Logon
- Account Management
- Policy Change
- Object Access

#### Windows Defender

- Real-Time Protection Enabled
- Cloud Protection Enabled
- Tamper Protection Enabled

#### Windows Firewall

- Firewall Enabled
- Inbound Connections Blocked by Default

---

## Endpoint Hardening

### Purpose

Reduce attack surface and improve endpoint security.

### Configuration Examples

#### SMB Hardening

- Disable SMBv1

#### WinRM Hardening

- Disable Basic Authentication
- Disable Unencrypted Traffic

#### PowerShell Logging

- Enable Module Logging
- Enable Script Block Logging

#### SmartScreen

- Enable SmartScreen

---

## Cryptography Hardening

### Purpose

Disable legacy cryptographic protocols and weak cipher suites.

### Implemented Controls

#### Disabled Protocols

- SSL 2.0
- SSL 3.0

#### Disabled Ciphers

- DES
- RC2
- RC4
- 3DES

#### Disabled Hashing Algorithms

- MD5

#### Preferred Protocols

- TLS 1.2
- TLS 1.3 (where supported)

---

## Server Baseline Policy

### Purpose

Provides standardized security and operating system settings for Windows servers.

### Configuration Examples

- Windows Firewall Configuration
- Audit Policy Configuration
- Microsoft Defender Settings
- Account Security Policies
- Event Logging

---

## Server Hardening

### Purpose

Reduce the attack surface of infrastructure systems and administrative servers.

### Configuration Examples

- SMB Hardening
- PowerShell Logging
- WinRM Hardening
- Security Option Configuration
- Service Hardening

---

## RDP Hardening

### Purpose

Secure Remote Desktop access to administrative systems.

### Configuration Examples

#### Security Layer

- Require SSL

#### Authentication

- Require Network Level Authentication (NLA)

#### Encryption

- High Encryption Level

#### RPC Security

- Require Secure RPC Communication

---

## Windows Update Policy

### Purpose

Provide centralized Windows Update management for domain-joined workstations.

### Configuration Examples

- Configure Automatic Updates
- Scheduled Installation
- Automatic Restart Management
- Microsoft Update Enabled

---

## Browser Policy

### Purpose

Provide standardized browser configuration and security settings.

### Configuration Examples

- Managed Favorites
- Homepage Configuration
- Security Settings
- Browser Hardening

---

## Client Local Administrators

### Purpose

Manage local administrator access through centralized Active Directory group membership.

### Configuration Examples

- Restricted Local Administrator Access
- Group-Based Local Administrator Assignment
- Administrative Delegation

---

## Department Workstation Policies

### Purpose

Provide department-specific user configuration.

### HR Workstation Policy

- Department Drive Mapping
- Desktop Configuration

### Finance Workstation Policy

- Department Drive Mapping
- Desktop Configuration

### IT Workstation Policy

- Department Drive Mapping
- Desktop Configuration

---

## Certificate Auto Enrollment

### Purpose

Automatically deploy certificates issued by Active Directory Certificate Services (AD CS).

### Configured Features

- Automatic Enrollment
- Automatic Renewal
- Revoked Certificate Cleanup
- Certificate Template Deployment

---

## Security Benefits

This Group Policy design provides:

- Centralized Configuration Management
- Consistent Security Baselines
- Reduced Attack Surface
- Cryptographic Hardening
- Secure Remote Administration
- Improved Audit Visibility
- Enterprise-Inspired Administration Practices

The structure demonstrates practical Active Directory and Group Policy management concepts commonly used in enterprise Windows environments.