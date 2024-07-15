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

## Key terminology and concepts
1. **Load Balancer**: A *device* or *software* that **distributes network traffic** across **multiple servers** based on **predefined rules or algorithms**
2. **Backend Servers**: The servers that **receive** and **process** requests **forwarded** by the *load balancer*. Also referred to as *server pool* or *server fam*
3. **Load Balancing Algorithm**: The **method** used by the load balancer to **determine how to distribute incoming traffic** among the backend servers.
4. **Health Checks**: **Periodic tests** performed by the *load balancer* to **determine the availability** and **performance** of backend servers. *Unhealthy servers* are **removed** from the server pool **until they recover**.
5. **Session Persistence**: A technique **used to ensure that subsequent requests from the same client are directed to the same backend server**, maintaining session state and providing a consistent user experience.
6. **SSL/TLS Termination**: The *process* of **decrypting SSL/TLS-encrypted traffic at the load balancer level**, **offloading** the *decryption burden* from *backend servers* and allowing for **centralized SSL/TLS management**.