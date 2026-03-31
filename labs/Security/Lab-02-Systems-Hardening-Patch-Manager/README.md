# Lab 02 - Systems Hardening with Patch Manager

## Overview

In this lab, I used AWS Systems Manager Patch Manager to patch both Linux and Windows EC2 instances. I created a custom patch baseline for Windows security updates and used patch groups to target specific instances.

---

## Environment

| Component | Detail |
|---|---|
| Service | AWS Systems Manager - Patch Manager |
| Instances | 3 Linux + 3 Windows EC2 instances |
| Linux Baseline | AWS-AmazonLinux2DefaultPatchBaseline |
| Windows Baseline | Custom - WindowsServerSecurityUpdates |

---

## Objectives

- Patch Linux instances using default baseline
- Create a custom patch baseline for Windows
- Use patch groups to target Windows instances
- Verify patch compliance across all instances

---

## Files

- lab-notes.md - Full walkthrough with steps and lessons learned
- screenshots/ - Screenshots taken during the lab
