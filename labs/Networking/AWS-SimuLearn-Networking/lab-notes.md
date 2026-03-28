# Lab Notes: AWS Networking Fundamentals

**Lab:** AWS SimuLearn — Networking  
**Date Completed:** <!-- Add your date -->  
**Focus:** Building, configuring, and troubleshooting core AWS networking components inside a VPC

---

## Overview

This lab documents my hands-on practice and conceptual understanding of AWS networking through SimuLearn. The focus was on building, configuring, and troubleshooting core networking components inside a Virtual Private Cloud (VPC) — part of my structured learning journey toward mastering AWS Cloud fundamentals.

---

## Objectives

- Understand how AWS networking components interact
- Configure secure communication between services
- Apply best practices for traffic control and segmentation
- Strengthen troubleshooting and architecture reasoning skills

---

## Core Concepts Covered

### Virtual Private Cloud (VPC)
- CIDR block configuration
- Logical network isolation
- Public vs private design patterns

### Subnets
- Public subnet configuration
- Private subnet configuration
- Multi-tier architecture layout

### Route Tables
- Internet Gateway routing
- Internal VPC communication
- Route propagation behavior

### Internet Gateway (IGW)
- Enabling public internet access
- Attaching IGW to VPC
- Public subnet routing logic

### NAT Gateway
- Allowing private subnet outbound internet access
- Secure internal resource architecture

### Security Groups
- Stateful firewall behavior
- Inbound vs outbound rules
- Instance-to-instance communication
- MySQL (port 3306) configuration between Web and DB servers

### Network ACLs (NACLs)
- Stateless traffic filtering
- Rule ordering and evaluation
- Subnet-level security control

---

## Architecture Scenario Practiced
```
Web Server (10.10.0.0/24)
        ⬇
Security Group allows TCP 3306
        ⬇
DB Server (10.10.2.0/24)
```

**Key learning:** Security Groups are stateful and should allow inbound MySQL traffic from the `WebServerSecurityGroup` rather than opening CIDR-wide access (`0.0.0.0/0`).

---

## Security Best Practices Applied

- Principle of Least Privilege
- Avoiding `0.0.0.0/0` for database access
- Using Security Group referencing for internal communication
- Separating public-facing and private resources

---

## Skills Demonstrated

- Network troubleshooting
- Traffic flow analysis
- CIDR reasoning
- Architecture diagram interpretation
- Secure AWS configuration
