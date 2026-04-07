# ☁️ Lab 01 — EC2 Instance Setup

> **Domain:** Compute | **Service:** Amazon EC2 | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Launch, configure, monitor, resize, and terminate an Amazon EC2 instance using the AWS Management Console. This lab covers the full EC2 lifecycle from provisioning to cleanup.

---

## 📚 What I Did

### Steps Completed

| Step | Action |
|---|---|
| 01 | Navigated to AWS Management Console |
| 02 | Launched a new EC2 instance |
| 03 | Named the instance and applied tags |
| 04 | Selected an AMI (Amazon Machine Image) |
| 06 | Created and downloaded a key pair |
| 07 | Configured network settings |
| 08 | Set up a Security Group |
| 09 | Configured storage (EBS volume) |
| 10 | Reviewed advanced details |
| 11 | Launched the instance |
| 12 | Verified instance is running |
| 13 | Reviewed instance details |
| 14 | Checked monitoring metrics |
| 15 | Retrieved public IPv4 address |
| 16 | Reviewed Security Group inbound rules |
| 17 | Added an HTTP inbound rule (port 80) |
| 18 | Stopped the instance |
| 19 | Changed the instance type |
| 20 | Modified the EBS volume |
| 21 | Started the resized instance |
| 22 | Tested termination protection (error triggered correctly) |
| 23 | Disabled termination protection |
| 24 | Terminated the instance |

---

## 🧠 Key Concepts Covered

### AMI (Amazon Machine Image)
A pre-configured template containing the OS and software needed to launch an instance. Think of it as a snapshot you clone into a running server.

### Instance Types
Define the compute power of your EC2 instance:
- **t2.micro / t3.micro** — free tier eligible, good for testing
- **t3.medium** — more RAM and CPU for moderate workloads
- Always stop the instance before changing the type

### Security Groups
Virtual firewalls that control inbound and outbound traffic:
- **Inbound rules** — what traffic can reach your instance
- Added HTTP (port 80) to allow web traffic
- SSH (port 22) for remote access via key pair

### Key Pairs
- Used to securely SSH into your EC2 instance
- Download the `.pem` file once — it cannot be retrieved again
- Keep it safe: losing it means losing SSH access

### EBS Volumes
- Persistent block storage attached to EC2
- Survives instance stops (unlike instance store)
- Can be resized while instance is stopped

### Termination Protection
- Prevents accidental deletion of instances
- Must be explicitly disabled before terminating
- Best practice: enable on production instances

---

## 💡 Key Takeaways

1. **Always tag your resources** — naming instances saves confusion when you have many running.
2. **Security Groups are stateful** — if you allow inbound, the response traffic is automatically allowed out.
3. **Stop before resizing** — changing instance type or modifying volumes requires the instance to be stopped first.
4. **Key pairs are one-time downloads** — treat them like passwords and store them securely.
5. **Termination protection is your safety net** — enable it on anything you can't afford to lose.

---

## 📸 Screenshots

> Screenshots available in [`./screenshots/`](./screenshots/)
