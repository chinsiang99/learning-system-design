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