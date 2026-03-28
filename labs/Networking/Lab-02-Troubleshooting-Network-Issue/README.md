# Lab 02 - Troubleshooting a Network Issue

## Overview

In this lab, I took on the role of a **Cloud Support Engineer at AWS**, helping a customer (Ana, a contractor) who could not reach her Apache web server from a browser or ping it from the internet.

I worked with an exact replica of the customer VPC to diagnose and fix the issue.

---

## Objectives

- Analyze a customer networking scenario
- Install and start an Apache (httpd) web server on an EC2 instance
- Investigate VPC configuration to find what was blocking access
- Restore HTTP connectivity to the web server

---

## Issue Found and Fixed

**Symptom:** Apache was running but the public IP would not load in a browser.

**Cause:** A VPC configuration error was blocking inbound HTTP traffic to the instance.

**Fix:** Corrected the relevant VPC setting to allow inbound traffic on port 80.

---

## Files

- lab-notes.md — Full walkthrough with commands, findings, and lessons learned
- screenshots/ — Screenshots taken at each key step
- original-overview/ — Original lab instructions for reference
