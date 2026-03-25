# Lab 01 - SimuLearn Databases in Practice - Notes

## Key AWS Concepts

| Concept | What it means |
|---------|---------------|
| RDS | Managed relational database service by AWS |
| Multi-AZ | Primary DB with standby in another AZ for high availability |
| Read Replica | Copy of DB for read-only traffic, reduces primary load |
| Security Group | Stateful firewall - return traffic is automatically allowed |
| Private Subnet | Subnet with no direct internet access - best for databases |
| Subnet Group | Tells RDS which subnets it can use across Availability Zones |

## Multi-AZ vs Read Replica - Key Difference

| Feature | Multi-AZ | Read Replica |
|---------|----------|--------------|
| Purpose | High availability | Read scalability |
| Replication | Synchronous | Asynchronous |
| Failover | Automatic | Manual promotion |
| Used for | Disaster recovery | Read-heavy workloads |

## Security Rules Applied
- Database placed in private subnet - no public internet access
- Port 3306 only open to WebServerSecurityGroup - not to 0.0.0.0/0
- Security Group referencing used instead of CIDR blocks
- Principle of Least Privilege applied throughout

## Gotchas to Remember
- Never place a database in a public subnet
- Never open port 3306 to 0.0.0.0/0
- Read Replica does NOT replace Multi-AZ for high availability
- Security Groups are stateful - NACLs are stateless (different behaviour)
