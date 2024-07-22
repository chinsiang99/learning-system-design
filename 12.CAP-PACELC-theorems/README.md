# Introduction to CAP Theorem
The **CAP theorem**, also known as **Brewer's theorem**, is a fundamental concept in distributed systems design. It was introduced by Eric Brewer in 2000. The CAP theorem provides a framework for understanding the trade-offs between three essential properties of distributed systems: **consistency**, **availability**, and **partition tolerance**.

## a. Background and history
Before the introduction of the CAP theorem, distributed systems were primarily designed with a focus on consistency and availability, often ignoring partition tolerance. However, as distributed systems grew in scale and complexity, it became evident that addressing network partitions was crucial for ensuring reliable and fault-tolerant operation.

## b. Overview of the CAP theorem
The CAP theorem states that **it is impossible for a distributed system to simultaneously provide all three properties**: *consistency*, *availability*, and *partition tolerance*. In other words, a distributed system **can only guarantee two out of these three properties** at any given time. The theorem highlights the inherent trade-offs that system designers must consider when building distributed systems.

- Consistency: A system is considered consistent if all nodes see the same data at the same time. This means that any read operation should return the most recent write operation's result, ensuring that the system maintains a single, up-to-date version of the data.

- Availability: A system is considered highly available if it continues to operate and respond to requests despite failures, ensuring that every request receives a response, either a success or an error.

- Partition Tolerance: A system is considered partition-tolerant if it can continue to operate and maintain its guarantees despite network partitions, which are situations where communication between nodes in the system is interrupted or lost.

The CAP theorem provides a useful guideline for understanding the limitations of distributed systems and making informed design decisions that balance the needs for consistency, availability, and partition tolerance.

<div align="center">
  <img src="./cap-theorem.png" alt="cap-theorem" />
</div>

# Components of CAP Theorem
The CAP theorem revolves around three key properties of distributed systems: *Consistency*, *Availability*, and *Partition Tolerance*. Each of these properties plays a vital role in determining the behavior of a distributed system under various conditions.

## a. Consistency
Consistency in distributed systems refers to the degree to which the system maintains a single, up-to-date version of the data. There are different levels of consistency, depending on the requirements of the system.

- Strong consistency: In a strongly consistent system, **all nodes see the same data at the same time**. Any read operation returns the most recent write operation's result, ensuring that the system maintains a single, coherent version of the data. Strong consistency is desirable for applications that require accurate and up-to-date information at all times, such as financial transactions or inventory management systems.

- Eventual consistency: In an eventually consistent system, **nodes may temporarily have different versions of the data**, but they **will eventually converge to the same, consistent state**. Eventual consistency is suitable for applications where slight inconsistencies can be tolerated for short periods, such as social media updates or user profiles. This model offers better availability and performance compared to strong consistency, at the cost of temporary data inconsistencies.

## b. Availability
Availability refers to the **ability of a distributed system to continue operating and responding to requests despite failures or partial outages**. Highly available systems ensure that every request receives a response, either a success or an error, without significant delays.

- High availability: High availability is achieved by replicating data across multiple nodes and designing the system to handle failures gracefully. In a highly available system, the loss of individual nodes does not cause a significant impact on the overall operation, as other nodes can continue to serve requests.

## c. Partition Tolerance
Partition tolerance is a critical property of distributed systems, as it determines the system's ability to handle network partitions and communication failures.

- Network partitioning: In a distributed system, nodes communicate with each other over a network. Network partitions occur when communication between some or all nodes is interrupted or lost. This can be caused by various reasons, such as hardware failures, network congestion, or configuration issues.

- Handling partition failures: Partition-tolerant systems are designed to handle network partitions gracefully and continue to operate without compromising their guarantees. This often involves strategies such as data replication, fallback mechanisms, and automatic recovery processes. However, as the CAP theorem states, it is impossible to guarantee consistency, availability, and partition tolerance simultaneously, so system designers must make trade-offs based on the specific requirements of their application.