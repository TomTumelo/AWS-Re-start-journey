# Lab 02 - Personal Notes

## Key AWS Services Used

| Service | Purpose |
|---------|---------|
| Amazon RDS | Managed relational database in the cloud |
| VPC Security Group | Controls inbound and outbound traffic to RDS |
| DB Subnet Group | Tells RDS which subnets to use across AZs |
| EC2 Web Server | Application layer that connects to RDS |

## Key Commands and Concepts

| Concept | What it means |
|---------|---------------|
| Multi-AZ | Primary DB with automatic standby in another AZ |
| DB Subnet Group | Requires subnets in at least two Availability Zones |
| Port 3306 | Default MySQL port |
| Endpoint URL | The address your app uses to connect to RDS |
| Security Group referencing | Allowing traffic from another SG instead of an IP range |

## Architecture Summary
```
Internet
    |
Web Server (EC2) - Public Subnet
    |
    | Port 3306
    |
RDS MySQL (Primary) - Private Subnet AZ1
    |
RDS MySQL (Standby) - Private Subnet AZ2
```

## Security Rules Applied
- RDS placed in private subnets - no public internet access
- Port 3306 only open to Web Security Group - not to 0.0.0.0/0
- Security Group referencing used - follows Principle of Least Privilege
- Removed default security group from RDS instance

## Multi-AZ vs Read Replica Reminder

| Feature | Multi-AZ | Read Replica |
|---------|----------|--------------|
| Purpose | High availability | Read scalability |
| Replication | Synchronous | Asynchronous |
| Failover | Automatic | Manual promotion |
| Serves traffic | No (standby only) | Yes (read-only) |

## Gotchas to Remember
- DB Subnet Group needs subnets in at least 2 Availability Zones
- Always remove the default security group from RDS
- Endpoint URL only appears after RDS status is Available
- Disabling automated backups speeds up lab but is not recommended in production
- Multi-AZ standby does NOT serve read traffic - it is only for failover
