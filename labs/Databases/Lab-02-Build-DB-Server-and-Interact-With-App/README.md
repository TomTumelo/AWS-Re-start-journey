# 🗄️ Lab 04 — Build a DB Server and Interact with a Web App

> **Domain:** Databases | **Services:** Amazon RDS, EC2, VPC | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Deploy a fully functional **Amazon RDS database server**, configure its security group, connect it to a running web application, and verify end-to-end connectivity through the app's interface.

---

## 📚 What I Did

### Steps Completed

| Step | Action | Screenshot |
|---|---|---|
| 1 | Created RDS database instance | `db-created.png` |
| 2 | Retrieved the RDS endpoint URL | `endpoint.png` |
| 3 | Configured inbound Security Group rules for the DB | `inbound-sg.png` |
| 4 | Connected the web application to the database | `web application.png` |
| 5 | Verified app-to-DB connectivity via load balancer | `database-lb.png` |

---

## 🧠 Key Concepts Covered

### RDS Deployment Flow

```
1. Create VPC with public + private subnets
        │
        ▼
2. Launch EC2 (web app) in public subnet
        │
        ▼
3. Launch RDS in private subnet
        │
        ▼
4. Configure Security Group:
   - Web SG: allow HTTP (80) from internet
   - DB SG: allow MySQL (3306) from Web SG only
        │
        ▼
5. Connect app to RDS using endpoint URL
        │
        ▼
6. Verify via browser / load balancer
```

### RDS Endpoint
The endpoint is the hostname your application uses to connect to the database:
```
mydb.abc123xyz.us-east-1.rds.amazonaws.com:3306
```
- Never hardcode this in your app — use environment variables or Secrets Manager
- The endpoint stays the same even after Multi-AZ failover

### Security Group Chaining
Instead of allowing a specific IP to reach the database, reference the **web server's Security Group**:
```
DB Security Group inbound rule:
  Type: MySQL/Aurora
  Port: 3306
  Source: [Web-Server-Security-Group-ID]  ← not an IP
```
This means only EC2 instances in the web SG can reach the DB — much more secure than IP-based rules.

### Load Balancer Integration
- Placed an **Application Load Balancer (ALB)** in front of the web tier
- ALB distributes traffic across multiple EC2 instances
- Web app connects to RDS endpoint behind the scenes

---

## 💡 Key Takeaways

1. **Databases belong in private subnets** — never expose RDS directly to the internet.
2. **Use Security Group references, not IPs** — more flexible and more secure.
3. **The RDS endpoint is your connection string** — store it in environment variables, never hardcode.
4. **Test connectivity before deploying the full app** — a simple `telnet endpoint 3306` saves hours of debugging.
5. **Load balancers add resilience** — your app keeps working even if one EC2 instance fails.

---

## 📸 Screenshots

> Screenshots available in [`./database-server-sg/`](./database-server-sg/)
