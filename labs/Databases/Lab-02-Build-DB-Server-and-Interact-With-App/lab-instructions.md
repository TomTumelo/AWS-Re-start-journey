# Lab 02 - Instructions

## Task 1: Create a Security Group for the RDS DB Instance

1. Go to AWS Console > VPC > Security Groups
2. Click Create security group and configure:
   - Name: DB Security Group
   - Description: Permit access from Web Security Group
   - VPC: Lab VPC
3. Add Inbound rule:
   - Type: MySQL/Aurora (3306)
   - Source: Web Security Group
4. Click Create security group

---

## Task 2: Create a DB Subnet Group

1. Go to AWS Console > RDS > Subnet groups
2. Click Create DB Subnet Group and configure:
   - Name: DB Subnet Group
   - Description: DB Subnet Group
   - VPC ID: Lab VPC
3. Add Subnets:
   - Select both Availability Zones
   - Select 10.0.1.0/24 and 10.0.3.0/24
4. Click Create

---

## Task 3: Create an Amazon RDS DB Instance

1. Go to RDS > Databases > Create database
2. Configure:
   - Engine: MySQL (latest version)
   - Template: Dev/Test
   - Availability: Multi-AZ DB Instance
   - DB identifier: lab-db
   - Master username: main
   - Master password: lab-password
   - Instance class: db.t3.medium (Burstable)
   - Storage: General Purpose SSD
   - VPC: Lab VPC
   - Security Group: DB Security Group (remove default)
   - Initial database name: lab
   - Disable automated backups
   - Disable Enhanced Monitoring
3. Click Create database
4. Wait for status to show Available
5. Copy the Endpoint URL from Connectivity and Security section

---

## Task 4: Interact With Your Database

1. Copy the WebServer IP from AWS Details
2. Open the WebServer IP in a browser
3. Click the RDS link at the top
4. Configure the connection:
   - Endpoint: (paste endpoint copied earlier)
   - Database: lab
   - Username: main
   - Password: lab-password
5. Click Submit
6. Test by adding, editing and removing contacts in the Address Book
