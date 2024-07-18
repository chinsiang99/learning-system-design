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