![[Pasted image 20221101121751.png]]
# Inspector
- automatic Security assessments
- continues scanning of infrastructure
- package vulns (audit)
- Network reachability
- generates Risk Score

## [[EC2]]
- useses AWS System Manager Agent
- anaysle against network access
- analyse running os against known vulns

## Containers pushed to ecr
- accessment on containers on puhs

## Integration
- AWS Security Hub
- Send events to event bride

## vs detective vs guarduty vs fraud detector
- inspector: preventive: looks for weaknesses(security issues) and tell you to fix them before the structure may be collapsed(attacked)
- detective: reactive: after the attack, detective looks for the root causes 
These 2 above run on demand
- guarduty: GuardDuty is a managed threat detection service that continuously monitors and analyzes events in your AWS environment to identify potentially malicious activity.
- fraud detector: uses for business apps, not for AWS internal
In summary, Amazon Fraud Detector is primarily used by AWS customers to enhance security in their business applications by identifying and preventing fraud, while Amazon GuardDuty is focused on monitoring and securing the overall AWS environment against various security threats and malicious activities.