![[Pasted image 20221101172817.png]]
# Cloudformation

## TLDR
Templates to create [[VPC]] and almost any resource in AWS. Allows to create Infrastructre as Code.

## Features
- IaC
- most resources are supported
- Template versions are stored in [[S3]]

## Cloudformation StackSets
- create stacks in AWS accounts across regions using a single Template
- use the template as the basis for provisioning stacks
- use with [[AWSOrganisations]]
## cfn-init vs cfn-signal
- cfn-init: custom script run as part of instance initiation(user data)
- cfn-signal: signal CF that resource was created/updated successfully or not
## Creation Policies
- **`CreationPolicy`** meanx a resource has to be up an running for the next step to continue
## Sequence of running
- CF creates/updates resources in parallel as much as possible
- `DependsOn, UpdatePolicy, CreationPolicy` results in other resources waiting for others to finish. E.g. `CreationPolicy` in an EC2 instance will have the EC2 fully running(or depends on signal sent by cfn-init, using user-data script for example) before CF proceeds with creating other resources
  ```yaml
  Resources:
  MyEC2Instance:
    Type: AWS::EC2::Instance
    Metadata:
      AWS::CloudFormation::Init:
        config:
          packages:
            yum:
              httpd: []
          services:
            sysvinit:
              httpd:
                enabled: true
                ensureRunning: true
    CreationPolicy:
      ResourceSignal:
        Timeout: PT5M
    Properties:
      UserData:
        Fn::Base64: 
          Fn::Sub: |
            #!/bin/bash -xe
            /opt/aws/bin/cfn-init -v --stack ${AWS::StackName} --resource MyEC2Instance --region ${AWS::Region}
            /opt/aws/bin/cfn-signal -e $? --stack ${AWS::StackName} --resource MyEC2Instance --region ${AWS::Region}
  ```