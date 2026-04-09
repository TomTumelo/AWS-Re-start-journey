# 📓 Lab Notes — CloudFormation Troubleshooting

---

## Task 1 — JMESPath Practice

JMESPath is a query language for JSON. Used throughout the AWS CLI with the `--query` parameter.

### Key expressions practiced

```
desserts[].name                                                    → all names in array
desserts[0].name                                                   → first item name
desserts[?name=='Carrot cake']                                     → filter by value
StackResources[?ResourceType=='AWS::EC2::Instance'].LogicalResourceId  → filter by type
```

### Why it matters
Every `--query` in AWS CLI commands uses JMESPath. Mastering it means cleaner, more readable CLI output and faster troubleshooting.

---

## Task 2 — CloudFormation Stack Troubleshooting

### What is a WaitCondition?
A CloudFormation resource that pauses stack creation until it receives a signal. Used to confirm UserData scripts completed successfully before marking the EC2 resource as `CREATE_COMPLETE`.

### What is UserData?
A bash script that runs automatically when an EC2 instance first launches. Used to install software, configure services, and bootstrap the instance.

### The `#!/bin/bash -e` flag
The `-e` flag causes the script to exit immediately if any command returns a non-zero status. This is what caused the WaitCondition to never receive its signal — the script failed and stopped before reaching the signal command.

### Key commands used

```bash
# Create stack
aws cloudformation create-stack \
  --stack-name myStack \
  --template-body file://template1.yaml \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameters ParameterKey=KeyName,ParameterValue=vockey

# Monitor resources
aws cloudformation describe-stack-resources \
  --stack-name myStack \
  --query 'StackResources[*].[ResourceType,ResourceStatus]' \
  --output table

# Find failures
aws cloudformation describe-stack-events \
  --stack-name myStack \
  --query "StackEvents[?ResourceStatus == 'CREATE_FAILED']"

# Prevent rollback (keep EC2 alive for log inspection)
aws cloudformation create-stack \
  --stack-name myStack \
  --template-body file://template1.yaml \
  --capabilities CAPABILITY_NAMED_IAM \
  --on-failure DO_NOTHING \
  --parameters ParameterKey=KeyName,ParameterValue=vockey

# Read cloud-init logs
tail -50 /var/log/cloud-init-output.log

# Delete failed stack
aws cloudformation delete-stack --stack-name myStack
```

### Root cause
```
No package http available.
```
`http` is not a valid package name. The correct Apache web server package is `httpd`.

### Fix
```yaml
# Before
yum install -y http

# After
yum install -y httpd
```

---

## Task 3 — Drift Detection

### What is drift?
Drift occurs when the actual state of a CloudFormation-managed resource differs from what is defined in the template. This happens when someone manually modifies a resource in the Console or CLI outside of CloudFormation.

### What I did
Manually changed the `WebServerSG` security group's SSH inbound rule from `0.0.0.0/0` to `My IP` via the AWS Console.

### Drift detection commands

```bash
# Start detection
aws cloudformation detect-stack-drift --stack-name myStack

# Check detection status (replace <id> with StackDriftDetectionId)
aws cloudformation describe-stack-drift-detection-status \
  --stack-drift-detection-id <id>

# View drifted resources
aws cloudformation describe-stack-resources \
  --stack-name myStack \
  --query 'StackResources[*].[ResourceType,ResourceStatus,DriftInformation.StackResourceDriftStatus]' \
  --output table
```

### Result
Security group showed `MODIFIED` — drift confirmed.

Note: Adding a file to S3 does NOT register as drift. Only changes to resource *properties* (like bucket configuration) are considered drift.

---

## Task 4 — Stack Deletion Challenge

### Why delete failed
CloudFormation will not delete an S3 bucket that contains objects. This is a safety mechanism to prevent accidental data loss.

```
StackStatusReason: The following resource(s) failed to delete: [MyBucket]
```

### Finding the logical resource ID

```bash
aws cloudformation describe-stack-resources \
  --stack-name myStack \
  --query "StackResources[?ResourceType=='AWS::S3::Bucket'].LogicalResourceId"
```

Returns: `MyBucket`

### Challenge solution

```bash
aws cloudformation delete-stack \
  --stack-name myStack \
  --retain-resources MyBucket
```

The `--retain-resources` flag tells CloudFormation to skip deletion of specified resources. Stack reaches `DELETE_COMPLETE` while the bucket and its contents are preserved.

---

## Personal Reflections

- The `--on-failure DO_NOTHING` flag is one of the most useful debugging tools in CloudFormation — without it, the evidence disappears before you can investigate.
- Drift detection is critical in production environments where multiple people have console access.
- `--retain-resources` elegantly solves the real-world problem of needing to tear down infrastructure without destroying data.
- JMESPath expressions inside `--query` are everywhere in the AWS CLI — being comfortable with them makes every operation faster.
