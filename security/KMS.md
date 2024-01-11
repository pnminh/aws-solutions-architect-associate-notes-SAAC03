# AWS Key Managed Service
- create and manage cryptographic keys
- control use of keys
- FIPS 140-2 valid
- used for ebs encryption
- integrated with iam for auth
- Can audit use of keys via CloudTrail
- 3 cent per 10000 api calls
- scoped per region
## Key Types

### Symetric
- AES256 keys
- single key to encrypt and decrypt
- AWS services which use KMS use this
- you can only get this key via api call

### Asymetric
- public key (encrypt)
- private key (decrypt)
- can download public key
- private key only api
- use case: encryption outside of aws which access to api

### Free
- aws managed
### Customer Manged Key (CMK)
- 1 dollar a month
- created or imported in kms

## Key Rotation

### AWS Manged key
- automatic every 1 year

### CMK
- must be enabled
- automatic very uear
- if importet only manual rotation with use of alias

## Key Policies
- similar to s3 policies
- controll access to kms
- default = everyone in this account can use the key
- use for cross account
- can also have principal as service, e.g. cloudtrail.amazonaws.com
## Multi Region Keys
- keys are replicated with same id into diffrent region
- encrypt and decypt in other keys
- use case to encrypt global services (auroa global, dynamo global tables)

## vs cloudHSM
- KMS: multi-tenant vault 
- CloudHSM: dedicated vault

## Customer Managed CMK (Customer-created):

These are CMKs that you create and manage yourself. You have full control over their lifecycle, rotation, and permissions.

## AWS Managed CMK (Service-created):

These are CMKs created and managed by AWS services, such as AWS CloudHSM or AWS Key Management Service itself.
With AWS Managed CMKs, you don't have direct control over the key's lifecycle or rotation. AWS manages these keys on your behalf.

## Master key:
- Key that can be used to encrypt/decrypt data key
- data key is short-lived one that does encryption/decryption of data
- Envelope Encryption:

The concept of envelope encryption involves using a data key to encrypt the actual data, and then protecting the data key by encrypting it with a CMK. This two-step process helps manage and secure the keys used in encryption.

## Default policy
- If key created using API: default key allows whole account full access. Account entities still need IAM(policy) with kms access to use KMS: 
```json
{
  "Sid": "Enable IAM User Permissions",
  "Effect": "Allow",
  "Principal": {
    "AWS": "arn:aws:iam::111122223333:root"
   },
  "Action": "kms:*",
  "Resource": "*"
}
```
- If key created on console: 3 parts 
  - key administrators: manage key, but cannot use it
  ```json
  {
    "Sid": "Allow access for Key Administrators",
    "Effect": "Allow",
    "Principal": {"AWS":"arn:aws:iam::111122223333:role/ExampleAdminRole"},
    "Action": [
        "kms:Create*",
        "kms:Describe*",
        "kms:Enable*",
        "kms:List*",
        "kms:Put*",
        "kms:Update*",
        "kms:Revoke*",
        "kms:Disable*",
        "kms:Get*",
        "kms:Delete*",
        "kms:TagResource",
        "kms:UntagResource",
        "kms:ScheduleKeyDeletion",
        "kms:CancelKeyDeletion"
    ],
    "Resource": "*"
  }
  ```
  - Key users: users(role/user) who use key directly or delegate to the services integrated with KMS to use it
  ```json
    {
    "Sid": "Allow use of the key",
    "Effect": "Allow",
    "Principal": {"AWS": [
        "arn:aws:iam::111122223333:role/ExampleRole",
        "arn:aws:iam::444455556666:root"
    ]},
    "Action": [
        "kms:Encrypt",
        "kms:Decrypt",
        "kms:ReEncrypt*",
        "kms:GenerateDataKey*",
        "kms:DescribeKey"
    ],
    "Resource": "*"
    },
    {
    "Sid": "Allow attachment of persistent resources",
    "Effect": "Allow",
    "Principal": {"AWS": [
        "arn:aws:iam::111122223333:role/ExampleRole",
        "arn:aws:iam::444455556666:root"
    ]},
    "Action": [
        "kms:CreateGrant",
        "kms:ListGrants",
        "kms:RevokeGrant"
    ],
    "Resource": "*",
    "Condition": {"Bool": {"kms:GrantIsForAWSResource": true}}
    }  
  ```
  Key users require these grant permissions to use their KMS key with integrated services, but these permissions are not sufficient. Key users also need permission to use the integrated services.
  
 For lambda
 ![](2024-01-11-04-34-07.png)