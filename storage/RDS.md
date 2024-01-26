![[Pasted image 20221101124548.png]]
# RDS

## TLDR
Various  relational databases, manged by aws.

## Features
- scaling capacity (up to set maximum storage, every 6h max, 5 mins needs to be low storage which is less than 10% remaining) this needs to be enabled.
- os patching
- no ssh
- monitoring dashboards
- multi az
- scaling capability

## Read replicas
- up to 5 read replicas
- eventually async replication
- can be promoted to their own database
- no cross az network cost
- cross region cost per network traffic
- can be multi AZ

## Multi AZ
- can be upgraded without downtime
- one dns name
- automatic failover to standby database by switching target ip or dns name
- sync replication
- one db will be standby
- deactive automation mode and take snapshot before modify
- automated backups will be multi region

## RDS Custom
- only for oracle and mssql
- access to underlying database and os
- ssh possible

## Security
- if you need encrpt in transit use ssl/tls by launching the client with the --ssl_ca flag
- can use [[KMS]] to encrypt data at rest

### Option

#### RDS Custom for Oracle
- allows customization to host and os

## Maintenance
- maintenence causes downtime even if the db is multi AZ

## Backups
- daily full backup during maintence window
- transactions logs are backed up by rds every 5 mins
- restory any point in time (5 mins ago)
- 1 to 35 days of retention
- The default backup retention period is 7 days if you create the DB instance using the console, 1 day if API
- 
- if multi az backups span multi region

### Manual Snapshot
- manual trigger
- retention as log as you want
- pay for the space occupied

### Savings
- take snapshot and delete database
- if you want rds back just restore with snapshot

### Restore
- restore mysql rds database from [[S3]]

## Security
- encrypt at rest with [[KMS]], must be defined at launch time
- if master is not encrypted, read replicas can not be encrypted
- to change from and to encypt use snapshot
- encrypt in flight with tls root certificates client side
- can use [[IAM]] roles to connect to database instead of username and pw on mySQL-compatible DBs
- can use [[SecurityGroup]]
- audit logs can be enabled and be send to [[CloudWatch]]


## RDS Proxy
- fully manged database proxy 
- allows apps to pool and share connection established with the database which allows less connections to database
- improves database performance
- severless
- autoscalling
- high available (multi az)
- reduces rds and aurora failover time by 66%
- enforces iam auth for db and store creds in aws secrets manager
- RDS Proxy is never public and can only be used from within the vpc
- connection pooling/similar to hikariDB?
## Enhanced Monitoring
[[CloudWatch]] feature for RDS
- RDS child processes
- RDS processes
- OS Processes
- Not available for EC2
## Authentication token
An authentication token is a unique string of characters that Amazon RDS generates on request. Authentication tokens are generated using AWS Signature Version 4. Each token has a lifetime of 15 minutes. You don't need to store user credentials in the database, because authentication is managed externally using IAM. You can also still use standard database authentication.

## vs Aurora Global
- Auroral global allows read replica in different region to be promoted to primary
- Normal RDS only allow muti-AZ replica(standby/secondary) to be promoted, not read replicas

## RDS events:
- Only for DB instance/AWS events, not related to data events(INSERT, DELETE, UPDATE)

## MS SQL Server
- encryption as rest is called transparent data encryption(TDE)
- Does not support IAM DB authentication(only MYSQL and Postgres support)
- Can force `SSL` using `rds.force_ssl` parameter and set to `true`(false by default), and require reboot to take effect