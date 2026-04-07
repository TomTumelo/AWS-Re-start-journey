# 📊 Lab 02 — Monitor an EC2 Instance with CloudWatch

> **Domain:** Compute | **Services:** Amazon EC2, CloudWatch, SNS | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Set up real-time monitoring for an EC2 instance using **Amazon CloudWatch**. Configure alarms that trigger **SNS email notifications** when CPU usage exceeds a threshold, and validate the alarm using a stress test.

---

## 📚 What I Did

### Steps Completed

| Step | Action |
|---|---|
| 01 | Created an SNS topic for alarm notifications |
| 02 | Confirmed the SNS email subscription |
| 03 | Verified subscription status in AWS Console |
| 04 | Received confirmation email |
| 05 | Explored CloudWatch metrics for the EC2 instance |
| 06 | Configured a CPU utilisation alarm |
| 07 | Verified alarm was created successfully |
| 08 | Ran a CPU stress test on the instance |
| 09 | Monitored stress test output with `top` |
| 10 | Alarm triggered as CPU spiked |
| 11 | Received SNS email notification |
| 12 | Built a CloudWatch dashboard |

---

## 🧠 Key Concepts Covered

### Amazon CloudWatch
AWS's monitoring and observability service. Collects metrics, logs, and events from AWS resources and applications.

**Key CloudWatch components:**
| Component | Purpose |
|---|---|
| **Metrics** | Time-series data points (CPU%, NetworkIn, DiskReadOps) |
| **Alarms** | Triggers actions when metrics cross thresholds |
| **Dashboards** | Visual panels to monitor multiple metrics at once |
| **Logs** | Stores and searches log data from applications and AWS services |

### Amazon SNS (Simple Notification Service)
A fully managed pub/sub messaging service. In this lab:
- Created a **topic** (a channel for notifications)
- Added an **email subscription** to that topic
- CloudWatch alarm published to the topic when triggered
- Email received instantly when alarm fired

### CloudWatch Alarm States
```
OK          → Metric is within the defined threshold
ALARM       → Metric has breached the threshold
INSUFFICIENT_DATA → Not enough data points yet to evaluate
```

### CPU Stress Test
Used the Linux `stress` tool to artificially spike CPU usage:
```bash
sudo yum install stress -y
stress --cpu 4 --timeout 300
```
Monitored in real time with `top` — watched CPU hit ~100%, triggering the CloudWatch alarm.

---

## 🏗️ Architecture

```
EC2 Instance
     │
     │ CPU Metrics (every 1 min)
     ▼
CloudWatch Metrics
     │
     │ Threshold breached (CPU > X%)
     ▼
CloudWatch Alarm
     │
     │ Publish notification
     ▼
SNS Topic
     │
     │ Email delivery
     ▼
📧 Email Notification Received
```

---

## 💡 Key Takeaways

1. **CloudWatch is your eyes on AWS** — without it, you're flying blind in production.
2. **SNS decouples notifications** — one alarm can notify email, SMS, Lambda, SQS all at once.
3. **Confirm your subscription** — SNS emails go to PENDING until you click the confirmation link.
4. **Dashboards give you a single pane of glass** — combine metrics from multiple services in one view.
5. **Stress testing validates your alarms** — always test that your alerts actually fire before going to production.

---

## 📸 Screenshots

> Screenshots available in [`./screenshots/`](./screenshots/)
