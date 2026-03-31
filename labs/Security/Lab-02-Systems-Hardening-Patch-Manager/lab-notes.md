# Lab Notes: Systems Hardening with Patch Manager

**Date Completed:** <!-- Add your date -->
**Duration:** ~60 minutes
**Service:** AWS Systems Manager - Patch Manager

---

## Task 1 - Patch Linux Instances Using Default Baseline

Navigated to Systems Manager > Fleet Manager to view all 6 pre-configured instances (3 Linux, 3 Windows). Each instance had an IAM role attached allowing Systems Manager to manage them.

Configured Patch now with the following settings:
- Patching operation: Scan and install
- Reboot option: Reboot if needed
- Target: Specify instance tags
- Tag key: Patch Group
- Tag value: LinuxProd

Monitored the AWS-PatchNowAssociation panel until all 3 Linux instances completed successfully.

📸 `screenshots/01-fleet-manager-instances.png`
📸 `screenshots/02-linux-patch-config.png`
📸 `screenshots/03-linux-patch-complete.png`

---

## Task 2 - Create Custom Patch Baseline for Windows

Created a new patch baseline called WindowsServerSecurityUpdates with two approval rules:

Rule 1:
- Products: WindowsServer2019
- Severity: Critical
- Classification: SecurityUpdates
- Auto-approval: 3 days
- Compliance reporting: Critical

Rule 2:
- Products: WindowsServer2019
- Severity: Important
- Classification: SecurityUpdates
- Auto-approval: 3 days
- Compliance reporting: High

After creating the baseline, modified patch groups and associated it with WindowsProd.

📸 `screenshots/04-custom-baseline-created.png`

---

## Task 3 - Patch Windows Instances

Tagged all 3 Windows instances with:
- Key: Patch Group
- Value: WindowsProd

Ran Patch now targeting the WindowsProd tag. Monitored the execution via State Manager and Run Command output, confirming PatchGroup: WindowsProd was applied.

📸 `screenshots/05-windows-patch-complete.png`

---

## Task 4 - Verify Compliance

Navigated to Patch Manager > Dashboard. Compliance summary showed Compliant: 6 confirming all instances were successfully patched.

Checked the Compliance reporting tab and verified all 6 instances showed Compliant status with critical, security, and other noncompliant counts all at zero.

📸 `screenshots/06-compliance-dashboard.png`

---

## Key Lessons Learned

**Patch Baselines**
- AWS provides default baselines for each OS that cannot be customized
- Custom baselines give full control over which patches are approved or rejected
- Auto-approval delays (e.g. 3 days) give time to test patches before they are applied

**Patch Groups**
- Patch groups use EC2 instance tags to target specific sets of instances
- The tag key must be Patch Group for Systems Manager to recognize it
- Different groups can use different baselines

**Patch Manager vs Manual Patching**
- Patch Manager scales across hundreds or thousands of instances at once
- Compliance reporting gives a clear view of which instances are up to date
- Run Command handles the actual patching behind the scenes automatically
