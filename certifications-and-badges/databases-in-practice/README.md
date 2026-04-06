# 🗄️ Databases in Practice

> **Certificate earned:** April 7, 2026 | **Issuer:** AWS / re/Start Program

---

## Overview

This module bridges database theory with real-world AWS implementation. It goes beyond SQL syntax to cover *how* databases are architected, scaled, backed up, and chosen for the right workloads in cloud environments.

---

## 📚 What I Learned

### Relational vs Non-Relational Databases

| Feature | Relational (SQL) | Non-Relational (NoSQL) |
|---|---|---|
| Structure | Tables, rows, columns | Documents, key-value, graphs |
| Schema | Fixed (defined upfront) | Flexible (dynamic) |
| Scaling | Vertical (scale up) | Horizontal (scale out) |
| Best for | Complex queries, ACID transactions | High velocity, unstructured data |
| AWS service | RDS, Aurora | DynamoDB |

### SQL Fundamentals
```sql
-- Core operations practiced:
SELECT, INSERT, UPDATE, DELETE       -- DML (Data Manipulation)
CREATE TABLE, ALTER TABLE, DROP      -- DDL (Data Definition)
JOIN (INNER, LEFT, RIGHT, FULL)      -- Combining tables
GROUP BY, HAVING, ORDER BY           -- Aggregation & sorting
Subqueries, indexes, constraints     -- Optimization & integrity
```

### Amazon RDS (Relational Database Service)
- **Supported engines**: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora
- **Multi-AZ deployments** — automatic failover to standby replica in another AZ
- **Read Replicas** — offload read traffic, can be cross-region
- **Automated backups** — point-in-time recovery up to 35 days
- **Maintenance windows** — patches applied automatically during low-traffic periods

### Amazon Aurora
- AWS's **cloud-native** relational database
- **5x faster** than MySQL, **3x faster** than PostgreSQL (AWS claims)
- Storage auto-scales up to 128 TB
- **Aurora Serverless** — scales compute up/down automatically based on demand
- Compatible with MySQL and PostgreSQL

### Amazon DynamoDB
- Fully managed **NoSQL** key-value and document database
- **Single-digit millisecond** performance at any scale
- **DynamoDB Streams** — capture change events for triggers/replication
- **On-demand vs Provisioned** capacity modes
- **Global Tables** — multi-region, multi-active replication

### Database Best Practices Applied
- **Indexing**: Know which columns to index — over-indexing slows writes
- **Connection pooling**: Don't open a new DB connection per request
- **Least privilege**: DB users should only access the tables they need
- **Encryption**: Enable at-rest and in-transit encryption on every database
- **Monitoring**: Use CloudWatch metrics + Enhanced Monitoring for RDS

---

## 🏗️ Architecture Pattern: Highly Available Database Setup

```
                    Application Tier
                         │
              ┌──────────▼──────────┐
              │    Load Balancer     │
              └──────────┬──────────┘
                         │
         ┌───────────────┼───────────────┐
         │               │               │
    App Server      App Server      App Server
         │               │               │
         └───────────────┼───────────────┘
                         │
              ┌──────────▼──────────┐
              │   RDS Primary (AZ-a) │  ◄── Writes
              └──────────┬──────────┘
                         │ synchronous replication
              ┌──────────▼──────────┐
              │  RDS Standby (AZ-b)  │  ◄── Failover target
              └─────────────────────┘
```

---

## 💡 Key Takeaways

1. **Match database type to workload** — forcing a relational model on unstructured data is painful.
2. **Multi-AZ ≠ Read Replica** — Multi-AZ is for *high availability*, Read Replicas are for *read scaling*.
3. **Backups don't replace snapshots** — automated backups + manual snapshots = full safety net.
4. **DynamoDB partition keys matter enormously** — a bad key design causes hot partitions and poor performance.
5. **Don't store secrets in connection strings** — use Secrets Manager to rotate DB credentials automatically.

---

## 🏅 Certificate

> 📄 *Certificate file in this folder*
