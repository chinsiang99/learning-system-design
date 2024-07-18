# Introduction to Caching

## What is Caching?
The cache is a **high-speed storage layer** that sits *between* the **application** and the **original source of the data**, such as a database, a file system, or a remote web service. When data is requested by the application, it is first checked in the cache. If the data is found in the cache, it is returned to the application. If the data is not found in the cache, it is retrieved from its original source, stored in the cache for future use, and returned to the application.

Caching can be used for various types of data, such as web pages, database queries, API responses, images, and videos. The goal of caching is to **reduce the number of times data needs to be fetched from its original source**, which can result in **faster processing** and **reduced latency**.

Caching can be implemented in various ways, including **in-memory caching**, **disk caching**, **database caching**, and **CDN caching**. *In-memory caching* stores data in the **main memory** of the computer, which is **faster to access than disk storage**. *Disk caching* stores data on the **hard disk**, which is **slower than main memory but faster than retrieving data from a remote source**. *Database caching* stores frequently accessed data in the **database** itself, **reducing the need to access external storage**. *CDN caching* stores data on a **distributed network of servers**, reducing the latency of accessing data from remote locations.

## Key terminology and concepts
### 1. Cache: A **temporary storage location** for data or computation results, typically designed for **fast access and retrieval**.

### 2. Cache hit: When a requested data item or computation result is **found** in the cache.

### 3. Cache miss: When a requested data item or computation result is **not found** in the cache and needs to be fetched from the original data source or recalculated.

### 4. Cache eviction: The process of **removing** data from the cache, typically to make room for new data or based on a predefined cache eviction policy.

### 5. Cache staleness: When the data in the cache is **outdated** compared to the original data source.

# Why is Caching Important?
Caching plays a critical role in i**mproving system performance** and **user experience** in software engineering. By storing frequently accessed data in a cache, applications can **reduce the response time** and **latency** of operations, resulting in faster and more efficient processing. Here are some reasons why caching is important:

## 1. Reduced latency
By serving data from the cache, which is typically faster to access than the original data source, caching can **significantly reduce the time** it takes to **retrieve the data**.

## 2. Improved system performance
Caching can **significantly improve the performance** of an application by **reducing the number of times data needs to be fetched** from its **original source**. Since cached data can be retrieved faster than from the original source, this results in a significant reduction in processing time, which leads to a more responsive application.

## 3. Reduced network load
Caching can also **reduce network load** by **minimizing the amount of data that needs to be transmitted over the network**. Since cached data is stored locally, there is no need to fetch data from the original source, **reducing the amount of data that needs to be transferred over the network**.

## 4. Increased scalability
Caching can **improve** the **scalability of an application** by **reducing the load on the original source**. By storing frequently accessed data in a cache, the original source is less likely to be overwhelmed with requests, making it more scalable.

## 5. Better user experience
Faster response times and **reduced latency** can lead to a better user experience. Applications that load quickly and respond to user requests in a timely manner are more likely to be used and preferred by users.

# Types of Caching
Caching can be implemented in various ways, depending on the specific use case and the type of data being cached. Here are some of the most common types of caching:

<div align="center">
  <img src="./caching-type.png" alt="caching type" />
</div>

## 1. In-memory caching
In-memory caching stores data in the **main memory of the computer**, which is faster to access than disk storage. In-memory caching is useful for frequently accessed data that can fit into the available memory. This type of caching is commonly used for caching API responses, session data, and web page fragments. To implement in-memory caching, software engineers can use various techniques, including using a cache library like **Memcached or Redis**, or implementing custom caching logic within the application code.

## 2. Disk caching
Disk caching stores data on the hard disk, which is slower than main memory but faster than retrieving data from a remote source. Disk caching is **useful for data that is too large to fit in memory** or for data that **needs to persist between application restarts**. This type of caching is commonly used for caching database queries and file system data.

## 3. Database caching
Database caching stores frequently accessed data in the database itself, reducing the need to access external storage. This type of caching is useful for data that is stored in a database and frequently accessed by multiple users. Database caching can be implemented using a variety of techniques, including database query caching and result set caching.

## 4. Client-side caching
This type of caching occurs on the client device, such as a web browser or mobile app. Client-side caching stores frequently accessed data, such as images, CSS, or JavaScript files, to reduce the need for repeated requests to the server. Examples of client-side caching include **browser caching and local storage**.

## 5. Server-side caching
This type of caching occurs on the server, typically in web applications or other backend systems. Server-side caching can be used to store frequently accessed data, precomputed results, or intermediate processing results to improve the performance of the server. Examples of server-side caching include **full-page caching**, **fragment caching**, and **object caching**.

## 6. CDN caching
CDN caching stores data on a distributed network of servers, reducing the latency of accessing data from remote locations. This type of caching is useful for data that is accessed from multiple locations around the world, such as **images, videos, and other static assets**. CDN caching is commonly used for content delivery networks and large-scale web applications.

## 7. DNS caching
DNS cache is a type of cache used in the Domain Name System (DNS) to store the results of DNS queries for a period of time. When a user requests to access a website, their computer sends a DNS query to a DNS server to resolve the website’s domain name to an IP address. The DNS server responds with the IP address, and the user’s computer can then access the website using the IP address. DNS caching improves the performance of the DNS system by reducing the number of requests made to DNS servers. When a DNS server receives a request for a domain name, it checks its local cache to see if it has the IP address for that domain name. If the IP address is in the cache, the DNS server can immediately respond with the IP address without having to query other servers. This can significantly reduce the response time for DNS queries and improve the overall performance of the system.

<div align="center">
  <img src="./how-to-use-cache.png" alt="what and where to cache" />
</div>

# Cache Replacement Policies
When implementing caching, it’s important to have a cache replacement policy to determine which items in the cache should be removed when the cache becomes full. Here are some of the most common cache replacement policies:

## 1. Least Recently Used (LRU)
LRU is a cache replacement policy that **removes the least recently used** item from the cache when it becomes full. This policy assumes that items that have been accessed more recently are more likely to be accessed again in the future.

## 2. Least Frequently Used (LFU)
LFU is a cache replacement policy that **removes the least frequently used** item from the cache when it becomes full. This policy assumes that items that have been accessed more frequently are more likely to be accessed again in the future.

## 3. First In, First Out (FIFO)
FIFO is a cache replacement policy that **removes the oldest item from the cache** when it becomes full. This policy assumes that the oldest items in the cache are the least likely to be accessed again in the future.

## 4. Random Replacement
Random replacement is a cache replacement policy that **removes a random item** from the cache when it becomes full. This policy doesn’t make any assumptions about the likelihood of future access and can be useful when the **access pattern is unpredictable**.

## Comparison of different replacement policies
Each cache replacement policy has its **advantages** and **disadvantages**, and the best policy to use depends on the specific use case. LRU and LFU are generally more effective than FIFO and random replacement since they take into account the access pattern of the cache. However, LRU and LFU can be more expensive to implement since they require maintaining additional data structures to track access patterns. FIFO and random replacement are simpler to implement but may not be as effective in optimizing cache performance. Overall, the cache replacement policy used should be chosen carefully to balance the **trade-off** between **performance** and **complexity**.

# Cache Invalidation
## Cache Invalidation Strategies
While caching is fantastic, it requires some maintenance to keep the cache **coherent** with the source of truth (e.g., database). If the **data is modified in the database**, it **should be invalidated** in the cache; if not, this **can cause inconsistent application behavior**.

Solving this problem is known as **cache invalidation**; there are **four main schemes** that are used:

### 1. Write-through cache
Under this scheme, data is written into the cache and the corresponding database simultaneously. **The cached data allows for fast retrieval and, since the same data gets written in the permanent storage**, we will have complete data consistency between the cache and the storage. Also, this scheme ensures that **nothing will get lost in case of a crash**, **power failure, or other system disruptions**. Although, write-through minimizes the risk of data loss, since every write operation **must be done twice** before returning success to the client, this scheme has the **disadvantage** of **higher latency for write operations**.

<div align="center">
  <img src="./write-through.png" alt="write trough cache" />
</div>

### 2. Write-around cache
This technique is similar to write-through cache, but data is **written directly to permanent storage**, **bypassing the cache**. This can reduce the cache being flooded with write operations that will not subsequently be re-read, but has the disadvantage that a read request for recently written data will create a **“cache miss”** and must be **read from slower back-end storage** and **experience higher latency**.

<div align="center">
  <img src="./write-around.png" alt="write around cache" />
</div>