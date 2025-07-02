# Kafka Docker Demo

Spin up ZooKeeper & Kafka with Docker Compose, then produce and consume a test message.

## Prerequisites

- Docker  
- Docker Compose  

## Quick Start

1. Launch ZooKeeper & Kafka
   docker compose up -d

2. Verify both services are running
   docker ps

   You should see zookeeper on port 2181 and kafka on port 9092.


## Usage
1. Create a Topic
   docker exec kafka \
     kafka-topics.sh --create \
       --topic test-topic \
       --bootstrap-server localhost:9092 \
       --partitions 1 \
       --replication-factor 1

   Confirm it exists:
   docker exec kafka \
   kafka-topics.sh --list \
   --bootstrap-server localhost:9092

2. Produce a Message
   docker exec -it kafka \
     kafka-console-producer.sh \
       --topic test-topic \
       --bootstrap-server localhost:9092
   Type your message

3. Consume the Message
   docker exec kafka \
     kafka-console-consumer.sh \
       --topic test-topic \
       --from-beginning \
       --bootstrap-server localhost:9092 \
       --max-messages 1
   Expected output:
    Hello from Kafka!
    Processed a total of 1 messages
   
   
