# 03. Identity & Access

## Overview

This section documents the centralized identity and access management architecture implemented within the HomeLab environment.

The environment utilizes Active Directory Domain Services (AD DS), security groups, role-based access control, certificate services, and structured administrative delegation to simulate common enterprise identity management practices.

---

## Table of Contents

- [Active Directory Domain Services](#active-directory-domain-services)
- [Organizational Unit Design](#organizational-unit-design)
- [User Management](#user-management)
- [Security Group Design](#security-group-design)
- [AGDLP Permission Model](#agdlp-permission-model)
- [Authentication Concepts](#authentication-concepts)
- [Active Directory Certificate Services (AD CS)](#active-directory-certificate-services-ad-cs)
- [Certificate Auto Enrollment](#certificate-auto-enrollment)
- [Certificate Templates](#certificate-templates)
- [Identity Security Principles](#identity-security-principles)
- [Validation](#validation)

---

## Active Directory Domain Services

### Environment

| Component | Value |
|------------|------------|
| Domain Name | home.lab |
| Domain Controller | DC-01 |
| Operating System | Windows Server 2025 |
| Functional Purpose | Centralized Identity Management |

### Core Services

- Active Directory Domain Services (AD DS)
- DNS
- Group Policy Management
- Active Directory Certificate Services (AD CS)

---

## Organizational Unit Design

The Active Directory structure is organized into dedicated Organizational Units (OUs) to simplify administration, policy assignment, and future scalability.

### OU Structure

```text
home.lab
│
├── Admin Accounts
├── Service Accounts
│
├── HR
│   ├── Users
│   └── Clients
│
├── Finance
│   ├── Users
│   └── Clients
│
├── IT
│   ├── Users
│   └── Clients
│
├── Infrastructure
│   ├── Servers
│   └── Hypervisors
│
└── Groups
    ├── Administrative
    ├── Departments
    ├── File Shares
    └── Security Groups
```

---

## User Management

User accounts are centrally managed through Active Directory and utilize unique numeric logon identifiers for authentication.

### Example User Account

```text
Display Name: Max Mustermann
Logon Name: 100001
```

### Administrative Accounts

Administrative activities are performed using dedicated privileged accounts.

Examples:

```text
adm_ada_100001
adm_server_100001
adm_client_100001
```

This separation follows the principle of least privilege and reduces exposure of privileged credentials.

### Service Accounts

Dedicated service accounts are used for applications and services requiring authentication within the environment.

Examples:

```text
svc_monitoring
svc_backup
svc_application
```

---

## Security Group Design

The environment utilizes role-based access control through Active Directory security groups.

### Department Groups

```text
GG_HR_Users
GG_FIN_Users
GG_IT_Users
```

Purpose:

- Department membership
- Policy targeting
- Resource access control

### Administrative Groups

```text
GG_Client_Admins
GG_Server_Admins
GG_Hypervisor_Admins
```

Purpose:

- Role-based administration
- Centralized privilege assignment
- Local administrator delegation

### File Share Groups

```text
DL_HR_Share_RW
DL_HR_Share_RO

DL_FIN_Share_RW
DL_FIN_Share_RO

DL_IT_Share_RW
DL_IT_Share_RO
```

Purpose:

- File share permissions
- NTFS access control
- Resource authorization

---

## AGDLP Permission Model

The HomeLab implements the Microsoft AGDLP model for access management.

### Overview

```text
Account
  ↓
Global Group
  ↓
Domain Local Group
  ↓
Permission
```

### Example

```text
100001
  ↓
GG_HR_Users
  ↓
DL_HR_Share_RW
  ↓
\\FILE01\HR
```

---

## Authentication Concepts

The environment uses centralized authentication through Active Directory.

Authentication methods include:

- Kerberos Authentication
- NTLM Authentication
- Domain-Based Login
- Certificate-Based Authentication

---

## Active Directory Certificate Services (AD CS)

### Purpose

The HomeLab includes an internal Public Key Infrastructure (PKI) using Active Directory Certificate Services.

The certificate authority provides:

- Internal certificate issuance
- Automatic certificate enrollment
- Certificate lifecycle management
- Secure authentication services

### Certificate Authority

```text
CA-01.home.lab
```

Role:

```text
Enterprise Root Certification Authority
```

---

## Certificate Auto Enrollment

Certificate deployment is automated through Group Policy.

### Configured Features

- Automatic Enrollment
- Automatic Renewal
- Revoked Certificate Cleanup
- Certificate Template Deployment

### Benefits

- Reduced administrative effort
- Consistent certificate deployment
- Improved security posture

---

## Certificate Templates

The following certificate templates are currently deployed within the HomeLab environment.

### Computer Certificate

Purpose:

- Device authentication
- Internal service trust
- Automatic certificate enrollment

Status:

- Implemented and validated through Group Policy Auto Enrollment

### Domain Controller Certificates

Purpose:

- Kerberos authentication
- Domain controller authentication
- Active Directory secure communications

Status:

- Automatically issued by the Enterprise Certification Authority

## Identity Security Principles

The environment is designed around the following security concepts:

- Principle of Least Privilege
- Role-Based Access Control (RBAC)
- Separation of Administrative Accounts
- Group-Based Authorization
- Centralized Authentication
- Certificate-Based Trust
- Structured Access Management

---

## Validation

The following identity management functions have been validated:

- Domain user authentication
- Security group membership
- AGDLP access model
- Certificate auto enrollment
- Administrative account separation
- Group Policy integration
- Resource authorization through security groups

