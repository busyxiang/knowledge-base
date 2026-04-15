# Kafka

## Consumer Groups

- A **consumer group** is a set of consumers from the same application that work together to consume and process messages from one or more topics
- Each topic is divided into a set of ordered **partitions**
- **Each partition is consumed by exactly one consumer within each consumer group at any given time**
   - This means if you have more consumers than partitions, some consumers will be idle
   - If a consumer fails, its partitions are reassigned to other consumers in the group (**rebalancing**)
