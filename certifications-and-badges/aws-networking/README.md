# 🌐 AWS SimuLearn: Networking Concepts

> **Badge earned:** April 7, 2026 | **Issuer:** Amazon Web Services

---

## What is AWS SimuLearn?

**AWS SimuLearn** puts you in real cloud architecture scenarios where decisions have consequences. The **Networking Concepts** path challenges you to design, build, and troubleshoot networks in AWS — from basic VPCs to multi-region connectivity.

---

## 📚 What I Learned

### VPC Fundamentals (Virtual Private Cloud)
Your own logically isolated section of the AWS cloud — think of it as your private data center in the cloud.

- **CIDR blocks** — defining your IP address space (e.g., `10.0.0.0/16`)
- **Subnets** — subdividing a VPC across Availability Zones
  - *Public subnets*: resources that need internet access (web servers, load balancers)
  - *Private subnets*: resources that shouldn't be publicly reachable (databases, app servers)
- **Route Tables** — rules that determine where network traffic goes
- **Internet Gateway (IGW)** — connects a VPC to the public internet
- **NAT Gateway** — lets private subnet resources reach the internet *without* being reachable from it

### A Standard 3-Tier Architecture

```
Internet
    │
    ▼
Internet Gateway
    │
    ▼
┌───────────────────────────────┐
│  PUBLIC SUBNET (Web Tier)     │
│  Load Balancer / Bastion Host │
└───────────────┬───────────────┘
                │
┌───────────────▼───────────────┐
│  PRIVATE SUBNET (App Tier)    │
│  EC2 Application Servers      │
└───────────────┬───────────────┘
                │
┌───────────────▼───────────────┐
│  PRIVATE SUBNET (DB Tier)     │
│  RDS / Aurora Database        │
└───────────────────────────────┘
```

### Load Balancing
| Load Balancer | Use Case |
|---|---|
| **ALB** (Application) | HTTP/HTTPS traffic, path-based routing, microservices |
| **NLB** (Network) | Ultra-high performance, TCP/UDP, static IPs |
| **GLB** (Gateway) | Third-party virtual appliances |

### Connectivity Options
- **VPC Peering** — direct private connection between two VPCs
- **AWS Transit Gateway** — hub-and-spoke model for connecting many VPCs
- **VPN (Site-to-Site)** — encrypted tunnel between on-premises network and AWS
- **AWS Direct Connect** — dedicated physical connection to AWS (faster, more consistent than VPN)

### DNS with Route 53
- **Record types**: A, AAAA, CNAME, MX, TXT, Alias
- **Routing policies**: Simple, Weighted, Latency-based, Failover, Geolocation, Geoproximity
- **Health checks** — Route 53 can reroute traffic if an endpoint goes down

### CloudFront (CDN)
- Caches content at **Edge Locations** globally
- Reduces latency for global users
- Integrates with S3, ALB, EC2, Lambda@Edge

---

## 💡 Key Takeaways

1. **Always use multiple AZs** — one subnet per AZ minimum. AZ failure is real.
2. **Public ≠ internet-facing** — "public subnet" just means it has a route to an IGW. Don't put databases there.
3. **NAT Gateway costs money** — it's per-hour + per-GB. Design your traffic flows thoughtfully.
4. **Security Groups + NACLs work together** — SGs are your first line, NACLs add a backup layer.
5. **Route 53 failover is powerful** — combined with health checks, it's automatic disaster recovery for DNS.

---

## 🏅 Badge

> 📄 *Badge/certificate file in this folder*
