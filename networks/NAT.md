# NAT
- used in a public vpc subnet to enable instances in private subnet output ipv4 traffic to the internet
- supports ACLs
- supports flow logs

## Nat Instance
- dedicated ec2 instance
- port forwarding
- can be used as bastion host
- supports SG attachment

## Nat Gateway
- aws service
- higher availabilty
- higher bandwith
- less ops needed

## vs Egress only IGW
- NAT gateway blocks IPv4 incoming traffic but not IPv6 one, while EIGW blocks only IPv6 traffic but not IPv4 one