# 🔒 Lab 11 — AWS SimuLearn: IAM Groups and Users

> **Domain:** Security | **Service:** AWS IAM | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Create and configure **IAM users and groups** in AWS, attach permission policies, and validate that access controls work as expected. Covers the core of AWS identity management.

---

## 📚 What I Did

### Steps Completed (18 steps)

| Steps | Action |
|---|---|
| 01–03 | Set up the IAM environment and navigated the console |
| 04–06 | Created IAM groups with specific permission levels |
| 07–09 | Attached managed policies to groups |
| 10–12 | Created IAM users and assigned them to groups |
| 13–15 | Tested user access by logging in with IAM credentials |
| 16–17 | Validated access (DIY challenge) |
| 18 | Final validation screenshot |

---

## 🧠 Key Concepts Covered

### IAM Core Components

```
AWS Account (Root)
└── IAM Users        ← Individual people or services
└── IAM Groups       ← Collections of users
└── IAM Roles        ← Temporary permissions for services/cross-account
└── IAM Policies     ← JSON documents defining permissions
```

### IAM Policy Structure
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

| Field | Purpose |
|---|---|
| `Effect` | `Allow` or `Deny` |
| `Action` | What API calls are permitted (e.g., `s3:GetObject`) |
| `Resource` | Which specific resource the policy applies to |
| `Condition` | Optional — add conditions like MFA required, IP range |

### AWS Managed Policies Used
| Policy | What it allows |
|---|---|
| `AdministratorAccess` | Full access to everything |
| `PowerUserAccess` | Full access except IAM management |
| `ReadOnlyAccess` | View all resources, change nothing |
| `AmazonS3FullAccess` | Full S3 control |
| `AmazonEC2ReadOnlyAccess` | View EC2 resources only |

### Groups vs Users vs Roles
- **Users** — long-term credentials for humans or applications
- **Groups** — assign policies to a group, all members inherit them (never assign policies directly to users)
- **Roles** — temporary credentials, used by EC2 instances, Lambda, cross-account access

### Principle of Least Privilege
> Grant only the permissions required to perform a task — nothing more.

```
❌ Bad:  Give developer AdministratorAccess because it's easier
✅ Good: Give developer access only to the specific S3 bucket and EC2 they need
```

### Testing Access
Logged in as the newly created IAM user and:
- Verified allowed actions worked
- Verified restricted actions were denied
- Confirmed the IAM boundary was correctly enforced

---

## 💡 Key Takeaways

1. **Never use the root account for daily work** — create an IAM admin user immediately after account creation.
2. **Always assign policies to groups, not users** — scaling a team is much easier.
3. **Least privilege is non-negotiable** — overly permissive policies are the root cause of most cloud breaches.
4. **Enable MFA for all human users** — especially anyone with elevated permissions.
5. **Rotate access keys regularly** — or better yet, use IAM Roles instead of long-term access keys.

---

## 📸 Screenshots

> Screenshots available in [`./lab_instructions.md/screenshots/`](./lab_instructions.md/screenshots/)
