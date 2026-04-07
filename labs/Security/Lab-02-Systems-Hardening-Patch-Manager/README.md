# 🔒 Lab 12 — Systems Hardening with Patch Manager

> **Domain:** Security | **Services:** AWS Systems Manager, Patch Manager, Fleet Manager | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Use **AWS Systems Manager Patch Manager** to automate OS patching across EC2 instances. Configure patch baselines, run patch scans, and verify compliance through the Systems Manager dashboard.

---

## 📚 What I Did

### Steps Completed

| Step | Action | Screenshot |
|---|---|---|
| 1 | Explored the Systems Manager dashboard | `dashboard.png` |
| 2 | Reviewed Fleet Manager for instance inventory | `fleet manager.png` |
| 3 | Explored existing patch baselines | `patch baselines.png` |
| 4 | Created a custom patch baseline for Linux | `patch config linux.png` |
| 5 | Created a custom patch baseline for Windows | `patch config windows.png` |
| 6 | Configured batch patching settings | `batch baseline.png` |

---

## 🧠 Key Concepts Covered

### AWS Systems Manager (SSM)
A management service that gives you operational insights and control over your AWS and on-premises infrastructure — without SSH.

**Key SSM capabilities:**
| Feature | What it does |
|---|---|
| **Fleet Manager** | View and manage all your EC2 instances in one place |
| **Patch Manager** | Automate OS patching on EC2 instances |
| **Session Manager** | SSH-less terminal access to instances |
| **Parameter Store** | Store configuration values and secrets |
| **Run Command** | Execute scripts remotely without SSH |
| **Inventory** | Collect software and configuration data |

### SSM Agent
A lightweight agent installed on EC2 instances that lets SSM communicate with them. Pre-installed on most AWS AMIs. Requires an IAM role with `AmazonSSMManagedInstanceCore` policy.

### Patch Baselines
Define which patches are **required**, **approved**, or **rejected** for your instances.

**AWS Default Baselines (pre-configured):**
- `AWS-AmazonLinux2DefaultPatchBaseline`
- `AWS-WindowsDefaultPatchBaseline`
- `AWS-UbuntuDefaultPatchBaseline`

**Custom Baseline example:**
```
Patch Baseline: "Production-Linux-Baseline"
├── Operating System: Amazon Linux 2
├── Classification: Security | CriticalUpdates | BugFix
├── Severity: Critical | High
├── Auto-approval delay: 7 days after release
└── Rejected patches: [specific patches to never install]
```

### Patch Compliance States
```
Compliant       → All required patches installed
Non-Compliant   → Missing required patches
Not Applicable  → Patch doesn't apply to this OS
```

### Patching Workflow
```
1. SSM Agent installed on EC2
        │
        ▼
2. Patch Manager scans instance
        │
        ▼
3. Compares installed patches vs baseline
        │
        ▼
4. Reports compliance status
        │
        ▼
5. (Optional) Auto-remediate: install missing patches
        │
        ▼
6. Dashboard shows updated compliance
```

### Why Patch Manager Over Manual Patching?

| Manual SSH Patching | Patch Manager |
|---|---|
| Log in to each server individually | Patch hundreds of servers at once |
| Error-prone, easy to miss servers | Consistent, auditable, automated |
| No compliance tracking | Full compliance dashboard |
| Requires SSH access | Works without open ports |
| No rollback tracking | Full patch history logged |

---

## 💡 Key Takeaways

1. **Unpatched systems are the #1 attack vector** — Patch Manager eliminates the excuse of "we forgot."
2. **No SSH needed with SSM** — Session Manager + Patch Manager means you can close port 22 entirely.
3. **Custom baselines give you control** — approve patches after a delay period to avoid patching regressions.
4. **Fleet Manager is your inventory** — know exactly what's running on every instance without logging in.
5. **Automate patching with maintenance windows** — schedule patches during low-traffic hours automatically.

---

## 📸 Screenshots

> Screenshots available in [`./screenshots/`](./screenshots/)
