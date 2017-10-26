There are two topics in Kafka right now:
  1. to-module -- for messages, intended to consume in modules
  2. to-connector -- respectively, in connectors

Kafka broker and Zookeeper are up on standard ports 9092 and 2181, respectively.

To consume or produce messages we need to connect to Kafka broker using some Kafka-client library.

## DevOps:

Kafka resides now in directory ~soft/kafka_2.11-0.11.0.0, though, it's subject to change. Descriptions of all operations presented here assume, that we're under user `soft` and in Kafka directory.

### Start Zookeeper:

`$ bin/zookeeper-server-start.sh config/zookeeper.properties`

### Start Kafka:

`$ bin/kafka-server-start.sh config/server.properties`

**TODO**: need to automize these operations on startup.
