![[Pasted image 20221101165431.png]]
# AWS Shield

## TLDR
Protect your resources from DDOS Attacks.



## Features
- is enabled by default with no additional cost
- SYN UDP Floods, Refelction attcks or other layer3 and layer4 attacks

## AWS Shield Advanced 
- optional paid service
- pay per organisation
- works for [[EC2]], [[ELB]], [[Cloudfront]], [[GlobalAccelerator]] and [[Route53]]
- 24/7 AWS DDOS Support Team
- 3k per month cost
- no higher fees due to ddos fees are nulled (dont pay for increased traffic)
- automaticly deploys state of the art [[WAF]] rules

## vs WAF
AWS Shield protects against massive crowds trying to overwhelm your website.
AWS WAF protects against individual visitors trying to sneak in with malicious intent.

AWS Shield is more focused on the network layer (layers 3 and 4), can do level7 DDOS detection with detect attacks like HTTP floods and DNS floods.
AWS WAF is focused on the application layer (layer 7).

AWS Shield is more capable of preventing DDOS attacks