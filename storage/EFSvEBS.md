# choose a volume

## EBS
- only one instace
- single az
- gp2 io increased via disk size
- io1: can increase io without disksize

## EFS 
- mounting 100 of linux ec2s 
- more expensive

## Instance Store
- i need max iops
- my data is not critical
  
## File system
- EBS: SAN
- EFS: POSIX compliant