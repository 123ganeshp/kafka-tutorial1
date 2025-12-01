# 🚀 Spring Boot Kafka Basics Project

This project demonstrates the **basic concepts of Apache Kafka** using a simple Spring Boot application.  
It includes a Kafka **producer** and **consumer** using the official Spring Kafka dependency.

---

## 📌 Project Features

- Basic Kafka producer in Spring Boot
- Basic Kafka consumer in Spring Boot
- REST endpoint to publish messages
- Kafka message logging
- Configurable topic name
- Uses Apache Kafka 4.x in **KRaft mode**
- All essential Kafka CLI commands included (MacOS)

---

## 📦 Dependencies Used

Add these dependencies in your `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

🟧 Kafka Commands (MacOS)
1️⃣ Go to Kafka Folder
cd /Users/ganeshpawar/Downloads/kafka
2️⃣ Create KRaft Config Folder & broker.properties
mkdir -p config/kraft
nano config/kraft/broker.properties
Paste the following:

process.roles=broker,controller
node.id=1
controller.quorum.voters=1@localhost:9093
listeners=PLAINTEXT://localhost:9092,CONTROLLER://localhost:9093
inter.broker.listener.name=PLAINTEXT
controller.listener.names=CONTROLLER
log.dirs=/tmp/kraft-combined-logs
num.network.threads=3
num.io.threads=8
socket.send.buffer.bytes=102400
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600

auto.create.topics.enable=true
offsets.topic.replication.factor=1
transaction.state.log.replication.factor=1
transaction.state.log.min.isr=1

Save and exit: Ctrl + O → Enter → Ctrl + X

3️⃣ Delete Old Logs (Optional / Clean Start)
rm -rf /tmp/kraft-combined-logs
4️⃣ Format Storage Directory (Only Once)
bin/kafka-storage.sh format -t $(bin/kafka-storage.sh random-uuid) -c config/kraft/broker.properties
5️⃣ Start Kafka Server
bin/kafka-server-start.sh config/kraft/broker.properties
6️⃣ Create a Topic (New Terminal)
cd /Users/ganeshpawar/Downloads/kafka
bin/kafka-topics.sh --create --topic first-topic --bootstrap-server localhost:9092
Check topic:
bin/kafka-topics.sh --list --bootstrap-server localhost:9092
7️⃣ Start Consumer (New Terminal)
cd /Users/ganeshpawar/Downloads/kafka
bin/kafka-console-consumer.sh --topic first-topic --from-beginning --bootstrap-server localhost:9092(This terminal will wait for messages.)
8️⃣ Start Producer (New Terminal)
cd /Users/ganeshpawar/Downloads/kafka
bin/kafka-console-producer.sh --topic first-topic --bootstrap-server localhost:9092
Type messages:
hello
kafka working fine
test message
You should immediately see them in the consumer terminal.
9️⃣ Useful Kafka Commands
List Topics
bin/kafka-topics.sh --list --bootstrap-server localhost:9092
Describe Topic
bin/kafka-topics.sh --describe --topic first-topic --bootstrap-server localhost:9092
Delete Topic
bin/kafka-topics.sh --delete --topic first-topic --bootstrap-server localhost:9092
Tips
Use new terminal windows/tabs for server, consumer, and producer.
For a clean start, always delete old logs:
rm -rf /tmp/kraft-combined-logs