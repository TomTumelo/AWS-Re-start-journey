# 🗄️ Lab 03 — SimuLearn: Databases in Practice

> **Domain:** Databases | **Services:** Amazon RDS, EC2 | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Simulate a real-world database deployment scenario on AWS using **Amazon RDS**. Launch an EC2 instance, install a SQL database engine, and interact with it — covering the full setup from AMI selection to querying data.

---

## 📚 What I Did

### Steps Completed

| Step | Action |
|---|---|
| 01 | Launched an EC2 instance for the database environment |
| 02 | Navigated to AMI selection |
| 03 | Searched for and selected a SQL-compatible AMI |
| 04–12 | Configured instance settings, storage, and security group |
| 13 | Verified database setup milestone |
| 14–19 | Performed database operations and queries |
| 20 | Final validation of the completed lab |

---

## 🧠 Key Concepts Covered

### Amazon RDS vs Self-Managed DB on EC2

| Feature | RDS (Managed) | DB on EC2 (Self-managed) |
|---|---|---|
| OS patching | AWS handles it | You handle it |
| Backups | Automated | Manual setup |
| High availability | Multi-AZ built-in | DIY |
| Scaling | Push-button | Manual |
| Cost | Higher | Lower |
| Control | Less | Full |

### SQL Fundamentals Practiced
```sql
-- Creating tables
CREATE TABLE students (
  id INT PRIMARY KEY,
  name VARCHAR(100),
  score DECIMAL(5,2)
);

-- Inserting data
INSERT INTO students VALUES (1, 'Tumelo', 95.5);

-- Querying
SELECT * FROM students WHERE score > 80;

-- Updating
UPDATE students SET score = 98 WHERE id = 1;
```

### Security Group for Databases
- Never expose port 3306 (MySQL) or 5432 (PostgreSQL) to the internet
- Allow inbound only from your application's Security Group
- Use private subnets for database instances in production

---

## 💡 Key Takeaways

1. **RDS removes undifferentiated heavy lifting** — let AWS manage patching, backups, and failover.
2. **Database security starts at the network layer** — private subnets + tight Security Groups.
3. **Always use parameter groups** — they let you tune database settings without SSH access.
4. **Multi-AZ is not a backup** — it's for availability. Use snapshots for point-in-time recovery.
5. **Read replicas offload read traffic** — never hit your primary DB with reporting queries.

---

## 📸 Screenshots

> Screenshots available in [`./original-overview/screenshots/`](./original-overview/screenshots/)
