# Lab 02 - Monitor an EC2 Instance

## Overview

In this lab, I set up monitoring for an EC2 instance using Amazon CloudWatch and Amazon SNS. I simulated a CPU spike attack by running a stress test on the instance, which triggered a CloudWatch alarm and sent an email notification.

---

## Environment

| Component | Detail |
|---|---|
| EC2 Instance | Stress Test instance |
| Monitoring | Amazon CloudWatch |
| Notification | Amazon SNS |
| Access | AWS Systems Manager Session Manager |

---

## Objectives

- Create an Amazon SNS notification
- Configure a CloudWatch alarm
- Stress test an EC2 instance
- Confirm that an Amazon SNS email was sent
- Create a CloudWatch dashboard

---

## Files

- lab-notes.md - Full walkthrough with steps and lessons learned
- screenshots/ - Screenshots taken during the lab
