# Lab Notes: EC2 Instance Setup

**Date Completed:** <!-- Add your date -->
**Duration:** <!-- Add duration -->
**Environment:** AWS Management Console

---

## Task 1 - Launch EC2 Instance

### Step 01 - Access EC2 Dashboard
Accessed the AWS Management Console and navigated to EC2.
📸 `screenshots/Step 01 Console.png`

### Step 02 - Launch Instance
Clicked Launch Instance to begin configuration.
📸 `screenshots/Step 02 Launch Instance.png`

### Step 03 - Name and Tags
Set the instance name to Web Server.
📸 `screenshots/Step 03 Name and Tags.png`

### Step 04 - Choose AMI
Selected Amazon Linux Free Tier Kernel 6.1.
📸 `screenshots/Step 04 Select AMI.png`

### Step 05 - Instance Type
Selected t3.micro - free tier eligible and sufficient for basic web hosting.

### Step 06 - Key Pair
Proceeded without a key pair as this is a lab environment.
📸 `screenshots/Step 06 Key Pair.png`

### Step 07 - Network Settings
Configured VPC as Lab VPC, created Web Server security group, and removed default inbound rules.
📸 `screenshots/Step 07 Network Settings.png`

### Step 08 - Storage Configuration
Kept the default 8 GiB Amazon EBS root volume. EBS is network-attached storage that persists independently of the instance.
📸 `screenshots/Step 08 Security Group Setup.png`

### Step 09 - Advanced Details - User Data Script
Enabled termination protection and added a User Data script to install Apache, start the service, enable it on boot, and create a test webpage.
📸 `screenshots/Step 09 Storage Configuration.png`

### Step 10 - Launch Instance
Clicked Launch Instance and verified instance state = Running.
📸 `screenshots/Step 10 Advanced Details.png`
📸 `screenshots/Step 11 Launch Instance.png`
📸 `screenshots/Step 12 View Instance Running.png`

---

## Task 2 - Monitor Instance

Checked monitoring metrics including CPU utilization and instance health checks.
📸 `screenshots/Step 13 Instance Details.png`
📸 `screenshots/Step 14 Monitoring Metrics..png`

---

## Task 3 - Update Security Group

**Problem:** Could not access the web server using the Public IPv4 address - HTTP traffic was blocked.

**Fix:** Edited inbound rules on the security group:
- Type: HTTP
- Port: 80
- Source: Anywhere IPv4

After saving, the web server became accessible.
📸 `screenshots/Step 15 Public IPv4 Address.png`
📸 `screenshots/Step 16 Security Group Inbound Rules.png`
📸 `screenshots/Step 17 Add HTTP Rule.png`

---

## Task 4 - Resize Instance

Stopped the instance before making changes, then changed instance type from t3.micro to t3.small, increased EBS volume size, and restarted.
📸 `screenshots/Step 18 Stop Instance..png`
📸 `screenshots/Step 19 Change Instance Type.png`
📸 `screenshots/Step 20 Modify EBS Volume.png`
📸 `screenshots/Step 21 Start Resized Instance.png`

---

## Task 5 - Termination Protection

Attempted to terminate the instance - failed due to termination protection. Disabled it then successfully terminated.
📸 `screenshots/Step 22 Termination Protection Error.png`
📸 `screenshots/Step 23 Disable Termination Protection.png`
📸 `screenshots/Step 24 Instance Terminated.png`

---

## Key Lessons Learned

**EC2 Instance Lifecycle**
- Instances go through pending, running, stopping, stopped, and terminated states
- You must stop an instance before changing its type

**Security Groups**
- Act as a stateful firewall at the instance level
- No inbound HTTP rule means the web server is unreachable even if Apache is running

**User Data**
- Scripts run automatically on first boot
- Powerful way to automate server configuration without manual SSH

**EBS Volumes**
- Network-attached storage that can be resized independently
- Persists even if the instance is stopped

**Termination Protection**
- Prevents accidental deletion of critical instances
- Must be explicitly disabled before termination is allowed
