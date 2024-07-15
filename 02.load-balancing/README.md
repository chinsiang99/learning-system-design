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

## How Load Balancer works?
Load balancers work by **distributing incoming network traffic** across multiple servers or resources to **ensure efficient utilization** of *computing resources* and *prevent overload*. Here are the **general steps** that a load balancer follows to distribute traffic:

1. The load balancer **receives a request** from a *client* or *user*.
2. The load balancer **evaluates the incoming request** and determines which server or resource should handle the request. This is done based on a **predefined load-balancing algorithm** that takes into account factors such as **server capacity**, **server response time**, **number of active connections**, and **geographic location**.
3. The load balancer **forwards the incoming traffic** to the *selected server* or *resource*.
4. The server or resource **processes the request** and sends a **response back** to the load balancer.
5. The load balancer **receives the response** from the server or resource and sends it to the *client* or *user* who made the request.

# Load Balancing Algorithms
A **load balancing algorithm** is a *method* used by a load balancer to distribute incoming traffic and requests among multiple servers or resources. The **primary purpose** of a load balancing algorithm is to **ensure efficient utilization** of available resources, improve overall **system performance**, and maintain **high availability** and **reliability**.

Load balancing algorithms help to **prevent any single server or resource from becoming overwhelmed**, which could lead to **performance degradation** or **failure**. By distributing the workload, load balancing algorithms can **optimize response times**, **maximize throughput**, and **enhance user experience**. These algorithms can consider factors such as **server capacity**, **active connections**, **response times**, and **server health**, among others, to make informed decisions on how to best distribute incoming requests.

Here are the most famous load balancing algorithms:

## 1. Round Robin
This algorithm distributes incoming requests to servers in a **cyclic order**. It assigns a request to the first server, then moves to the second, third, and so on, and after reaching the **last server**, it **starts again at the first**.

### Pros:

- Ensures an **equal distribution** of requests among the servers, as each server **gets a turn in a fixed order**.
- Easy to implement and understand.
- Works well when servers have similar capacities.

### Cons:

- **No Load Awareness**: **Does not** take into account the **current load** or **capacity** of each server. All servers are **treated equally** regardless of their current state.
- **No Session Affinity**: Subsequent requests from the **same client** may be directed to **different servers**, which can be problematic for stateful applications.
- **Performance Issues with Different Capacities**: May not perform optimally when servers have **different capacities** or **varying workloads**.
- **Predictable Distribution Pattern**: Round Robin is **predictable** in its **request distribution pattern**, which **could potentially** be *exploited* by attackers who can observe traffic patterns and might find vulnerabilities in specific servers by predicting which server will handle their requests.

### Use Cases
- **Homogeneous Environments**: Suitable for environments where all servers have **similar capacity and performance**.
- **Stateless Applications**: Works well for *stateless applications* where each **request** can be **handled independently**.

<div align="center">
  <img src="./round-robin.png" alt="round robin algo" />
</div>

## 2. Least Connections

The *Least Connections algorithm* is a **dynamic load balancing technique** that assigns incoming requests to the server with the **fewest active connections** at the time of the request. This method ensures a more balanced distribution of load across servers, especially in environments where traffic patterns are unpredictable and request processing times vary.

### Pros:

- **Load Awareness**: Takes into account the current load on each server by considering the **number of active connections**, leading to **better utilization** of server resources.
- **Dynamic Distribution**: **Adapts to changing traffic patterns** and **server loads**, **ensuring** no single server becomes a **bottleneck**.
- **Efficiency in Heterogeneous Environments**: Performs well when **servers have varying capacities** and **workloads**, as it **dynamically** allocates requests to **less busy servers**.

### Cons:

- **Higher Complexity**: More complex to implement compared to simpler algorithms like Round Robin, as it **requires real-time monitoring** of **active connections**.
- **State Maintenance**: Requires the load balancer to **maintain the state of active connections**, which can increase overhead.
- **Potential for Connection Spikes**: In scenarios where connection duration is short, servers can experience rapid spikes in connection counts, leading to frequent rebalancing.

### Use Cases
- **Heterogeneous Environments**: Suitable for environments where servers have **different capacities** and **workloads**, and the load needs to be dynamically distributed.
- **Variable Traffic Patterns**: Works well for applications with **unpredictable** or **highly variable traffic patterns**, ensuring that no single server is overwhelmed.
- **Stateful Applications**: Effective for applications where maintaining session state is important, as it helps distribute active sessions more evenly.

### Comparison to Round Robin
- **Round Robin**: Distributes requests in a **fixed**, **cyclic order** without considering the current load on each server.
- **Least Connections**: Distributes requests based on the **current load**, directing new requests to the server with the **fewest active connections**.

<div align="center">
  <img src="./least-connections.png" alt="least connections algo" />
</div>

## 3. Weighted Round Robin

*Weighted Round Robin* (WRR) is an enhanced version of the Round Robin load balancing algorithm. It **assigns weights** to **each server** based on their **capacity** or **performance**, distributing incoming requests **proportionally according to these weights**. This ensures that **more powerful servers** handle a **larger share of the load**, while **less powerful servers** handle a **smaller share**.

### Pros
- **Load Distribution According to Capacity**: Servers with higher capacities **handle more requests**, leading to **better utilization** of resources.
- **Flexibility**: Easily adjustable to accommodate changes in server capacities or additions of new servers.
- **Improved Performance**: Helps in **optimizing** overall system performance by **preventing overloading** of **less powerful servers**.

### Cons
- **Complexity in Weight Assignment**: **Determining appropriate weights** for each server can be **challenging** and requires **accurate performance metrics**.
- **Increased Overhead**: Managing and updating weights can introduce **additional overhead**, especially in **dynamic environments** where server performance fluctuates.
- **Not Ideal for Highly Variable Loads**: In environments with highly variable load patterns, WRR may not always provide optimal load balancing as it **doesn't consider real-time server load**.

### Use Cases
- **Heterogeneous Server Environments**: Ideal for environments where servers have **different processing capabilities**, ensuring efficient use of resources.
- **Scalable Web Applications**: Suitable for web applications where **different servers** may have **varying performance characteristics**.
- **Database Clusters**: Useful in database clusters where some nodes have **higher processing power** and can handle more queries

<div align="center">
  <img src="./weighted-round-robin.png" alt="weighted round robin algo" />
</div>

## 4. Weighted Least Connections
*Weighted Least Connections* is an **advanced load balancing algorithm** that combines the principles of the **Least Connections** and **Weighted Round Robin algorithms**. It takes into account both the **current load** (*number of active connections*) on each server and the **relative capacity of each server** (*weight*). This approach ensures that **more powerful servers** handle a **proportionally larger share of the load**, while also dynamically adjusting to the real-time load on each server.

### Pros
- **Dynamic Load Balancing**: Adjusts to the **real-time load** on each server, ensuring a more balanced distribution of requests.
- **Capacity Awareness**: Takes into account the **relative capacity of each server**, leading to **better utilization** of resources.
- **Flexibility**: Can handle environments with heterogeneous servers and variable load patterns effectively.

### Cons
- **Complexity**: **More complex** to implement compared to simpler algorithms like Round Robin and Least Connections.
- **State Maintenance**: Requires the load balancer to **keep track** of **both active connections** and **server weights**, increasing **overhead**.
- **Weight Assignment**: Determining appropriate weights for each server can be **challenging** and requires **accurate performance metrics**.

### Use Cases
- **Heterogeneous Server Environments**: Ideal for environments where servers have different processing capacities and workloads.
- **High Traffic Web Applications**: Suitable for web applications with **variable traffic patterns**, ensuring no single server becomes a bottleneck.
- **Database Clusters**: Useful in database clusters where nodes have varying performance capabilities and query loads.

<div align="center">
  <img src="./weighted-least-connection.png" alt="weighted least connection algo" />
</div>

## 5. IP Hash
IP Hash load balancing is a *technique* that assigns client requests to servers **based on the client's IP address**. The load balancer uses a **hash function** to **convert** the **client's IP address into a hash value**, which is then **used to determine** which *server* **should handle the request**. This method **ensures** that **requests from the same client IP address are consistently routed** to the *same server*, providing **session persistence**.

### Example
Suppose you have three servers (Server A, Server B, and Server C) and a client with the IP address 192.168.1.10. The load balancer applies a hash function to this IP address, resulting in a hash value. If the hash value is 2 and there are three servers, the load balancer routes the request to Server C (2 % 3 = 2).

### Pros
- **Session Persistence**: Ensures that **requests from the same client IP address** are consistently **routed to the same server**, which is beneficial for stateful applications.
- **Simplicity**: Easy to implement and **does not require** the load balancer to maintain the **state of connections**.
- **Deterministic**: **Predictable and consistent** routing based on the **client's IP address**.

### Cons
- **Uneven Distribution**: If client IP addresses are not **evenly distributed**, some servers **may receive more requests** than others, leading to an **uneven load**.
- **Dynamic Changes**: **Adding** or **removing** servers can **disrupt the hash mapping**, causing some clients to be routed to different servers.
- **Limited Flexibility**: **Does not take into account** the **current load** or **capacity** of servers, which can lead to **inefficiencies**.

### Use Cases
- **Stateful Applications**: Ideal for *applications* where **maintaining session persistence is important**, such as online shopping carts or user sessions.
- **Geographically Distributed Clients**: Useful when clients are **distributed across different regions** and **consistent routing** is required.

<div align="center">
  <img src="./ip-hashing.png" alt="ip hashing algo" />
</div>

## 6. Least Response Time
Least Response Time load balancing is a **dynamic algorithm** that **assigns incoming requests to the server** with the **lowest response time**, ensuring efficient utilization of server resources and optimal client experience. This approach aims to **direct traffic** to the server that **can handle the request the fastest**, based on **recent performance metrics**.

### How Least Response Time Load Balancing Works
- **Monitor Response Times**: The load balancer **continuously monitors** the **response times of each server**. Response time is typically measured from when a request is sent to a server until a response is received.
- **Assign Requests**: When a new request arrives, the load balancer **assigns it** to the server **with the lowest average response time**.
- **Dynamic Adjustment**: The load balancer dynamically adjusts the assignment of requests **based on real-time performance data**, ensuring that the fastest server handles the next request.

### Pros
- **Optimized Performance**: Ensures that requests are handled by the **fastest available server**, leading to **reduced latency** and **improved client experience**.
- **Dynamic Load Balancing**: **Continuously adjusts** to **changing server performance**, ensuring optimal distribution of load.
- **Effective Resource Utilization**: Helps in **better utilization** of server resources by directing traffic to servers that can respond quickly.

### Cons
- **Complexity**: **More complex** to implement compared to simpler algorithms like Round Robin, as it **requires continuous monitoring** of server performance.
- **Overhead**: Monitoring response times and dynamically adjusting the load can introduce **additional overhead**.
- **Short-Term Variability**: Response times can vary in the short term due to network fluctuations or transient server issues, potentially causing frequent rebalancing.

### Use Cases
- **Real-Time Applications**: Ideal for applications where **low latency** and **fast response times** are critical, such as online gaming, video streaming, or financial trading platforms.
- **Web Services**: Useful for web services and APIs that need to provide **quick responses** to **user requests**.
- **Dynamic Environments**: Suitable for environments with **fluctuating loads** and **varying server performance**.

<div align="center">
  <img src="./least-response.png" alt="least response algo" />
</div>

## 7. Random
Random load balancing is a simple algorithm that distributes incoming requests to servers **randomly**. Instead of following a fixed sequence or using performance metrics, the load balancer selects a server at random to handle each request. This method can be effective in scenarios where the **load** is **relatively uniform** and **servers have similar capacities**.

Suppose you have three servers: Server A, Server B, and Server C. When a new request arrives, the load balancer randomly chooses one of these servers to handle the request. Over time, if the randomness is uniform, each server should receive approximately the same number of requests.

### Pros
- **Simplicity**: Very easy to implement and understand, requiring **minimal configuration**.
- **No State Maintenance**: The load balancer **does not** need to *track* the **state or performance of servers**, reducing overhead.
- **Uniform Distribution Over Time**: **If the random selection is uniform**, the load will be evenly distributed across servers over a long period.

### Cons
- **No Load Awareness**: **Does not consider** the **current load** or **capacity** of servers, which can lead to uneven distribution if server performance varies.
- **Potential for Imbalance**: In the short term, random selection can lead to an uneven distribution of requests.
- **No Session Affinity**: Requests from the same client may be directed to **different servers**, which can be **problematic for stateful applications**.
- **Security systems** that rely on detecting anomalies (e.g., to mitigate DDoS attacks) might find it slightly more challenging to identify malicious patterns **if a Random algorithm is used**, due to the **inherent unpredictability in request distribution**. This could potentially dilute the visibility of attack patterns.

### Use Cases
- **Homogeneous Environments**: Suitable for environments where servers have **similar capacity** and **performance**.
- **Stateless Applications**: Works well for stateless applications where each request can be **handled independently**.
- **Simple Deployments**: Ideal for simple deployments where the complexity of other load balancing algorithms is not justified.

<div align="center">
  <img src="./random.png" alt="random algo" />
</div>

## 8. Least Bandwidth
The Least Bandwidth load balancing algorithm **distributes incoming requests** to servers **based on the current bandwidth usage**. It routes each new request to the server that is **consuming the least amount of bandwidth at the time**. This approach helps in balancing the network load more efficiently by ensuring that no single server gets overwhelmed with too much data traffic.

### Pros
- **Dynamic Load Balancing**: Continuously adjusts to the current network load, ensuring optimal distribution of traffic.
- **Prevents Overloading**: Helps in preventing any single server from being overwhelmed with too much data traffic, leading to better performance and stability.
- **Efficient Resource Utilization**: Ensures that all servers are utilized more effectively by balancing the bandwidth usage.

### Cons
- **Complexity**: **More complex** to implement compared to simpler algorithms like Round Robin, as it requires continuous **monitoring of bandwidth usage**.
- **Overhead**: **Monitoring bandwidth** and **dynamically adjusting** the load can introduce **additional overhead**.
- **Short-Term Variability**: Bandwidth usage can fluctuate in the short term, potentially causing frequent rebalancing.

### Use Cases
- **High Bandwidth Applications**: Ideal for applications with **high bandwidth usage**, such as **video streaming**, **file downloads**, and **large data transfers**.
- **Content Delivery Networks (CDNs)**: Useful for CDNs that need to balance traffic efficiently to deliver content quickly.
- **Real-Time Applications**: Suitable for real-time applications where **maintaining low latency** is **critical**.

<div align="center">
  <img src="./least-bandwidth.png" alt="random algo" />
</div>