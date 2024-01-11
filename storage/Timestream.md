# Timestream
- time series database
- fully managed
- scalable
- store and analyse trillions of events per day
- full sql compatibilty
- recent and historical data diffrent storage tiers
- support encrypt in transit and at rest

## Use cases 
- iot
- operational apps
- real time analytics

## Architecture

### Sources
- Lambda
- AWS Iot
- Kinesis data analytics for apache flink
- prometheus (3rd party) (monitoring metrics)
- telegraph (3rd party) (metrics)

### Targets
- quicksight
- sage maker
- grafana (Monitoring Dashboard)
- any jdbc connection

### vs appstream
appstream: stream video