# Lab Notes: Monitor an EC2 Instance

**Date Completed:** <!-- Add your date -->
**Duration:** ~60 minutes
**Services:** Amazon CloudWatch, Amazon SNS, Amazon EC2

---

## Task 1 - Configure Amazon SNS

Created an SNS topic called MyCwAlarm with Standard type. Created a subscription using Email protocol and confirmed it via the confirmation email received.

📸 `screenshots/01-sns-topic-created.png`
📸 `screenshots/02-subscription-confirmed.png`

---

## Task 2 - Create a CloudWatch Alarm

Navigated to CloudWatch > Metrics > EC2 > Per-Instance Metrics and selected CPUUtilization for the Stress Test instance.

Configured the alarm with the following settings:
- Metric name: CPUUtilization
- Statistic: Average
- Period: 1 minute
- Threshold type: Static
- Condition: Greater than 60 percent
- Action: Send notification to MyCwAlarm SNS topic
- Alarm name: LabCPUUtilizationAlarm

📸 `screenshots/03-cloudwatch-metrics.png`
📸 `screenshots/04-alarm-config.png`
📸 `screenshots/05-alarm-created.png`

---

## Task 3 - Stress Test the EC2 Instance

Connected to the Stress Test EC2 instance via the EC2InstanceURL and ran the following command to spike CPU to 100 percent for 400 seconds:

sudo stress --cpu 10 -v --timeout 400s

Opened a second terminal and ran top to monitor live CPU usage. Monitored the CloudWatch alarm until it changed to In alarm state.

Received an email notification from AWS Notifications confirming the alarm triggered.

📸 `screenshots/06-stress-test-running.png`
📸 `screenshots/07-alarm-triggered.png`
📸 `screenshots/08-sns-email-received.png`

---

## Task 4 - Create a CloudWatch Dashboard

Created a dashboard called LabEC2Dashboard with a Line widget showing CPUUtilization for the Stress Test instance. This provides a quick access view of the metric at any time.

📸 `screenshots/09-cloudwatch-dashboard.png`

---

## Key Lessons Learned

**CloudWatch Alarms**
- Alarms watch a single metric and trigger actions when a threshold is crossed
- The In alarm state means the threshold has been breached
- A 1 minute period gives near real-time alerting

**Amazon SNS**
- SNS topics act as a hub that can fan out notifications to multiple subscribers
- Email subscriptions must be confirmed before they can receive notifications
- SNS integrates directly with CloudWatch alarms for automated alerting

**CPU Stress Testing**
- The stress command simulates high CPU load for testing monitoring setups
- CPU spiking can indicate malware or a malicious actor on the instance
- CloudWatch gives visibility into these events so they can be acted on quickly

**CloudWatch Dashboards**
- Dashboards give a single pane of glass view of your resources
- Widgets can be customized to show any metric across any resource
- Useful for ongoing monitoring without having to navigate through menus
