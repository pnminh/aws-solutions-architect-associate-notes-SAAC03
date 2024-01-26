![[Pasted image 20221102200732.png]]
# AWS Backup

## TLDR
AWS Backup is a service to centraly manage and review your backup strategies.

## Features
- central place to manage and automate backups across AWS Services
- cross region backups
- cross account backupos
- PITR support
- can create backup policies (backup plans)
- tag based

## Supported: Only AWS resources
- [[EC2]] 
- [[EBS]]
- [[S3]]
- [[RDS]]
- [[Aurora]]
- [[DynamoDB]]
- [[EFS]]
- [[StorageGateway]]
- ...

## Target
- back ups in [[S3]]

## Vault Lock
- backups can not be deleted
![](2024-01-10-16-19-47.png)