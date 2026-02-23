.

🐧 Lab 233 – Working with the Linux File System
📌 Overview

This lab focuses on mastering Linux file system operations inside an Amazon Linux EC2 instance.

You will:

Create a structured directory hierarchy

Create files

Copy directories

Move directories

Delete files and folders

Validate changes using Linux commands

This lab reinforces core Linux administration skills inside AWS.

🧰 Prerequisites

Before starting:

AWS Academy / AWS Lab access

Running Amazon Linux EC2 instance

SSH access (PuTTY for Windows OR Terminal for Mac/Linux)

Basic Linux command knowledge

🚀 Task 1 – Connect to EC2 via SSH
Step 1 – Start the Lab

Click Start Lab

Wait until Lab Status: Ready

Click AWS to open the AWS Management Console

Step 2 – Download Key Pair
🪟 Windows Users

Go to Details → Show

Download labsuser.ppk

Open PuTTY

Enter Public IP

Load .ppk file under SSH → Auth

Click Open

🍎 Mac/Linux Users

Download labsuser.pem

Open Terminal

Navigate to Downloads:

cd ~/Downloads

Change permissions:

chmod 400 labsuser.pem

Connect to EC2:

ssh -i labsuser.pem ec2-user@<public-ip>

Type yes if prompted

🏗 Task 2 – Create Folder Structure
🎯 Goal Structure
/home/ec2-user/CompanyA/
├── Finance/
│   ├── Salary.csv
│   └── ProfitAndLossStatements.csv
├── HR/
│   ├── Assessments.csv
│   └── TrialPeriod.csv
└── Management/
    ├── Managers.csv
    └── Schedule.csv
Step 1 – Navigate Home
pwd
cd /home/ec2-user
Step 2 – Create Main Folder
mkdir CompanyA
cd CompanyA

Verify:

ls
Step 3 – Create Subdirectories
mkdir Finance HR Management

Verify:

ls
Step 4 – Create HR Files
cd HR
touch Assessments.csv TrialPeriod.csv
ls
Step 5 – Create Finance Files
cd ../Finance
touch Salary.csv ProfitAndLossStatements.csv
ls
Step 6 – Create Management Files
cd ..
touch Management/Managers.csv Management/Schedule.csv
ls Management
Step 7 – Validate Entire Structure
ls -laR

This recursively shows all directories and files.

🔄 Task 3 – Reorganize Structure
🎯 New Structure
CompanyA/
└── HR/
    ├── Finance/
    │   ├── Salary.csv
    │   └── ProfitAndLossStatements.csv
    ├── Management/
    │   ├── Managers.csv
    │   └── Schedule.csv
    └── Employees/
        ├── Assessments.csv
        └── TrialPeriod.csv
Step 1 – Confirm Location
pwd

Should show:

/home/ec2-user/CompanyA
Step 2 – Copy Finance into HR
cp -r Finance HR

Verify:

ls HR/Finance
Step 3 – Delete Old Finance Folder

Remove files first:

rm Finance/ProfitAndLossStatements.csv Finance/Salary.csv

Then remove directory:

rmdir Finance

Verify:

ls
Step 4 – Move Management into HR
mv Management HR

Verify:

ls HR/Management
Step 5 – Create Employees Folder
cd HR
mkdir Employees
Step 6 – Move HR Files into Employees
mv Assessments.csv TrialPeriod.csv Employees

Verify:

ls Employees
🧪 Final Validation

Run:

ls -laR
