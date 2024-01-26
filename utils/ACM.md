# AWS Certificate Manager
- manage, provision and deployu SSL Certs
- certs creaded by ACM are automaticly renewed


## IAM certificate Store
- only used for regions where ACM is not available
- can be used via cli
## Getting notification with cert nearing expiration 
- Using cloudwatch event(Event Bridge) with ACM built-in Cert Exp event
- Using scheduled EventBridge event(e.g. daily) to trigger lambda function to look into `DaysToExpiry metric` for ACM on CloudWatch