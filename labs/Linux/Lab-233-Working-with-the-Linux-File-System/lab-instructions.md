# Lab 233 – Instructions

## Task 1: Connect to EC2 via SSH

### Windows (PuTTY)
1. Click **Details > Show** and download the `labsuser.ppk` file
2. Note the **PublicIP** address
3. Open PuTTY and connect using the PPK file

### Mac/Linux
```bash
cd ~/Downloads
chmod 400 labsuser.pem
ssh -i labsuser.pem ec2-user@<public-ip>
```

---

## Task 2: Create the Folder Structure
```bash
# Make sure you are in the home folder
pwd

# Create top-level folder
mkdir CompanyA
cd CompanyA

# Create subfolders
mkdir Finance HR Management

# Create HR files
cd HR
touch Assessments.csv TrialPeriod.csv
cd ../Finance

# Create Finance files
touch Salary.csv ProfitAndLossStatements.csv
cd ..

# Create Management files
touch Management/Managers.csv Management/Schedule.csv

# Validate everything
ls -laR
```

### Expected Structure
```
CompanyA/
├── Finance/
│   ├── ProfitAndLossStatements.csv
│   └── Salary.csv
├── HR/
│   ├── Assessments.csv
│   └── TrialPeriod.csv
└── Management/
    ├── Managers.csv
    └── Schedule.csv
```

---

## Task 3: Reorganize the Folder Structure
```bash
# Make sure you are in CompanyA
pwd

# Copy Finance into HR, then delete the original
cp -r Finance HR
rm Finance/ProfitAndLossStatements.csv Finance/Salary.csv
rmdir Finance

# Move Management into HR
mv Management HR

# Create Employees folder and move HR files into it
cd HR
mkdir Employees
mv Assessments.csv TrialPeriod.csv Employees

# Validate
ls . Employees
```

### Final Structure
```
CompanyA/
└── HR/
    ├── Employees/
    │   ├── Assessments.csv
    │   └── TrialPeriod.csv
    ├── Finance/
    │   ├── ProfitAndLossStatements.csv
    │   └── Salary.csv
    └── Management/
        ├── Managers.csv
        └── Schedule.csv
```
