# Lab 01 - SimuLearn Databases in Practice

## Overview
Hands-on lab covering Amazon RDS provisioning, VPC integration, security group
configuration, read replica creation and multi-tier architecture design.

## Implementation Breakdown

### RDS Deployment
- Engine: MySQL
- Instance class: db.t3.micro
- Storage: General Purpose (gp2/gp3)
- Database identifier: simulearn-db
- Public access: Disabled
- VPC: Lab VPC
- Subnet group: Private subnets
- Outcome: RDS instance successfully provisioned and available

### Security Configuration
- Security Group Modified: DbServerSecurityGroup
- Inbound Rule: MySQL/Aurora, TCP, Port 3306, Source: WebServerSecurityGroup
- Follows Principle of Least Privilege
- Restricts access to only the application layer
- Uses Security Group referencing instead of CIDR
- Security Groups are stateful - return traffic is automatically allowed

### Read Replica Setup
- Created to improve read scalability
- Reduces load on primary instance
- Simulates production-grade scaling pattern
- Replica receives asynchronous replication
- Used for read-only workloads
- Not a backup solution
- Does not automatically fail over unless promoted

## Security Best Practices Applied
- Database in private subnet
- No 0.0.0.0/0 access on port 3306
- Separation of compute and data layers
- Security Group referencing
- Backup configuration enabled
- Multi-layer architecture design

## Key Concepts Practiced
- Amazon RDS provisioning
- VPC integration
- Subnet group selection
- Security Groups (stateful firewall behavior)
- MySQL connectivity
- Read Replica creation
- Multi-tier architecture reasoning

## Common Mistakes Avoided
- Placing database in public subnet
- Enabling public access unnecessarily
- Opening MySQL to entire CIDR block
- Modifying NACL instead of Security Group
- Confusing Multi-AZ with Read Replica

## Skills Demonstrated
- Cloud architecture reasoning
- Secure database configuration
- Network-level troubleshooting
- Infrastructure documentation
- AWS service integration
- Structured technical communication

## Learning Reflection
This lab strengthened understanding of:
- How databases integrate into cloud networking
- The importance of controlled internal traffic
- How read scaling differs from high availability
- Why architecture design matters beyond simple deployment

## Next Steps
- Implement Multi-AZ deployment for high availability
- Compare RDS vs DynamoDB use cases
- Simulate failure and promote read replica
- Explore parameter groups and performance tuning
- Implement automated backups and snapshot recovery

## Learning Philosophy
Input -> Configuration -> Security -> Validation -> Documentation
Every component is part of a larger architecture chain.
