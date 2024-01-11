 # EC2 Instance Store

- hardware disk, lower latency than ebs
- better IO performance
- Data will be lost if instance is stopped (ephemeral)
- Good for buffer, cache, scratch data, temporary content
- Hardware fail loses data
- Backup and Replication recommended (manual)

## Behavior
- When rebooted: still available, EIP still attached to instance
- When stopped: lost, EIP detached from instance
- 