# Lab Notes: Troubleshooting a Network Issue

**Date Completed:** <!-- Add your date -->
**Duration:** ~1 hour
**Role:** Cloud Support Engineer (simulated customer scenario)

---

## Scenario

A customer named Ana (contractor) raised a support ticket:

> "When I create an Apache server through the command line, I cannot ping it. I also get an error when I enter the IP address in the browser. Can you please help figure out what is blocking my connection?"

I was given an exact replica of her VPC to investigate and fix.

---

## Task 1 - SSH into the EC2 Instance

Connected to the Amazon Linux EC2 instance using a PEM key:

```bash
cd ~/Downloads
chmod 400 labsuser.pem
ssh -i labsuser.pem ec2-user@<public-ip>
```

---

## Task 2 - Install and Start Apache

Checked the status of httpd - it was installed but not running:

```bash
sudo systemctl status httpd.service
```

Started the service:

```bash
sudo systemctl start httpd.service
sudo systemctl status httpd.service
```

Tried loading http://<PUBLIC-IP> in a browser - page did not load. Apache was running so the problem was in the VPC configuration.

---

## Task 3 - Investigate the VPC Configuration

### Subnets
- Verified the EC2 instance was in the correct public subnet
- Confirmed auto-assign public IP was enabled

### Route Tables
- Checked for a 0.0.0.0/0 route pointing to the Internet Gateway

### Internet Gateway
- Confirmed an IGW existed and was attached to the VPC

### Security Group
- Checked inbound rules for HTTP (port 80)

### Network ACL
- Verified inbound and outbound rules were not blocking traffic

---

## Root Cause

<!-- Fill in what you found -->

---

## Fix Applied

<!-- Fill in what you changed -->

---

## Result

Loaded http://<PUBLIC-IP> in the browser - Apache test page displayed successfully.

---

## Key Lessons Learned

**Isolate the layer then fix it**
- Apache running does not mean Apache is reachable
- Work outward: instance, security group, route table, internet gateway, NACL

**HTTP vs HTTPS**
- Apache listens on port 80 by default
- Security group must explicitly allow port 80 inbound

**Security Groups are stateful**
- If inbound is allowed, response traffic is automatically allowed outbound

**NACLs are stateless**
- Both inbound and outbound rules must explicitly allow traffic
- Evaluated in rule-number order, first match wins
