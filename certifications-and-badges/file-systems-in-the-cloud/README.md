# 🗂️ AWS SimuLearn: File Systems in the Cloud

> **Badge earned:** April 7, 2026 | **Issuer:** Amazon Web Services

---

## What is AWS SimuLearn?

**AWS SimuLearn** places you in realistic cloud scenarios where you make real architectural decisions. The **File Systems in the Cloud** path challenges you to design, configure, and manage scalable file storage solutions on AWS — understanding when to use which storage type and why.

---

## 📚 What I Learned

### Storage Types in AWS

```
Block Storage          Object Storage         File Storage
──────────────         ──────────────         ────────────
Amazon EBS             Amazon S3              Amazon EFS
(EC2 volumes)          (buckets/objects)      (shared NFS)
                                              Amazon FSx
Like a hard drive      Like a filing          Like a shared
attached to your PC    cabinet in the cloud   network drive
```

### Amazon EBS (Elastic Block Store)
- Persistent **block storage** for EC2 instances
- Lives in a single AZ — attach to one EC2 at a time
- **Volume types:**

| Type | Use Case | Characteristic |
|---|---|---|
| gp3 / gp2 | General purpose | Balanced price/performance |
| io2 / io1 | High IOPS workloads | Databases, transactional apps |
| st1 | Throughput optimized | Big data, log processing |
| sc1 | Cold storage | Infrequently accessed data |

- **Snapshots** — point-in-time backups stored in S3, can be copied cross-region

### Amazon EFS (Elastic File System)
- Fully managed **NFS file system** — scales automatically
- **Multi-AZ** — multiple EC2 instances can mount it simultaneously
- Grows and shrinks automatically as you add/remove files
- **Storage classes:**
  - *Standard* — frequently accessed files
  - *Infrequent Access (IA)* — lower cost for files not accessed daily
  - *Archive* — rarely accessed, lowest cost

### Amazon FSx
Purpose-built file systems for specific workloads:

| FSx Type | Built On | Best For |
|---|---|---|
| **FSx for Windows** | Windows Server | Windows apps, Active Directory |
| **FSx for Lustre** | Lustre | HPC, ML training, media processing |
| **FSx for NetApp ONTAP** | NetApp | Enterprise hybrid workloads |
| **FSx for OpenZFS** | OpenZFS | Data management, migration from on-prem |

### Amazon S3 (Object Storage)
- Store any amount of data as **objects** in **buckets**
- Globally unique bucket names
- **Storage classes:**

| Class | Use Case | Retrieval |
|---|---|---|
| S3 Standard | Frequent access | Instant |
| S3 Standard-IA | Infrequent access | Instant |
| S3 One Zone-IA | Non-critical, infrequent | Instant |
| S3 Glacier Instant | Archives, fast retrieval | Instant |
| S3 Glacier Flexible | Archives | Minutes–hours |
| S3 Glacier Deep Archive | Long-term archive | Up to 12 hours |
| S3 Intelligent-Tiering | Unknown access patterns | Auto |

### S3 Key Features
- **Versioning** — keep every version of every object
- **Lifecycle policies** — automatically move objects between storage classes
- **Replication** — cross-region (CRR) and same-region (SRR)
- **Event notifications** — trigger Lambda, SQS, SNS on object changes
- **Static website hosting** — serve HTML/CSS/JS directly from a bucket

### Choosing the Right Storage

```
Need to attach storage to a single EC2?     → EBS
Need shared storage across many EC2s?       → EFS
Need Windows file shares / Active Dir?      → FSx for Windows
Need HPC / ML training data?                → FSx for Lustre
Need to store files, backups, media, data?  → S3
Need to archive data cheaply long-term?     → S3 Glacier
```

---

## 🏗️ Architecture Pattern: Web App with Layered Storage

```
         Users
           │
    ┌──────▼──────┐
    │     ALB      │
    └──────┬──────┘
           │
    ┌──────▼──────┐        ┌─────────────┐
    │  EC2 Fleet   │◄──────►   EFS Mount  │  ← Shared app files
    └──────┬──────┘        └─────────────┘
           │
    ┌──────▼──────┐        ┌─────────────┐
    │  EBS Volume  │        │  S3 Bucket  │  ← Media, backups, logs
    │  (OS + App)  │        └─────────────┘
    └─────────────┘
```

---

## 💡 Key Takeaways

1. **EBS is for one EC2, EFS is for many** — don't try to share an EBS volume across instances.
2. **S3 is not a file system** — it's object storage. No folder hierarchy, no file locking.
3. **S3 Intelligent-Tiering saves money automatically** — use it when access patterns are unpredictable.
4. **EFS scales to petabytes with zero management** — ideal for containerized and serverless workloads.
5. **Lifecycle policies are free money** — automatically move cold data to cheaper storage classes.

---

## 🏅 Badge

> 📄 *Badge/certificate file in this folder*
