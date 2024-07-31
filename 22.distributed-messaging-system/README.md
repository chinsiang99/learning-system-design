# Introduction to Messaging System

## Background
**One of the common challenges among distributed systems is handling a continuous influx of data from multiple sources**. Imagine a log aggregation service that is receiving hundreds of log entries per second from different sources. The function of this log aggregation service is to store these logs on disk at a shared server and also build an index so that the logs can be searched later. A few challenges of this service are:

- How will the log aggregation service handle a spike of messages? If the service can handle (or buffer) 500 messages per second, what will happen if it starts receiving a higher number of messages per second? If we decide to have multiple instances of the log aggregation service, how do we divide the work among these instances?
- How can we receive messages from different types of sources? The sources producing (or consuming) these logs need to decide upon a common protocol and data format to send log messages to the log aggregation service. This leads us to a strongly coupled architecture between the producer and consumer of the log messages.
- What will happen to the log messages if the log aggregation service is down or unresponsive for some time?

**To efficiently manage such scenarios, distributed systems depend upon a messaging system**.

## What is a messaging system?
A messaging system is **responsible for transferring data among services, applications, processes, or servers**. Such a system helps decouple different parts of a distributed system by providing an **asynchronous way of transferring messaging between the sender and the receiver**. Hence, all senders (or producers) and receivers (or consumers) focus on the data/message without worrying about the mechanism used to share the data.

<div align="center">
  <img src="./messaging.png" alt="messaging" />
</div>

There are two common ways to handle messages: Queuing and Publish-Subscribe.

## Queue
In the queuing model, messages are **stored sequentially in a queue**. **Producers push messages to the rear of the queue**, and **consumers extract the messages from the front of the queue**.

<div align="center">
  <img src="./queue.png" alt="queue" />
</div>

A **particular message can be consumed by a maximum of one consumer only**. Once a consumer grabs a message, it is removed from the queue such that the next consumer will get the next message. This is a great model for distributing message-processing among multiple consumers. But this also **limits the system as multiple consumers cannot read the same message from the queue**. 

<div align="center">
  <img src="./queue-message-consumption.png" alt="queue-message-consumption" />
</div>

## Publish-subscribe messaging system
In the pub-sub (short for publish-subscribe) model, **messages are divided into topics**. A publisher (or a producer) **sends a message to a topic that gets stored in the messaging system under that topic**. Subscribers (or the consumer) **subscribe to a topic to receive every message published to that topic**. Unlike the Queuing model, the pub-sub model **allows multiple consumers to get the same message**; **if two consumers subscribe to the same topic, they will receive all messages published to that topic**.

<div align="center">
  <img src="./pub-sub.png" alt="pub-sub" />
</div>

## Message Broker

The messaging system that stores and maintains the messages is commonly known as the **message broker**. It provides a loose coupling between publishers and subscribers, or producers and consumers of data.

<div align="center">
  <img src="./message-broker.png" alt="message-broker" />
</div>

The message broker stores published messages in a queue, and subscribers read them from the queue. Hence, subscribers and publishers do not have to be synchronized. This loose coupling enables subscribers and publishers to read and write messages at different rates.

The messaging system's ability to store messages **provides fault-tolerance, so messages do not get lost between the time they are produced and the time they are consumed**.

To summarize, a message system is deployed in an application stack for the following reasons:

1. Messaging buffering: To provide a **buffering mechanism in front of processing** (i.e., to deal with temporary incoming message spikes that are greater than what the processing app can deal with). This enables the system to **safely deal with spikes in workloads by temporarily storing data until it is ready for processing**.

2. Guarantee of message delivery: Allows producers to publish messages with **assurance that the message will eventually be delivered if the consuming application is unable to receive the message when it is published**.

3. Providing abstraction: Distributed messaging systems **enable decoupling of sender and receiver components in a system**, allowing them to **evolve independently**. This architectural pattern promotes modularity, making it easier to maintain and update individual components without affecting the entire system.

4. Scalability: Distributed messaging systems can handle a large number of messages and can scale horizontally to accommodate increasing workloads. This allows applications to grow and manage higher loads without significant performance degradation.

5. Fault Tolerance: By distributing messages across multiple nodes or servers, these systems can continue to operate even if a single node fails. This redundancy provides increased reliability and ensures that messages are not lost during system failures.

5. Asynchronous Communication: These systems **enable asynchronous communication between components**, allowing them to process messages at their own pace without waiting for immediate responses. This can improve overall system performance and responsiveness, particularly in scenarios with high latency or variable processing times.

6. Load Balancing: Distributed messaging systems can automatically distribute messages across multiple nodes, ensuring that no single node becomes a bottleneck. This allows for better resource utilization and improved overall performance.

7. Message Persistence: Many distributed messaging systems provide message persistence, ensuring that **messages are not lost if a receiver is temporarily unavailable or slow to process messages**. This feature helps maintain data consistency and reliability across the system.

8. Security: Distributed messaging systems often support various security mechanisms, such as encryption and authentication, to protect sensitive data and prevent unauthorized access.

9. Interoperability: These systems often support multiple messaging protocols and can integrate with various platforms and technologies, making it easier to connect different components within a complex system.


# What is Kafka?
Apache Kafka is an **open-source publish-subscribe-based messaging system**. It is distributed, durable, fault-tolerant, and highly scalable by design. Fundamentally, it is **a system that takes streams of messages from applications known as producers**, **stores them reliably on a central cluster** (containing a set of brokers), and **allows those messages to be received by applications** (known as consumers) that process the messages.

<div align="center">
  <img src="./kafka.png" alt="kafka" />
</div>

## Background
Kafka was created at LinkedIn around 2010 to track various events, such as page views, messages from the messaging system, and logs from various services. Later, it was made open-source and developed into a comprehensive system which is used for:

1. Reliably storing a huge amount of data.
2. Enabling high throughput of message transfer between different entities.
3. Streaming real-time data.

At a high level, we can call Kafka a **distributed Commit Log**. A Commit Log (also known as a Write-Ahead log or a Transactions log) is an **append-only data structure that can persistently store a sequence of records**. Records are always appended to the end of the log, and once added, **records cannot be deleted or modified**. Reading from a commit log always happens from left to right (or old to new).

Kafka stores all of its messages on disk. Since all reads and writes happen in sequence, Kafka takes advantage of sequential disk reads (more on this later).

<div align="center">
  <img src="./kafka-sample.png" alt="kafka-sample" />
</div>

## Kafka use cases
Kafka can be used for collecting big data and real-time analysis. Here are some of its top use cases:

1. Metrics: Kafka can be used to collect and aggregate monitoring data. Distributed services can push different operational metrics to Kafka servers. These metrics can then be pulled from Kafka to produce aggregated statistics.
2. Log Aggregation: Kafka can be used to collect logs from multiple sources and make them available in a standard format to multiple consumers.
3. Stream processing: Kafka is quite useful for use cases where the collected data undergoes processing at multiple stages. For example, the raw data consumed from a topic is transformed, enriched, or aggregated and pushed to a new topic for further consumption. This way of data processing is known as stream processing.
4. Commit Log: Kafka can be used as an external commit log for any distributed system. Distributed services can log their transactions to Kafka to keep track of what is happening. This transaction data can be used for replication between nodes and also becomes very useful for disaster recovery, for example, to help failed nodes to recover their states.
5. Website activity tracking: One of Kafka's original use cases was to build a user activity tracking pipeline. User activities like page clicks, searches, etc., are published to Kafka into separate topics. These topics are available for subscription for a range of use cases, including real-time processing, real-time monitoring, or loading into Hadoop or data warehousing systems for offline processing and reporting.
6. Product suggestions: Imagine an online shopping site like amazon.com, which offers a feature of 'similar products' to suggest lookalike products that a customer could be interested in buying. To make this work, we can track every consumer action, like search queries, product clicks, time spent on any product, etc., and record these activities in Kafka. Then, a consumer application can read these messages to find correlated products that can be shown to the customer in real-time. Alternatively, since all data is persistent in Kafka, a batch job can run overnight on the 'similar product' information gathered by the system, generating an email for the customer with product suggestions.

## Kafka common terms

Before digging deep into Kafka's architecture, let's first go through some of its common terms.

### Brokers
A **Kafka server is also called a broker**. Brokers are **responsible for reliably storing data provided by the producers and making it available to the consumers**.

### Records
A record is **a message or an event that gets stored in Kafka**. Essentially, it is the data that travels from producer to consumer through Kafka. A record contains a *key*, a *value*, a *timestamp*, and *optional metadata headers*.

<div align="center">
  <img src="./kafka-message.png" alt="kafka-message" />
</div>

### Topics
Kafka **divides its messages into categories called Topics**. In simple terms, a **topic is like a table in a database**, and the **messages are the rows in that table**.

- Each message that Kafka receives from a *producer* is **associated with a topic**.
- Consumers can **subscribe to a topic** to get *notified* when new messages are added to that topic.
- A **topic can have multiple subscribers** that read messages from it.
- In a Kafka cluster, a **topic is identified by its name and must be unique**.

**Messages in a topic can be read as often as needed** — unlike traditional messaging systems, **messages are not deleted after consumption**. Instead, **Kafka retains messages for a configurable amount of time** or **until a storage size is exceeded**. Kafka's performance is effectively constant with respect to data size, so storing data for a long time is perfectly fine.

<div align="center">
  <img src="./kafka-topics.png" alt="kafka-topics" />
</div>

### Producers
Producers are **applications** that **publish (or write) records to Kafka**.

### Consumers
Consumers are the **applications** that **subscribe to (read and process) data from Kafka topics**. Consumers **subscribe to one or more topics and consume published messages by pulling data from the brokers**.

In Kafka, **producers and consumers are fully decoupled** and agnostic of each other, which is a key design element to achieve the high scalability that Kafka is known for. For example, **producers never need to wait for consumers**.

### High-level architecture
At a high level, applications (producers) send messages to a Kafka broker, and these messages are read by other applications called consumers. Messages get stored in a topic, and consumers subscribe to the topic to receive new messages.

### Kafka cluster
Kafka is deployed as a cluster of one or more servers, where each server is responsible for running one Kafka broker.

### ZooKeeper
ZooKeeper is a **distributed key-value store** and is used for **coordination and storing configurations**. It is highly optimized for reads. **Kafka uses ZooKeeper to coordinate between Kafka brokers**; ZooKeeper **maintains metadata information about the Kafka cluster**. We will be looking into this in detail later.

<div align="center">
  <img src="./high-architecture-kafka.png" alt="high-architecture-kafka" />
</div>