![[Pasted image 20221101210837.png]]
# Amazon Aurora

## TLDR
AWS Created custom DB tech, very high performan. Useful for global and serverless relational database applications.

## Features
- not open source
- MySQL and Postgre
- global
- self healing
- fault tolerant
- autoscaling up to 64 TB per instance
- is a cluster
- multi az
- each az has a copy of the cluster
- 5x faster than mysql
- 3x fast than postgre
- up to 15 replicas
- faster replication
- 20% more cost than [[RDS]]
- restore to any point in time

## Primary DB
- read and write
- only one per cluster
- if fails a replica will be promoted

## Aurora Replica
- same storage as primary
- multiple per az possible
- only read
- reader endpoint does load balancing
- can enable replica autoscaling

## Custom Endpoints
- subset of aurora instances as custom endpoint(e.g. larger instance type for analytical queries)

## Aurora Serverless
- automated db instantiation and autoscaling
- for unpredictable workloads
- pay per second
- client talks to aurora proxy fleet
### Failover with one AZ down
- If your provisioned or Aurora Serverless v2 cluster contains any reader instances in other AZs, Aurora uses the failover mechanism to promote one of those reader instances to be the new primary instance.

- If your provisioned or Aurora Serverless v2 cluster only contains a single DB instance, or if the primary instance and all reader instances are in the same AZ, make sure to manually create one or more new DB instances in another AZ.

- If your cluster uses Aurora Serverless v1, Aurora automatically creates a new DB instance in another AZ. However, this process involves a host replacement and thus takes longer than a failover.
=> v1 doesn't provide read-replica so no direct failover????
## Aurora multi master
- all nodes are read/write nodes there is no master
- replication between all nodes
- use for inmmediate failover

## Global Aurora Database
- 1 primary region for read an write
- up to 5 secondary read regions
- up to 16 read replicas for each read region
- less than 1 second for replication across region

## Aurora machine learning
- ML based predications to your apps via SQL

### Use cases
- fraud detection
- add targeting
- sentiment analysis
- product recommendations

### Services
- [[SageMaker]]
- [[Comprehend]]

## Backups

### Automated 
- 1 to 35 days
- can not be disabled
- point in time recovery in that timeframe
- can be exported to s3 but needed to be copied first
### Manual
- triggered by user
- keep as long as user wants

### Restore
- into new database

### Cloning
- create a new aurora cluster from a existing one
- faster than snapshot & restore
- cost effective
- usful to create staging

### AWS Backup
- Allow retention above limit of automated backups, e.g 80 days
- Backup plan does automation with backup that is outside of Aurora automated one, e.g. once a day
## Lambda

### Store Procedure
- Can trigger a AWS Lambda function from a SP

## Cluster endpoint vs custom endpoint
- cluster endpoint: main endpoint that allows write to primarydb
- custom: can include write instance and read instances, or just for read

## Once instance only failover
- For Aurora: if the instance is down, another one will be created in the same AZ, but if that is unsuccessful instance is created on a new AZ
- For Aurora Serverless:
  - v1: a new instance is created on different AZ
  - v2: requires manual creation of new instance(v2 supports read replicas so if there is read replica available the failover can take place automatically, similar to Aurora multiAZ)
Note: for AUrora multiAZ: CNAME points to read replica