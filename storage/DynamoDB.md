![[Pasted image 20221101212132.png]]
# DynamoDB

## TLDR
NoSQL Serverless DB. Tons of features and can be global.

## Features
- NoSQL
- serverless
- milisec latency
- key value doc db
- single digit milisecond performance
- multi az
- fully manged
- multi master
- backup and restore
- in memory caching
- transaction capabilty

##  Capacity Modes
- provisoned capacity with optional autoscaling
  - if autoscaling is disabled, initial provision capacity is fixed
  - otherwise, initial provision capacity is for init, then autoscaling kicks in and can change the numbers
- on demand capacity
- can change modes with no downtime

## Use cases
- can replace elasticache (storing session data with ttl feature)
 - serverless apps
 - rapidly evolve schemas
 - small documents 100bs
 - distributed serverless cache

## DAX cluster
- read cache 
- in memory
- microsecond read latency

## Auth
- [[IAM]]

## Dynamo DB Stream
- event processing
- invoke [[Lambda]] or send to [[Kinesis]]
- 24 hour retention 
- limited number of consumers

## Dynamo DB Kinesis Data Steams
- 1 year retention
- all features of [[Kinesis]]

## Global Tables
- active/active setup for multi region
- two way replication
- must enable Streams as prerequiste

## Backups
- automated backups up to 35 days with PITR to restore to new table
- on demand backups

## Export
- export import to [[S3]]

## Security
- support [[KMS]] Customer Managed Key

## CLI Created Tabled
- Autoscaling wont be enabled by default
## Ondemand backup vs AWS backup
- ondemand only creates backup in same account and region
- to copy backup to other regions/accounts, need AWS backup