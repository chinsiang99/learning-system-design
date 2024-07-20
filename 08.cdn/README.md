# What is CDN?
A Content Delivery Network (CDN) is a **distributed network of servers** strategically **located across various geographical locations to deliver web content**, such as **images**, **videos**, and **other static assets**, more efficiently to users. The primary purpose of a CDN is to **reduce latency and improve the overall performance of web applications by serving content** from the server nearest to the user. CDNs can also help improve **reliability, availability, and security of web applications**.

## How CDNs work?
When a user requests content from a web application, the request is routed to the nearest **CDN server** (also known as an **edge server**) based on factors such as network latency and server load. The edge server then checks if the requested content is already cached. If it is, the content is served directly from the cache; otherwise, the edge server fetches the content from the origin server, caches it, and serves it to the user. Subsequent requests for the same content can then be served from the cache, reducing latency and offloading traffic from the origin server.

<div align="center">
  <img src="./cdn.png" alt="cdn" />
</div>

## Key terminology and concepts
1. Point of Presence (PoP): A PoP is a **physical location** where CDN servers are deployed, typically in data centers distributed across various geographical locations. PoPs are **strategically placed close to end-users** to minimize latency and improve content delivery performance.

2. Edge Server: An edge server is a **CDN server located at a PoP**, responsible for caching and delivering content to end-users. **These servers store cached copies of the content, reducing the need to fetch data from the origin server**.

3. Origin Server: The origin server is the **primary server where the original content is stored**. CDNs **fetch content from the origin server and cache it on edge servers for faster delivery to end-users**.

4. Cache Warming: Cache warming is the p**rocess of preloading content into the edge server's cache** **before it is requested by users, ensuring that the content is available for fast delivery when it is needed**.

5. Time to Live (TTL) : TTL is a value that determines how long a piece of content should be stored in the cache before it is considered stale and needs to be refreshed from the origin server.

6. Anycast: Anycast is a **network routing technique** used by CDNs to **direct user requests to the nearest available edge server**, based on the **lowest latency or the shortest network path**.

7. Content Invalidation: Content invalidation is the process of removing or updating cached content when the original content on the origin server changes, ensuring that end-users receive the most up-to-date version of the content.

8. Cache Purging: Cache purging is the process of forcibly removing content from the edge server's cache, usually triggered manually or automatically when specific conditions are met.