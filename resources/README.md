# AWS Backup, Disaster Recovery and Business Continuity – Resource Reference

## 1. Overview

This document provides a centralized reference for the AWS resources created during the project.

The project uses Mumbai as its primary Region and Singapore as its cross-region backup destination.

## 2. AWS Region Reference

| Purpose | Region | Region Code |
|---|---|---|
| Primary infrastructure | Mumbai | `ap-south-1` |
| Cross-region backup destination | Singapore | `ap-southeast-1` |

## 3. Networking Resources

| Resource | Name | Configuration |
|---|---|---|
| VPC | `dr-vpc` | `10.30.0.0/16` |
| Internet Gateway | `dr-igw` | Attached to project VPC |
| Public Route Table | `dr-public-rt` | Default route through IGW |
| Private Route Table | `dr-private-rt` | Local VPC route only |
| Public Subnet A | `dr-public-a` | `10.30.1.0/24` |
| Public Subnet B | `dr-public-b` | `10.30.2.0/24` |
| Private Subnet A | `dr-private-a` | `10.30.11.0/24` |
| Private Subnet B | `dr-private-b` | `10.30.12.0/24` |

### Security Groups

| Security Group | Purpose |
|---|---|
| `dr-ec2-sg` | EC2 access |
| `dr-efs-sg` | EFS NFS access |
| `dr-rds-sg` | RDS MySQL access |

## 4. Compute Resources

| Resource | Name | Configuration |
|---|---|---|
| Application Server A | `dr-app-server-a` | Amazon Linux 2023, t3.micro |
| Application Server B | `dr-app-server-b` | Amazon Linux 2023, t3.micro |
| Recovered Server | `dr-recovered-server` | Launched from project AMI |
| AMI | `dr-app-server-ami-v1` | Application server image |

Apache is installed on the application servers to serve the project web page.

## 5. Storage Resources

### EBS

| Resource | Name | Configuration |
|---|---|---|
| Data Volume | `dr-app-data` | 5 GiB, gp3, encrypted |
| File System | XFS | Mounted at `/data` |
| Manual Snapshot | `dr-app-data-backup-v1` | Manual EBS snapshot |
| Lifecycle Policy | Name tagged for `dr-app-data` | Daily, seven-snapshot retention |

### EFS

| Resource | Name | Configuration |
|---|---|---|
| File System | `dr-efs` | Regional, Elastic, encrypted |
| File System ID | `fs-067b8f1d7cd5754be` | Mumbai Region |
| Mount Targets | Two | Located in private subnets |

### S3

| Resource | Name | Configuration |
|---|---|---|
| Bucket | `yash-dr-backup-2026` | Mumbai Region |
| Versioning | Enabled | Multiple object versions |
| Encryption | SSE-S3 | Default encryption |
| Public Access | Blocked | ACLs disabled |
| Lifecycle Rule | `dr-s3-lifecycle` | Standard-IA transition and version cleanup |

## 6. Database Resources

| Resource | Name | Configuration |
|---|---|---|
| Original RDS | `dr-mysql` | MySQL, db.t3.micro |
| Storage | — | 20 GiB gp3, encrypted |
| Deployment | — | Single-AZ, private |
| Manual Snapshot | `dr-mysql-backup-v1` | Manual snapshot |
| Restored RDS | `dr-mysql-restore-test` | Separate restored instance |
| Backup Retention | — | One day automated retention |
| Deletion Protection | — | Enabled on original instance |

**Important:** The original RDS instance has no application database or application records. It was not modified during the restoration exercise.

## 7. AWS Backup Resources

| Resource | Name | Region |
|---|---|---|
| Backup Plan | `dr-backup-plan` | Mumbai |
| Backup Rule | `dr-daily-backup` | Mumbai |
| Primary Backup Vault | `dr-backup-vault` | Mumbai |
| Cross-Region Vault | `dr-cross-region-vault` | Singapore |
| Main Resource Assignment | `dr-backup-resources` | Mumbai |
| EFS Resource Assignment | `dr-efs-backup-assignment` | Mumbai |

### Backup Rule Configuration

| Setting | Value |
|---|---|
| Schedule | Hourly |
| Starting time | 3:00 PM Asia/Calcutta |
| Start window | 1 hour |
| Completion window | 2 hours |
| Primary retention | 7 days |
| Cross-region copy retention | 7 days |

The hourly schedule is intentional.

## 8. Monitoring and Notification Resources

| Resource | Name | Purpose |
|---|---|---|
| EventBridge Rule | `dr-backup-notification-rule` | Detects backup, copy and restore job state changes |
| SNS Topic | `dr-backup-alerts` | Email notifications |
| CloudWatch Namespace | `AWS/Backup` | Backup metrics inspection |

The SNS email subscription was confirmed and a backup notification email was received.

No dedicated CloudWatch dashboard or alarm was created.

## 9. Cross-Region Recovery Reference

| Item | Configuration |
|---|---|
| Source Region | `ap-south-1` |
| Destination Region | `ap-southeast-1` |
| Destination Vault | `dr-cross-region-vault` |
| Verified recovery point | EBS |
| Verified recovery-point status | Available |

The verified cross-region recovery point is for EBS. This does not establish that every protected service has a verified cross-region copy.

## 10. Important Project Limitations

- No NAT Gateway.
- No Application Load Balancer.
- No Auto Scaling Group.
- RDS uses Single-AZ deployment.
- No automated regional failover.
- No dedicated CloudWatch dashboard or alarm.
- EBS restored-volume data content verification remains pending.
- No application database or records were created in the original RDS instance.

## 11. Related Documentation

- [Project Overview](../README.md)
- [Architecture](../architecture/aws-architecture.md)
- [Networking](../networking/README.md)
- [Compute](../compute/README.md)
- [Storage](../storage/README.md)
- [Database](../database/README.md)
- [AWS Backup](../backup/README.md)
- [Disaster Recovery](../disaster-recovery/README.md)
- [Monitoring](../monitoring/README.md)
- [Implementation](../implementation/README.md)
- [Testing](../testing/README.md)
- [Screenshots](../screenshots/README.md)

---

**Project:** AWS Backup, Disaster Recovery and Business Continuity  
**Document:** AWS Resource Reference  
**Primary Region:** `ap-south-1`  
**Backup Destination:** `ap-southeast-1`