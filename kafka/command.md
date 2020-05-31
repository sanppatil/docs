
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

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
