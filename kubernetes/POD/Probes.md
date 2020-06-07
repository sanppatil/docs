
# Commands for interacting with Topics

## Display list of topics

```console
 kafka-topics --list \
     --bootstrap-server localhost:9092
 ```

## Create topic

```console
 kafka-topics --create \
     --bootstrap-server localhost:9092 \
     --replication-factor 3 \
     --partitions 6 \
     --topic sample-topic
 ```

## Describe topic

```console
 kafka-topics --describe \
     --bootstrap-server localhost:9092 \
     --topic sample-topic
 ```

## Delete topic

```console
 kafka-topics --delete \
     --bootstrap-server localhost:9092 \
     --topic sample-topic
 ```

## Find out all the partitions without a leader
>Find out all the partitions where one or more of the replicas for the partition are not in-sync with the leader
```console
 kafka-topics --describe \
     --bootstrap-server localhost:9092 \
     --topic sample-topic \
     --unavailable-partitions
 ```
