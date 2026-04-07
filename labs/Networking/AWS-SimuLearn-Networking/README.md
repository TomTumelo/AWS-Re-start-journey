# 🌐 Lab 07 — AWS SimuLearn: Networking Concepts

> **Domain:** Networking | **Services:** VPC, Subnets, Route Tables, Internet Gateway | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Build and configure a complete AWS network from scratch using **Amazon VPC**. Set up public and private subnets, route tables, and an Internet Gateway to enable controlled internet access for cloud resources.

---

## 📚 What I Did

### Steps Completed

| Step | Action | Screenshot |
|---|---|---|
| 01 | Created a VPC with a CIDR block | `step 1.png` |
| 02 | Created subnets within the VPC | `step 2.png` |
| 03 | Configured an Internet Gateway | `Step 3.png` |
| 05 | Set up route tables | `Step 5.png` |
| 06 | Associated route table with public subnet | `Step 6.png` |
| 07 | Verified connectivity and routing | `Step 7.png` |

---

## 🧠 Key Concepts Covered

### VPC (Virtual Private Cloud)
Your own isolated network in AWS. You define the IP address range, subnets, routing, and access controls.

```
VPC: 10.0.0.0/16  (65,536 IP addresses)
├── Public Subnet:  10.0.1.0/24  (256 IPs) — AZ-a
├── Public Subnet:  10.0.2.0/24  (256 IPs) — AZ-b
├── Private Subnet: 10.0.3.0/24  (256 IPs) — AZ-a
└── Private Subnet: 10.0.4.0/24  (256 IPs) — AZ-b
```

### Internet Gateway (IGW)
Connects your VPC to the public internet. Attach one IGW per VPC.

```
Internet ──► Internet Gateway ──► Public Subnet ──► EC2
```

### Route Tables
Control where network traffic is directed:

**Public Route Table:**
```
Destination     Target
10.0.0.0/16     local        ← VPC internal traffic
0.0.0.0/0       igw-xxxxx    ← Everything else → Internet
```

**Private Route Table:**
```
Destination     Target
10.0.0.0/16     local        ← VPC internal only
(no internet route)
```

### Public vs Private Subnets
- **Public**: Has a route to the IGW + resources have public IPs
- **Private**: No route to IGW — can only be reached from within the VPC (or via NAT)

### CIDR Notation
```
10.0.0.0/16  → 65,536 addresses (VPC level)
10.0.1.0/24  → 256 addresses    (subnet level)
10.0.1.0/28  → 16 addresses     (very small subnet)
```
Note: AWS reserves 5 IPs per subnet (first 4 + last 1).

---

## 🏗️ Architecture Built

```
                    Internet
                        │
               Internet Gateway
                        │
        ┌───────────────┼───────────────┐
        │               │               │
  Public Subnet    Public Subnet        │
  (AZ-a)          (AZ-b)               │
  10.0.1.0/24     10.0.2.0/24          │
        │               │               │
        └───────────────┼───────────────┘
                        │
        ┌───────────────┼───────────────┐
        │               │               │
 Private Subnet   Private Subnet        │
  (AZ-a)          (AZ-b)               │
  10.0.3.0/24    10.0.4.0/24           │
        └───────────────────────────────┘
```

---

## 💡 Key Takeaways

1. **VPC = your private data center in AWS** — define your network before deploying anything.
2. **Route tables control traffic flow** — a subnet is only "public" if its route table has a 0.0.0.0/0 → IGW route.
3. **One IGW per VPC** — you can't attach multiple internet gateways.
4. **Always use multiple AZs** — one subnet per AZ minimum for high availability.
5. **Private subnets need NAT for outbound internet** — they can initiate connections out but can't receive inbound traffic.

---

## 📸 Screenshots

> Screenshots available in [`./screenshots/`](./screenshots/)
