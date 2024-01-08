![[Pasted image 20221030232125.png]]
# Kubernetes

## TLDR
Kubernetes in AWS. [[ECS]] Default options are not Kubernetes, but AWS own tech.

## Options

### Manged Node Groups
- Creates [[EC2]] instances for you
- [[ASG]] managed by [[EKS]]
- Supports on demand and spot instances

### Self Managed
- [[EC2]] are created by the user and registered to the cluster
- Can use prebuild [[EKS]] optimized [[AMi]]
- Supports on demand or spot instaces

### Fargate
- No nodes, instances or maintance required

## Data volumes
- Need to specify storage class
- [[EBS]] (for [[EC2]] version only)
- [[EFS]] (works with fargate)
- [[FSxLustre]]
- FSx for NetApp ONETAP

## Authentification
- Need a config map to map IAM to Kubernetes RBAC System (is automaticly created)

## etcd encryption
By using AWS Secret Manager with a new AWS KMS key, you can add an extra layer of security to your EKS cluster's etcd key-value store. To do this, you need to create a new KMS key in the AWS KMS console, then create a new secret in the AWS Secret Manager console, specifying the new KMS key as the encryption key. Finally, you can configure your EKS cluster to use the new secret by creating a Kubernetes secret object that references the AWS Secret Manager secret.
https://aws.amazon.com/blogs/containers/using-eks-encryption-provider-support-for-defense-in-depth/