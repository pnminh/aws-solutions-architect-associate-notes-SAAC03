![[Pasted image 20221101114116.png]]
# Route 53

## TLDR
AWS Nameserver and Domain Name register Service.

## Features
- managed
- scalable
- authorative dns (can be updated by customer)
- registar (can register own names)
- 100% availabilty
- health checks


## DNS Record
- domanin name
- record Type
- value (ip)
- routing policy
- ttl

### Record types

#### A
- hostname to ipv4

#### AAAA
- hostname to ipv6

#### CNAME
- maps dns querys to another domain or subdomain
- AAAA
- CNAME
- NS

#### Alias
- can target a root domain (cname can not)
- can only be used for aws resources

## Endpoint types

### Outbound
- used by resources in [[VPC]] to resolve dns querys to resources outside of the [[VPC]]  (e.g. on premise)

## Inbound
- used by resources outside of aws to resolve name to resources inside a [[VPC]]

## Routing Types

### Weighted
- split traffic % to a % to b

### Latency based
- route to record with least latency for user

### GeoProximity
- Requires route 53 traffic flow.
- Proximity(distance) between request location and the resources. E.g. 150km between the user's IP location and EC resource location. Smallest one will be chosen 
- Can add bias
  e.g. 150km between user's IP and resource location A, 100km to location B. If location A bias is 50 and B is 0 -> bias distance for A = 150*(1-50/100) = 75km and for B=100km -> location A will be chosen. 
- https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy-geoproximity.html
### Geolocation
- Set a user's location to an AWS region
- default record for unknown IP location/anything that is not mapped
- Route 53 returns a “no answer” response for queries from those locations
## vs BIND(Berkeley Internet Name Domain)
- managed vs manual config
- BIND is for local dns server