
# AWS SimuLearn – IAM Groups and Users Lab

## 📌 Lab Overview

In this lab, I worked with AWS Identity and Access Management (IAM) to understand how access control works in AWS.

The goal of this lab was to:

- Create IAM groups
- Create IAM users
- Add users to groups
- Attach AWS managed policies to groups
- Validate user permissions

This lab demonstrates how AWS uses role-based access control (RBAC) to manage permissions securely and efficiently.

---

## 🎯 Objectives

By the end of this lab, I was able to:

- Understand IAM structure (Users → Groups → Policies)
- Create and configure IAM users
- Create IAM groups
- Attach AWS managed policies
- Test and validate assigned permissions

---

## 🛠 Services Used

- AWS IAM
- AWS Management Console

---

## 🧱 Lab Architecture

IAM Best Practice Used:

Users ➜ Assigned to Groups ➜ Groups Assigned Policies

Instead of attaching permissions directly to users, permissions were assigned to groups for better scalability and security.

---

## 🔹 Step 1 – Create IAM Group

1. Navigate to IAM in AWS Console
2. Click **User Groups**
3. Click **Create group**
4. Name the group
5. Attach an AWS managed policy
6. Create group

---

## 🔹 Step 2 – Create IAM Users

1. Click **Users**
2. Click **Create user**
3. Enter username
4. Enable console access
5. Set password options
6. Assign user to previously created group
7. Create user

---

## 🔹 Step 3 – Attach AWS Managed Policy to Group

1. Open IAM
2. Select the group
3. Click **Attach policies**
4. Choose an AWS managed policy
5. Confirm attachment

---

## 🔹 Step 4 – Validate Permissions

1. Sign in as the IAM user
2. Attempt to access AWS services
3. Confirm access matches assigned policy

---

## 📷 Screenshots

Screenshots of each step are available in the `screenshots/` folder.

---

## 🔐 Security Best Practice Learned

- Always assign permissions to groups, not individual users
- Follow the principle of least privilege
- Use AWS managed policies when appropriate

---

## 📚 Key Takeaway

IAM is the foundation of AWS security.  
Understanding how users, groups, and policies interact is critical for secure cloud environments.

---

## 👤 Author

Tom Tumelo  
AWS Re/Start Journey 🚀
