# AWS Backup, Disaster Recovery and Business Continuity – Screenshots

## 1. Overview

This directory contains visual evidence of the AWS infrastructure, backup configuration, disaster recovery exercises and monitoring setup.

Screenshots help demonstrate the actual AWS resources and validation results performed during the project.

All screenshots should represent the real AWS environment.

## 2. Screenshot Categories

Organize screenshots using the following categories.

| Category | Evidence to capture |
|---|---|
| Networking | VPC, subnets, route tables and security groups |
| Compute | EC2 instances and application page |
| AMI Recovery | AMI details and recovered EC2 instance |
| EBS | Volume configuration, snapshot and restored volume |
| EFS | File system, mount targets and shared-file test |
| S3 | Bucket settings, versioning and object versions |
| RDS | Original DB configuration and restored DB status |
| AWS Backup | Backup plan, vaults and completed jobs |
| Cross-Region DR | Singapore backup vault and available EBS recovery point |
| Monitoring | EventBridge rule and SNS notification configuration |
| Notifications | Received backup notification email |

## 3. Recommended Screenshot Naming

Use descriptive filenames so evidence is easy to identify.

```text
screenshots/
├── README.md
├── 01-vpc-overview.png
├── 02-subnet-configuration.png
├── 03-route-tables.png
├── 04-security-groups.png
├── 05-ec2-instances.png
├── 06-application-page.png
├── 07-ami-configuration.png
├── 08-recovered-ec2-instance.png
├── 09-ebs-volume-configuration.png
├── 10-ebs-restored-volume.png
├── 11-efs-file-system.png
├── 12-efs-shared-file-test.png
├── 13-s3-versioning.png
├── 14-s3-object-versions.png
├── 15-rds-configuration.png
├── 16-rds-restored-instance.png
├── 17-backup-plan.png
├── 18-backup-vaults.png
├── 19-completed-backup-jobs.png
├── 20-singapore-recovery-point.png
├── 21-eventbridge-rule.png
├── 22-sns-notification.png
└── 23-backup-email.png
```

These are suggested filenames. Add a screenshot only after capturing the corresponding evidence.

## 4. Screenshot Guidelines

- Capture screenshots directly from the AWS Console or actual test environment.
- Keep resource names and relevant status information visible.
- Prefer screenshots that show the complete configuration or result.
- Use readable image resolution.
- Avoid duplicate or unrelated screenshots.
- Do not edit screenshots in a way that changes the displayed AWS status.
- Do not include passwords, access keys, secret values, session tokens or other sensitive information.
- Hide account identifiers and personal email addresses before publishing where practical.

## 5. Evidence Verification

Before publishing screenshots:

1. Confirm that each screenshot belongs to this project.
2. Confirm that the displayed resource or test result is genuine.
3. Check that the image is readable.
4. Remove sensitive information.
5. Use the recommended naming convention.
6. Verify that the screenshot matches the relevant documentation.

## 6. Important Notes

Not every suggested screenshot has necessarily been captured.

The screenshot list is an evidence collection checklist, not a claim that all evidence is already available.

The documentation must remain consistent with the actual AWS implementation and test results.

---

**Project:** AWS Backup, Disaster Recovery and Business Continuity  
**Directory:** `screenshots/`  
**Primary Region:** `ap-south-1`  
**Backup Destination:** `ap-southeast-1`