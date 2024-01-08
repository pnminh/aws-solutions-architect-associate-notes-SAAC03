![[Pasted image 20221101210003.png]]
# VPC Virtual Private Cloud

## TLDR
A stack of AWS resources, more clearly the connectivity and setup options for and between these resources.

## Console Wizard

### Options

#### VPC with public subnet
- single public subnet
- internet gateway
- recommended for simple public facing application

#### VPC withg public and private subnets
- public subnet
- private subnet
- internet gateway
- recommended for 2 tier application

#### VPC with public, private subnets and AWS Site-to-Site [[VPN]]
- public subnet
- private subnet
- virtual private gatway
- internet gateway
- recommended to extend network into the cloud and some resource are internet facing

#### VPC with private subnet and AWS Site-to-Site [[VPN]]
- private subnet
- virtual private gateway
- recommended to extend private network into the cloud

## VPC Endpoint
- privatly connect a VPC to supported services 
- does not require an internet gateway, [[NAT]], [[VPN]] or [[DirectConnect]]
- instances dont require public ip adresses
- uses AWS Private Link as connection Line
- data does not leave AWS while communicatiing
- doesn not support inter region communication

### Interface Endpoint
- eni with private ip adress in the target subnet

### Gateway Endpoint
- only for [[S3]] and [[DynamoDB]]
- gateway which you set as a route target 

## VPC Peering
- connection between 2 VPCs using private adresses
- not transitive
- need to setup route tables

### Transit Gatway
- hub for multiple peering connections
- attach options are, vpc, direct connect gateway or another transit gateway either as peering or vpn
- MTU = max package size
- MTU 85kbs if direct connect or peering vpc
- MTU 15kbs if [[VPN]]
- has a route table
- route propagation
- gives double throughput of virtual private gateway by using ECMP support

## VPC Sharing
- share one or more subnets within other accounts beloning to the same [[AWSOrganisations]]
- every account can only work with the resources they created

## VPC Flow Logs
- Capture Information about IP traffic through your interfacines
- VPC Flow Logs
- Subnet Flow Logs
- ENI Flow Logs

### Other Sources
- [[ELB]]
- [[RDS]]
- [[ElastiCache]]
- [[Redshift]]
- WorkSpaces 
- NATGW
- Transit Gateway
...


### Targets
- [[S3]]
- [[CloudWatch]] Logs
### Information
- ip information
- port information
- action (accept/reject)

### Query
- [[S3]] Athena
- [[CloudWatch]] Logs Insights

## NACL
- not stateful
- firewall on subnet level
- for outbound traffic allow ephemeral ports 32768-65535 (all ports for diffrent services to listen for outbound traffic)

## VPC Traffic Mirroring
- capture and inspect network traffic
- unintrusive
- traffic gets direct to security applicance fleet
- fleet redicet traffic back

## Note
- each subnet has 5 IPs not available to use
- VPC between a /28 netmask and /16 netmask
## Public subnet
- create IGw and attach to VPC
- add 0.0.0.0/0 dest to IGW in the routeables(can be default or a new one, should only be used for public subnets after this)

## Private subnet
- create new routeable and only attach a private subnet to it
- create NAT gateway into public subnet
- add 0.0.0.0/0 to nat-gw for the routeable above
- to access EC2 instance connect endpoint(for private subnet)=> create VPC endpoint 
- separate NACL for private subnet: when creating custom NACL, default is deny for both inbound and outbound
  - need both ephemeral ports(32768-65535) for inbound and outbound
  - other ports that are required

## Virtual private gateway vs transit gateway
- Use TGW if:
You have multiple VPCs in a region that need to connect to each other or your on-premises network.
You need a centralized and scalable hub for managing your network connections.
You require complex traffic routing and isolation between networks.
- Use VGW if:
You only have a single VPC and need to connect it to a single on-premises network.
You want a simple and affordable solution for secure remote access.
You don't need advanced routing or traffic segmentation features.
## Virtual private gateway vs direct connect gateway
- Direct connect gateway can connect multiple VPCs and on-prem networks
- Each VPC uses VGW to connect to DGW