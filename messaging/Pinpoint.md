# Amazon Pinpoint
- scalable marketing comunications service
- SMS 
- push
- voice
- in App messaging
- personalize messages
- recivie replies
- scale to billions per day

## Use cases
- campaings for marketing
- transacional sms messages

## Targets for events
- [[SNS]]
- [[Kinesis]] Data Firehouse
- [[CloudWatch]] Logs

## Diffrence to SNS and SES
- Pinpoint takes care of message template schedules and campaings
- [[SNS]] [[SES]] needs app to handle this

## Journey:
- In the context of Amazon Pinpoint, a "journey" refers to a stateful and automated process that involves a series of interactions or messages between the sender (business or organization) and the receiver (end-user or customer)
- an event is an action that occurs when a user interacts with one of your applications
- events can be sent to Kinesis