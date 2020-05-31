
## Kafka Commands

### Display  list of topics 

```console
 kafka-topics --list \
     --bootstrap-server localhost:9092
 ```

### Create topic

```console
 kafka-topics --create \
     --bootstrap-server localhost:9092 \
     --replication-factor 3 \
     --partitions 6 \
     --topic sample-topic
 ```

### Describe topic

```console
 kafka-topics --describe \
     --bootstrap-server localhost:9092 \
     --topic sample-topic
 ```

### Delete topic

```console
 kafka-topics --delete \
     --bootstrap-server localhost:9092 \
     --topic sample-topic
 ```

### Find out all the partitions without a leader
>Find out all the partitions where one or more of the replicas for the partition are not in-sync with the leader
```console
 kafka-topics --describe \
     --bootstrap-server localhost:9092 \
     --topic sample-topic \
     --unavailable-partitions
 ```

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
