![[Pasted image 20221102200008.png]]
# AWS Firewall Manager

## TLDR
Centraly manage firewall config and rules for [[AWSOrganisations]]

## Supported Services
- [[WAF]]
- [[AWSShield]] Advanced
- [[SecurityGroup]]
- [[NetworkFirewall]]
- [[Route53]] DNS Firewall

## Features
- region level
- automatic apply rules to new resources

## vs WAF rules
### WS Firewall Manager Rules:

#### VPC Security Group Rule:

Objective: Allow inbound traffic only from a specific IP range to your Amazon EC2 instances.
Firewall Manager Rule: Allow inbound traffic from IP range X.X.X.X to port 80 and 443 in all VPC security groups.

#### AWS Shield Advanced Rule:

Objective: Mitigate DDoS attacks by blocking traffic from known malicious IP addresses.
Firewall Manager Rule: Configure AWS Shield Advanced to block traffic from a list of identified malicious IP addresses across all protected resources.

### AWS WAF Rules:

#### SQL Injection Protection Rule:

Objective: Protect against SQL injection attacks on a web application.
WAF Rule: Create a rule that inspects incoming HTTP requests for SQL injection patterns in query parameters. Block or log requests that match the pattern.