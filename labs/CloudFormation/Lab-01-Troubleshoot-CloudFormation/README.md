# 🛠️ Lab — Troubleshoot AWS CloudFormation

> **Domain:** Infrastructure as Code | **Services:** CloudFormation · EC2 · S3 · VPC · IAM | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Practice troubleshooting failed AWS CloudFormation deployments using the AWS CLI. Covers stack creation failures, EC2 log analysis, drift detection, and resolving stack deletion issues.

---

## 📋 Skills Demonstrated

- JMESPath querying of JSON documents
- AWS CloudFormation stack creation and troubleshooting
- EC2 `cloud-init` log analysis
- Infrastructure as Code (IaC) template editing
- Stack drift detection via AWS CLI
- Resolving `DELETE_FAILED` stacks while retaining S3 resources

---

## 🔍 Problem Statement

The CloudFormation stack failed during creation because the EC2 UserData script attempted to install a package with the wrong name:

```bash
yum install -y http     # ❌ incorrect — package does not exist
```

This caused the `WaitCondition` to time out after 60 seconds, triggering a full stack rollback.

---

## 🧪 Lab Tasks Overview

| Task | Description |
|---|---|
| Task 1 | JMESPath practice — query JSON documents |
| Task 2 | Create, fail, troubleshoot, and fix a CloudFormation stack |
| Task 3 | Manually modify a security group and detect configuration drift |
| Task 4 | Delete a stack while retaining an S3 bucket with objects |

---

## 🔎 Root Cause Investigation

### Step 1 — Identify the failure

```bash
aws cloudformation describe-stack-events \
  --stack-name myStack \
  --query "StackEvents[?ResourceStatus == 'CREATE_FAILED']"
```

**Finding:** `WaitCondition timed out. Received 0 conditions when expecting 1.`

### Step 2 — Preserve resources for investigation

Re-created the stack with `--on-failure DO_NOTHING` to prevent rollback and keep the EC2 instance alive for log inspection.

### Step 3 — SSH into Web Server and read cloud-init logs

```bash
tail -50 /var/log/cloud-init-output.log
```

**Finding:**
```
No package http available.
util.py[WARNING]: Failed running /var/lib/cloud/instance/scripts/part-001
```

The UserData script failed immediately. Because the script used `#!/bin/bash -e`, any failed command caused the entire script to exit — meaning the wait signal was never sent.

---

## 🔧 Fix Applied

Edited the CloudFormation template:

```bash
vim template1.yaml
```

Changed line 128 from:

```yaml
yum install -y http
```

to:

```yaml
yum install -y httpd
```

Confirmed fix:

```bash
cat template1.yaml | grep httpd
```

---

## ✅ Successful Deployment

After fixing the template, the stack deployed successfully:

```
StackStatus: CREATE_COMPLETE
```

Web server responded at the public IP with:

```
Hello from your web server!
```

---

## 📡 Drift Detection

Manually modified the `WebServerSG` security group in the AWS Console — changed SSH inbound rule from `0.0.0.0/0` to `My IP`.

### Detected drift via CLI:

```bash
aws cloudformation detect-stack-drift --stack-name myStack

aws cloudformation describe-stack-resources \
  --stack-name myStack \
  --query 'StackResources[*].[ResourceType,ResourceStatus,DriftInformation.StackResourceDriftStatus]' \
  --output table
```

**Result:** Security group showed status `MODIFIED` — confirming drift was detected.

---

## 🗑️ Stack Deletion Challenge

### Problem

Normal `delete-stack` failed because the S3 bucket contained objects:

```
StackStatusReason: The following resource(s) failed to delete: [MyBucket]
```

CloudFormation refuses to delete non-empty S3 buckets to prevent accidental data loss.

### Solution

Used the `--retain-resources` flag to keep the bucket while deleting everything else:

```bash
aws cloudformation delete-stack \
  --stack-name myStack \
  --retain-resources MyBucket
```

**Result:** Stack deleted successfully. S3 bucket and its contents preserved. ✅

---

## 💡 Key Takeaways

1. **`--on-failure DO_NOTHING` is essential for debugging** — without it, the failed EC2 gets deleted before you can read its logs.
2. **`cloud-init-output.log` is your first stop** — it captures every UserData command and its output.
3. **`#!/bin/bash -e` stops scripts on first error** — powerful for ensuring WaitConditions only signal on full success.
4. **Drift detection catches manual changes** — any resource modified outside CloudFormation shows as `MODIFIED`.
5. **`--retain-resources` is the clean solution** — keeps critical data while still achieving a `DELETE_COMPLETE` stack status.

---

## 📸 Screenshots

> Screenshots available in [`./screenshots/`](./screenshots/)

| Screenshot | Description |
|---|---|
| `one.png` / `two.png` | JMESPath query results |
| `identity-confirmation.png` | AWS CLI credentials verified |
| `region.png` | Region discovery |
| `terminal.png` | SSH into CLI Host |
| `Create-the-Stack.png` | Initial stack creation |
| `Watch-Stack-Progress.png` | Stack resources monitoring |
| `Check-Why-It-Failed.png` | CREATE_FAILED events |
| `Read-the-Error-Log.png` | cloud-init log showing root cause |
| `Confirm-the-Fix.png` | httpd confirmed in template |
| `Create-Again-Without-Rollback.png` | Retry with DO_NOTHING |
| `Create-the-Fixed-Stack.png` | Fixed stack creation |
| `Watch-Stack-Build.png` | All resources CREATE_COMPLETE |
| `Confirm-Stack-Success.png` | Stack status CREATE_COMPLETE |
| `browser-test.png` | Web server live in browser |
| `Change-the-Inbound-Rule.png` | Manual security group change |
| `Get-Bucket-Name.png` | S3 bucket name from stack outputs |
| `Upload-File-to-S3.png` | File uploaded to bucket |
| `Confirm-File-is-in-Bucket.png` | File confirmed in S3 |
| `Start-Drift-Detection.png` | Drift detection initiated |
| `Check-Drift-Status.png` | Drift status DRIFTED |
| `View-Drifted-Resources.png` | Security group MODIFIED |
| `Attempt-Normal-Delete.png` | DELETE_FAILED |
| `Confirm-Success.png` | Stack DELETE_COMPLETE |
