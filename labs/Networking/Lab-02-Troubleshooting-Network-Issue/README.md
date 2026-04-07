# 🌐 Lab 08 — Troubleshooting a Network Issue

> **Domain:** Networking | **Services:** VPC, EC2, Security Groups, Route Tables | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Diagnose and fix a broken network configuration that prevents a web server from being accessible via a browser. Practice real-world troubleshooting skills by identifying missing routes, misconfigured Security Groups, and service issues.

---

## 📚 What I Did

### Problem
A web application hosted on EC2 was unreachable from a browser — the page wouldn't load and SSH access was broken.

### Troubleshooting Steps

| Step | Finding | Screenshot |
|---|---|---|
| Checked subnets | Identified routing issues | `subnets.png` |
| Reviewed route tables | Found missing internet route | `route tables.png` |
| Attempted SSH | Connection was timing out | `SSH.png` |
| Checked httpd status | Web server was not running | `systemctstatusb4.png` |
| Checked Security Group | Missing HTTP inbound rule | — |
| Added inbound rule | Added port 80 HTTP rule | `added inbound rule.png` |
| Started httpd service | Service started successfully | `httpd running.png` |
| Browser before fix | Page not loading | `browser before fix.png` |
| Browser after fix | Page loading correctly ✅ | `browser after fix.png` |

---

## 🧠 Key Concepts Covered

### The Troubleshooting Framework
When a web app is unreachable, work through these layers **in order**:

```
Layer 1: DNS          → Is the domain resolving to the right IP?
Layer 2: Routing      → Does the subnet have a route to the internet?
Layer 3: Security Group → Is port 80/443 open inbound?
Layer 4: NACL         → Is the Network ACL blocking traffic?
Layer 5: OS Firewall  → Is iptables/firewalld blocking traffic?
Layer 6: Service      → Is the web server (httpd/nginx) actually running?
Layer 7: App          → Is the application itself healthy?
```

### Common Issues Found & Fixed

**Issue 1: Missing Route Table Entry**
```
Before:
Destination     Target
10.0.0.0/16     local
(no internet route!)

After:
Destination     Target
10.0.0.0/16     local
0.0.0.0/0       igw-xxxxx  ← Added this
```

**Issue 2: Missing Security Group Inbound Rule**
```
Before: Only SSH (22) was open
After:  Added HTTP (80) from 0.0.0.0/0
```

**Issue 3: Web Server Not Running**
```bash
# Check status
sudo systemctl status httpd

# Start the service
sudo systemctl start httpd

# Enable on boot
sudo systemctl enable httpd
```

### SSH Troubleshooting
```bash
# Test basic connectivity
ping ec2-public-ip

# Test SSH port specifically
telnet ec2-public-ip 22

# Connect with key pair
ssh -i keypair.pem ec2-user@ec2-public-ip

# Check Security Group: port 22 must be open inbound
```

---

## 💡 Key Takeaways

1. **Work from outside in** — start at the network layer and work toward the application.
2. **Security Groups are the most common culprit** — always check inbound rules first.
3. **Route tables are invisible until broken** — always verify the public subnet has an IGW route.
4. **`systemctl status` is your first diagnostic** — tells you immediately if a service is running.
5. **Document before and after** — screenshots of broken vs fixed state prove the issue and solution.

---

## 📸 Screenshots

> Screenshots available in [`./screenshots/`](./screenshots/)
