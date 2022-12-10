Kafka + Spark Streaming + PySpark

1.Introduction
Real-time data ingesting is a common problem in real-time analytics, because in a platform such as e-commerce, active users in a given time and the number of events created by each active user are many. Hence, recommendations (i.e., predictions) for each event or groups of events are expected to be near real-time.

Apache Kafka addresses the first two problems stated above. It is a distributed streaming platform, which helps to build real-time streaming data pipelines.

In this project, we want use kafka and Spark Streaming to work together.

2. Steps

  Discuss the steps to perform to setup Apache Spark in a Linux environment.
  Starting Kafka (for more details, please refer to this article).
  Creating a PySpark app for consume and process the events and write back to Kafka.
  Steps to produce and consume events using Kafka-Python.

3. Environment install

1.Create, Configure and Launch a Google Cloud Dataproc cluster.

![image](https://user-images.githubusercontent.com/68774929/206847433-e98a9382-0d7d-4647-9b64-af6e2e9ced0f.png)


2.Connecting to the Master Node using Secure Shell (ssh)

![image](https://user-images.githubusercontent.com/68774929/206847618-197278c1-7a46-4986-a016-d26640855303.png)


Setup Kafka
Step 1. Download kafka

which is available at https://kafka.apache.org/downloads

    $ wget https://downloads.apache.org/kafka/3.3.1/kafka_2.12-3.3.1.tgz
    $ tar -xvf kafka_2.12-3.3.1.tgz
    
![image](https://user-images.githubusercontent.com/68774929/206847903-e832cf10-f6e8-4061-9d29-3e57344fe5fd.png)


Setup Spark
    $ pip3 install msgpack
    $ pip3 install kafka-python
    
![image](https://user-images.githubusercontent.com/68774929/206848146-213fb9ba-af3d-4b0a-b180-c2b41e139058.png)


4. Check kafka is working, use input_event topic as example

![image](https://user-images.githubusercontent.com/68774929/206848440-f67aa13d-86d8-4c1e-9600-81b346e0aa8b.png)

Step 1. Start Kafka Zookeeper (Keep this terminal open: terminal 1)

    $ cd kafka_2.12-3.3.1/
    $ bin/zookeeper-server-start.sh config/zookeeper.properties
    


Step 2. Start Kafka broker(Keep this terminal open: terminal 2)

    $ cd kafka_2.12-3.3.1/
    $ bin/kafka-server-start.sh config/server.properties
    
![image](https://user-images.githubusercontent.com/68774929/206848869-b3c3705d-9e6b-4bb2-8ec3-92d3695c1d27.png)


Step 3: Create one Kafka Topics (input_event)

    $ cd kafka_2.12-3.3.1/
    $ bin/kafka-topics.sh --create --topic input_event --bootstrap-server localhost:9092 --partitions 3 --replication-factor 1
    
    
 ![image](https://user-images.githubusercontent.com/68774929/206848964-762f1bbe-2bdc-4dea-a1e0-a9a3d140691d.png)
 
 
 
 Step 4: Create consumer.py, then run it (terminal 3)

    $ vi consumer.py
    $ python3 consumer.py
    from kafka import KafkaConsumer

    consumer = KafkaConsumer('input_event', bootstrap_servers=['localhost:9092'])
    for msg in consumer:
        print(msg)

Step 5: Create producer.py, then run it(terminal 4)

    $ vi producer.py
    $ python3 producer.py
    from kafka import KafkaProducer
    
    
    producer = KafkaProducer(bootstrap_servers='localhost:9092')
    producer.send('input_event', b'(1, Main Menu), (2, Phone), (3, Smart Phone), (4, iPhone)')
    producer.close()

Step 6: Result


5. Implement Kafka + Spark Streaming + PySpark

Step 1: In terminal 1(Start Kafka Zookeeper):

    $ cd kafka_2.12-3.3.1/
    $ bin/zookeeper-server-start.sh config/zookeeper.properties
Step 2: In terminal 2(Start Kafka broker):

    $ cd kafka_2.12-3.3.1/
    $ bin/kafka-server-start.sh config/server.properties
Step 3: Create two Kafka Topics (input_event and output_event)

    $ cd kafka_2.12-3.3.1/
    $ bin/kafka-topics.sh --create --topic input_event --bootstrap-server localhost:9092 --partitions 3 --replication-factor 1
    $ bin/kafka-topics.sh --create --topic output_event --bootstrap-server localhost:9092 --partitions 3 --replication-factor 1
Now, we have two topic: input_event, output_event

Step 4: In terminal 3, create consumer.py, then run it:

    $ vi consumer.py
    $ python3 consumer.py

from kafka import KafkaConsumer

consumer = KafkaConsumer('output_event', bootstrap_servers=['localhost:9092'])
for msg in consumer:
    print(msg)
Step 5: In terminal 4, create producer.py, then run it:

    $ vi producer.py
    $ python3 producer.py

from kafka import KafkaProducer

producer = KafkaProducer(bootstrap_servers='localhost:9092', value_serializer=str.encode, key_serializer=str.encode)
event_stream_key = 'product_list'
event_stream_value = 'product1 product2 product3 product1'
producer.send('input_event', key = event_stream_key, value = event_stream_value)
In terminal 5, running spark_processor.py

spark_processor.py will process events and write back to Kafka: 1.consume the message from input_event topic 2.process the data 3.push the message to output_event topic.



    $ spark-submit --packages org.apache.spark:spark-streaming-kafka-0-10_2.12:3.1.3,org.apache.spark:spark-sql-kafka-0-10_2.12:3.1.3 --deploy-mode client spark_processor.py


6.Analyse
Now, we have two method:

install 2.* version spark to run the program. It is not working
Change the spark_processor.py code to receiving data from kafka. https://spark.apache.org/docs/latest/structured-streaming-kafka-integration.html
Then I try the second method, it still have some problem, I can't receive the data from kafka.
