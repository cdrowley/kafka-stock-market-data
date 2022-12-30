## Notes
- replace {your.host.name} with EC2 public IP


## Download & Uncompress Kafka
`wget https://downloads.apache.org/kafka/3.3.1/kafka_2.12-3.3.1.tgz`
`tar -xvf kafka_2.12-3.3.1.tgz`


## Install Java
`sudo yum install java-1.8.0-openjdk`
`java -version`
`cd kafka_2.12-3.3.1`


## Start Zoo-keeper
`bin/zookeeper-server-start.sh config/zookeeper.properties`


## Start / Expose Kafka-server
- Duplicate SSH Session / Console
- Kafka is running on and accessible via AWS private server
- change server properties to enable public IP connections
    - `sudo nano config/server.properties`
    - uncomment `#advertised.listeners=PLAINTEXT://{your.host.name}:9092`
    - EC2 Console > Security > Edit Inbound Rules > Add Rule (All tragic / My IP)

- allocate more memory to kafka
`export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"`

`cd kafka_2.12-3.3.1`
`bin/kafka-server-start.sh config/server.properties`


## Create Kafka Topic
- Duplicate SSH Session / Console
`cd kafka_2.12-3.3.1`
`bin/kafka-topics.sh --create --topic demo_test --bootstrap-server {your.host.name}:9092 --replication-factor 1 --partitions 1`


## Optional (to test Producer/Consumer command line)
## Start Kafka Producer
- If issues, check IP for inbound traffic (for this demo relax security then remove EC2 instance ASAP)
`bin/kafka-console-producer.sh --topic demo_test --bootstrap-server {your.host.name}:9092`

## Start Kafka Consumer
- Duplicate SSH Session / Console
`cd kafka_2.12-3.3.1`
`bin/kafka-console-consumer.sh --topic demo_test --bootstrap-server {your.host.name}:9092`
