![[Pasted image 20221031085227.png]]
# Directory Service

## TLDR
A collection of sub services which allows companies to leverage directory authentication within AWS. Supports Microsoft Active Directoy.

## Versions

### AWS Managed Active Directory
- The Active Directory is managed on aws side.
- Can also be used on premise, a 2 side trust connection is established between aws AD and on prem AD

## AD Connector
- Can use on prem ad auth in aws, by proxying to the ad domain controller on premise
- AD is managed on premise

## Simple AD
- Create a new AD managed in AWS 
- No on prem AD required but can be joined

##  AWS Managed Microsoft Active Directory vs Self-managed Microsoft Active Directory
- AWS Managed Microsoft Active Directory: managed by AWS
- Self-managed Microsoft Active Directory: hosted on EC2, managed by users

## AD connector vs SAML with MS ADFS
AD Connector is like a Bridge:

AD Connector acts like a secure bridge between your existing office and the new cloud office, allowing employees to use the same keys.
Federated IdP is like a New Security System:

Setting up a federated Identity Provider with SAML and ADFS is like installing a new security system for your cloud office, complete with its own set of keys.
Choose the approach that suits your company's needs. AD Connector is like extending the existing setup to the cloud, while the federated IdP is like setting up a new, more independent security system specifically for the cloud.