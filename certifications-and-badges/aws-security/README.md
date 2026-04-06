# 🔒 AWS SimuLearn: Core Security Concepts

> **Badge earned:** April 7, 2026 | **Issuer:** Amazon Web Services

---

## What is AWS SimuLearn?

**AWS SimuLearn** is a simulation-based learning platform where you make real architectural decisions in realistic cloud scenarios. For the **Core Security Concepts** path, you act as a cloud security engineer responding to threats, configuring access controls, and hardening AWS environments.

---

## 📚 What I Learned

### Identity & Access Management (IAM)
- Users, Groups, Roles, and Policies
- Principle of **Least Privilege** — only grant what's needed, nothing more
- IAM Policy structure: Effect, Action, Resource, Condition
- **MFA** (Multi-Factor Authentication) enforcement for sensitive accounts
- Cross-account role assumption

### Data Protection
| Protection Type | AWS Service/Feature |
|---|---|
| Encryption at rest | AWS KMS, S3 SSE, EBS encryption |
| Encryption in transit | TLS/SSL, ACM (Certificate Manager) |
| Key management | AWS KMS, CloudHSM |
| Secrets | AWS Secrets Manager, Parameter Store |

### Network Security
- **Security Groups** — stateful, instance-level firewall (allow rules only)
- **NACLs** (Network Access Control Lists) — stateless, subnet-level firewall (allow + deny)
- Private subnets: keeping databases and internal services off the internet
- VPC Flow Logs for traffic monitoring

### Threat Detection & Response
- **Amazon GuardDuty** — intelligent threat detection using ML
- **AWS Shield** — DDoS protection (Standard: free, Advanced: paid)
- **AWS WAF** — web application firewall for HTTP/HTTPS filtering
- **AWS Inspector** — automated vulnerability scanning for EC2 and containers
- **Amazon Macie** — discovers and protects sensitive data in S3

### Compliance & Auditing
- **AWS CloudTrail** — logs every API call made in your account (who did what, when)
- **AWS Config** — tracks resource configuration changes over time
- **AWS Security Hub** — centralized security findings dashboard

---

## 🔐 The Shared Responsibility Model (Security Lens)

```
┌─────────────────────────────────────┐
│         CUSTOMER RESPONSIBILITY      │
│  • IAM users, roles, policies       │
│  • OS patching (on EC2)             │
│  • Application-level security       │
│  • Data encryption choices          │
│  • Network/firewall configuration   │
├─────────────────────────────────────┤
│           AWS RESPONSIBILITY         │
│  • Physical data center security    │
│  • Hardware & hypervisor            │
│  • Managed service infrastructure   │
│  • Global network protection        │
└─────────────────────────────────────┘
```

---

## 💡 Key Takeaways

1. **Deny by default** — IAM denies everything unless explicitly allowed.
2. **Defense in depth** — Layer security: NACLs + Security Groups + WAF + GuardDuty together.
3. **Never hardcode credentials** — Use IAM Roles for EC2/Lambda, Secrets Manager for apps.
4. **Enable CloudTrail on day one** — You can't investigate incidents without logs.
5. **Rotate everything** — Access keys, passwords, certificates. Automate it.

---

## 🏅 Badge

> 📄 *Badge/certificate file in this folder*
