![[Pasted image 20221102200252.png]]
# AWS Network Firewall

## TLDR
Firewall for a [[VPC]]
- configured at VPC level and not subnet
## Features
- 1000s of rules
- protocol rules
- stateful domain list group (e.g. only allow traffic to *.google.com)
- general pattern matching using regex
- send logs to [[S3]], [[CloudWatch]] , or [[Kinesis]] firehouse
- inspect packets go in and out of VPC
- filtering
- custom lists of bad domains
- pass traffic throw know AWS services and endpoints like S3
## Filter
- Alow
- Drop
- Alert

## Active flow inspection
- intrusion preventions (Managed by AWS)
- - cannot integrate directly with ELB
## vs NACLs
- NF is stateful, NACLs is stateless