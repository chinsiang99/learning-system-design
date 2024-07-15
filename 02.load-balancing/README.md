# Introduction to Load Balancing

Load balancing is a **crucial component** of *System Design*, as it helps **distribute incoming requests** and **traffic** evenly across **multiple servers**. The **main goal** of load balancing is to **ensure high availability**, **reliability**, and **performance** by *avoiding* **overloading** a single server and *avoiding* **downtime**.

Typically a load balancer sits between the client and the server accepting incoming network and application traffic and distributing the traffic across multiple backend servers using various algorithms. By balancing application requests across multiple servers, a load balancer **reduces the load on individual servers** and **prevents any one server from becoming a single point of failure**, thus *improving* overall application **availability** and **responsiveness**.

To *utilize* **full scalability** and **redundancy**, we can try to balance the load at **each layer of the system**. We can add LBs at **three places**:

1. Between the *user* and the *web server*
2. Between *web servers* and an *internal platform layer*, like **application servers** or **cache servers**
3. Between *internal platform layer* and *database*.

<div align="center">
  <img src="./sample-load-balancing.png" alt="sample load balancing" />
</div>