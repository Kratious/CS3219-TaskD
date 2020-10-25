# CS3219-TaskD

This repository includes 6 containers.

3 zookeeper containers and 3 kafka containers to demonstrate successful kafka pub/sub and zookeeper failover management.

# Setup

`$ docker-compose up -d`

# Kafka Pub/Sub

Go into **kafka1** container and run the following commands.

To create a topic:

`$ kafka-topics.sh --create --topic example-topic --bootstrap-server kafka1:9092, kafka2:9092, kafka3:9092`

To act as a topic publisher:

```
$ kafka-console-producer.sh --topic example-topic --bootstrap-server kafka1:9092, kafka2:9092, kafka3:9092
> Hello this is a message sent for example topic
> Another message 1
> Another message 2

```

Go into **kafka2** container and run the following commands.

To act as topic consumer:

`$ kafka-console-consumer.sh --topic example-topic --from-beginning --bootstrap-server kafka1:9092, kafka2:9092, kafka3:9092`


# Zookeeper Failover

To determine mode of each zookeeper, run the following command:

`$zkServer.sh status`

It will show `Mode: follower/leader`

Stop the leader container and re-run `$zkServer.sh status` to see that failover succeeds.

Repeat the Kafka Pub/Sub steps to verify that it still works.