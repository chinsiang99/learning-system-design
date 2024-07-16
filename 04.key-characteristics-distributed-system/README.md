# Scalability
*Scalability* is the **ability of a system to handle an increasing workload**, either by **adding more resources** (*scaling out*) or by **upgrading the capacity of existing resources** (*scaling up*). In distributed systems, scalability is essential to **ensure that the system can effectively manage the growing demands of users**, **data**, and **processing power**. Here's an overview of the different aspects of scalability:

## 1. Horizontal Scaling
*Horizontal scaling*, also known as **scaling out**, involves **adding more machines** or **nodes** to a system to distribute the workload evenly. This approach allows the system to handle an increased number of requests without overloading individual nodes. Horizontal scaling is particularly useful in distributed systems because it provides a cost-effective way to manage fluctuating workloads and maintain high availability.

## 2. Vertical Scaling
*Vertical scaling*, or **scaling up**, refers to **increasing the capacity** of individual nodes within a system. This can be achieved by **upgrading the hardware**, such as adding more *CPU*, *memory*, or *storage*. Vertical scaling can help improve the performance of a system by allowing it to handle more workloads on a single node. However, this approach has limitations, as there is a physical limit to the amount of resources that can be added to a single machine, and it can also lead to single points of failure.

## Horizontal vs. Vertical Scaling

With **horizontal-scaling** it is often easier to **scale dynamically** by adding more machines into the existing pool; **Vertical-scaling** is usually **limited to the capacity of a single server** and scaling beyond that capacity often involves **downtime** and **comes with an upper limit**.

Good examples of horizontal scaling are Cassandra and MongoDB as they both provide an easy way to scale horizontally by adding more machines to meet growing needs. Similarly, a good example of vertical scaling is MySQL as it allows for an easy way to scale vertically by switching from smaller to bigger machines. However, this process often involves downtime.

<div align="center">
  <img src="./scaling.png" alt="scaling" />
</div>