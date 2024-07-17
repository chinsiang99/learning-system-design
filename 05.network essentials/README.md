# HTTP vs. HTTPS
**HTTP** (*Hypertext Transfer Protocol*) and **HTTPS** (*Hypertext Transfer Protocol Secure*) are both **protocols** used for **transmitting data over the internet**, primarily used for loading webpages. While they are similar in many ways, the **key difference** lies in the **security aspect** provided by HTTPS. Let's compare the two:

## HTTP
### Characteristics:
1. No Encryption: HTTP **does not encrypt** the data being transmitted. This means that the data can be intercepted and read by others.
2. Default Port: It typically operates over port 80.
3. Vulnerabilities: **More vulnerable** to **man-in-the-middle** attacks and **eavesdropping**.

### Use Cases:
1. Browsing simple websites where sensitive data is not exchanged, like informational blogs.
2. In the past, it was the standard for all web communications, but its use is declining due to security concerns.

## HTTPS

### Characteristics:
1. Encryption: HTTPS encrypts the data being transmitted using protocols like **SSL** (Secure Sockets Layer) or **TLS** (Transport Layer Security). This encryption ensures that even if the data is intercepted, it cannot be easily read by attackers.
2. Default Port: It operates over port 443.
3. Security: Provides **authentication** of the accessed website and protection of privacy and integrity of the exchanged data.
Trustworthiness: Websites with HTTPS are generally trusted more by users. **Browsers often mark HTTP sites as 'Not Secure'**.

### Use Cases:
- Ideal for any transactions that involve personal, financial, or sensitive data.
- Recommended for all types of websites to ensure secure communication.

## Key Differences:
1. Security: The most significant difference is security. **HTTPS provides a secure layer** through **encryption**, while **HTTP does not**.
2. Performance: *HTTPS* may cause **slightly more server load** due to the **encryption** and **decryption** process, but modern hardware and optimized software have significantly minimized this impact.
3. SEO Ranking: Search engines like Google give **preference to HTTPS** websites, considering them more secure. This can affect a website's search engine ranking.
4. Certificate Requirement: To implement HTTPS, a website must obtain an SSL/TLS certificate from a **Certificate Authority** (CA). This process is not required for HTTP.

## Summary
In summary, while HTTP is fine for simple, informational content, HTTPS is essential for any situation where security and privacy are important. The widespread adoption of HTTPS is part of an ongoing effort to create a more secure and trustworthy internet.

# TCP vs. UDP
**TCP** (Transmission Control Protocol) and **UDP** (User Datagram Protocol) are two of the main protocols used for **transmitting data over the internet**. Each has its characteristics, advantages, and disadvantages, making them suitable for different types of applications.

## TCP (Transmission Control Protocol)

### Definition
TCP is a **connection-oriented protocol** that ensures **reliable**, **ordered**, and **error-checked delivery** of a stream of bytes between applications.

### Characteristics
- Reliability: TCP **ensures that data is delivered accurately** and in **order**, retransmitting lost or corrupted packets.
- Connection-Oriented: **Establishes a connection** between sender and receiver **before transmitting data**.
- Flow Control: Manages data transmission rate to prevent network congestion.
- Congestion Control: Adjusts the transmission rate based on network traffic conditions.
- Acknowledgements and Retransmissions: Uses acknowledgments to confirm receipt of data and retransmits if necessary.

### Use Cases
Applications where **reliability** and **order** are **critical**, like **web browsing** (HTTP/HTTPS), **email** (SMTP, POP3, IMAP), and **file transfers** (FTP).

### Example
Loading a webpage: TCP is used to ensure all web content is loaded correctly and in the right order.

## UDP (User Datagram Protocol)
### Definition
UDP is a **connectionless protocol** that sends messages, called datagrams, **without establishing a prior connection** and **without guaranteeing reliability or order**.

### Characteristics
- Low Overhead: **Does not establish a connection**, leading to **lower overhead** and **latency**.
- Unreliable Delivery: Does not guarantee message delivery, order, or error checking.
- Speed: **Faster** than TCP due to its simplicity and l**ack of retransmission mechanisms**.
- No Congestion Control: Does not reduce transmission rates under network congestion.

### Use Cases
Applications that require speed and can tolerate some loss of data, like streaming video or audio, online gaming, or VoIP (Voice over Internet Protocol).

### Example
Streaming a live sports event: UDP is used for faster transmission, even if it means occasional pixelation or minor video artifacts.

## Key Differences

### 1. Reliability:

- TCP: **Reliable** transmission, ensuring data is delivered **accurately** and in **order**.
- UDP: **Unreliable** transmission; **data may be lost** or arrive out of order.

### 2. Connection:

- TCP: **Connection-oriented**; establishes a connection before transmitting data.
- UDP: **Connectionless**; sends data without establishing a connection.

### 3. Speed and Overhead:

- TCP: Slower due to **handshaking**, **acknowledgments**, and **congestion** control.
- UDP: Faster with minimal overhead, suitable for **real-time applications**.

### 4. Data Integrity:

- TCP: **High data integrity**, suitable for applications like file transfers and web browsing.
- UDP: **Lower data integrity**, acceptable for applications like streaming where perfect accuracy is less critical.

### 5. Use Case Suitability:

- TCP: Used when **data accuracy is more critical than speed**.
- UDP: Used when **speed is more critical than accuracy**.

## Conclusion
TCP is used for applications where reliable and accurate data transmission is crucial, whereas UDP is chosen for applications where speed is more important than reliability, and some loss of data is acceptable.

# URL vs. URI vs. URN
Understanding the differences between **URL**, **URI**, and **URN** can be crucial in web development and networking. Let's break down these concepts:

## URL (Uniform Resource Locator):
- Definition: A URL is a **specific type of URI** that **not only identifies a resource on the internet** but also **provides a method to locate** it by **describing its primary access mechanism**, usually its network location.
- Components: It typically **includes a protocol** (such as HTTP, HTTPS, FTP), domain name, and path, optionally followed by query parameters or a fragment identifier.
- Example: https://www.example.com/path?query=term#section
- Key Characteristics:
    - Specifies how the resource can be accessed (protocol).
    - Includes the location of the resource (like a web address).

## URI (Uniform Resource Identifier):
- Definition: A *URI* is a **generic term** used to identify a resource either by **location, name, or both**. It serves as a **universal identifier** for resources on the internet.
- Scope: All **URLs** and **URNs** are **URIs**, but not all URIs are URLs or URNs.
- Example: A URL **https://www.example.com** is also a URI, and a URN like **urn:isbn:0451450523** (identifying a book by its ISBN) is also a URI.
- Key Characteristics:
    - A more general concept than both URL and URN.
    - It can be either a **locator** (*URL*), a **name** (*URN*), or **both**.

## URN (Uniform Resource Name):
- Definition: A URN is a type of URI that **names a resource** without describing how to locate it. It’s used to assign a **unique and persistent identifier** to a resource.
- Example: **urn:isbn:0451450523** uniquely identifies a book using its ISBN, irrespective of where it exists.
- Key Characteristics:
    - Provides a **unique and persistent** identifier.
    - **Does not specify a location** or **method** to access the resource.

## Summary of Differences:
- URL: Specifies both the identity and the location of a resource (How and Where).
- URI: A more comprehensive term covering both URLs (identifying and locating) and URNs (just identifying).
- URN: Focuses only on uniquely identifying a resource, not on where it is located or how to access it.

In practical terms, when you’re browsing the internet, you're mostly dealing with URLs. URIs and URNs come more into play in specific contexts like software development, digital libraries, and systems where unique and persistent identification of a resource is crucial.

# Introduction to DNS

## What is DNS (Domain Name System)?
*DNS*, or **Domain Name System**, is a system used to **translate human-readable domain names** (e.g., www.designgurus.com) into **IP addresses** (e.g., 198.47.25.1) that computers can understand. This translation process is crucial because computers and networking devices rely on IP addresses to identify and communicate with each other on the internet. In simple terms, DNS acts like a phonebook for the internet, allowing users to access websites using easy-to-remember domain names instead of having to memorize numeric IP addresses.

## Purpose and Importance of DNS
The primary purpose of DNS is to **make it easier for people to access websites** and other online resources. By providing a human-readable naming system for computers and other devices connected to the internet, DNS **enables users to navigate the internet using familiar and intuitive domain names**.

DNS is essential for the smooth functioning of the internet. Some of its key benefits include:

1. User-friendliness: Domain names are easier to remember and type than IP addresses, which are long strings of numbers.
2. Scalability: DNS is a distributed and hierarchical system, allowing it to handle the ever-growing number of domain names and IP addresses on the internet.
3. Flexibility: DNS allows websites to change their IP addresses without affecting users. When a website's IP address changes, the DNS records are updated, and users can continue accessing the site using the same domain name.
4. Load balancing: DNS can distribute user requests across multiple servers, improving the performance and reliability of websites.

## DNS Components and Terminology
### 1. **Domain names**, **TLDs** (Top-Level Domains), and **subdomains**

- Domain names: A domain name is a human-readable address used to access a website or other resources on the internet. It consists of a series of character strings separated by dots, such as www.example.com. Domain names are easier to remember and use than IP addresses.

- TLDs (Top-Level Domains): A top-level domain (TLD) is the **rightmost part of a domain name**, **such as ".com" in www.example.com**. TLDs are managed by various organizations and can be divided into two categories: **generic TLDs** (gTLDs), like **.com**, **.org**, or **.net**, and **country-code TLDs** (ccTLDs), which represent specific countries or territories, like .us for the United States or .uk for the United Kingdom.

- Subdomains: A subdomain is a subdivision of a domain name, allowing the creation of separate sections or areas within a website. Subdomains appear to the left of the main domain name, such as **blog.example.com**, where **"blog"** is the subdomain of example.com.

### 2. DNS servers: **Root**, **TLD**, and **Authoritative Name Servers**
- Root servers: Root servers are the highest level of DNS servers and are responsible for directing queries to the appropriate TLD servers. There are 13 root server clusters worldwide, managed by various organizations, each having multiple servers for redundancy and reliability.

- TLD servers: TLD servers store information about domain names within their specific TLD. When they receive a query, they direct it to the appropriate authoritative name server responsible for that domain.

- Authoritative name servers: These servers hold the actual DNS records for a domain, including its IP address and other information. They provide the final answer to DNS queries, allowing users to access the desired website or resource.

<div align="center">
  <img src="./dns.png" alt="dns" />
</div>

### 3. DNS resolvers (caching and forwarding)
- DNS resolvers: Also known as recursive resolvers, DNS resolvers are usually provided by internet service providers (ISPs) or other organizations. They act as intermediaries between users and DNS servers, receiving DNS queries from users and sending them to the appropriate DNS servers to be resolved. Once the resolver receives the answer, it caches the information and returns it to the user.

- Caching resolver: A caching resolver stores previously resolved queries in its cache, speeding up the resolution process for future requests. If the requested information is available in the cache, the caching resolver returns the answer directly without contacting other DNS servers.

- Forwarding resolver: A forwarding resolver forwards DNS queries to another resolver, which is typically a caching resolver, instead of contacting DNS servers directly. This setup allows for better control, security, and performance.

# DNS Resolution Process
DNS **translates human-readable domain names** into **machine-readable IP addresses**. This translation process, known as DNS resolution, enables users to access websites and online services using easy-to-remember domain names instead of having to memorize complex numerical IP addresses. The DNS resolution process involves a series of recursive and iterative queries, utilizing a distributed and hierarchical infrastructure of DNS servers, resolvers, and caching mechanisms. This chapter delves into the details of the DNS resolution process, providing a clear understanding of how domain names are resolved into IP addresses and the role of various DNS components in ensuring a seamless and efficient browsing experience for users.


## 1. Recursive and Iterative DNS queries
DNS resolution is the process of converting a domain name into its corresponding IP address. There are two types of DNS queries involved in this process: recursive and iterative queries.

- Recursive query: In a recursive query, the DNS resolver asks for the complete answer to a query from the DNS server. If the server has the answer, it responds with the required information. If not, the server takes responsibility for contacting other DNS servers to find the answer and then returns it to the resolver. Recursive queries put more responsibility on the DNS server to find the requested information.

- Iterative query: In an iterative query, the DNS resolver asks the DNS server for the best answer it has at the moment. If the server doesn't have the complete answer, it responds with a referral to another server that might have more information. The resolver then contacts that server with a new iterative query, repeating the process until it finds the complete answer. In iterative queries, the resolver takes on more responsibility for finding the requested information.

## 2. DNS caching and TTL (Time To Live)
To speed up the DNS resolution process, resolvers and servers cache the results of previous queries. When a resolver receives a query, it first checks its cache to see if the answer is already available. If it finds the cached information, it returns the answer without contacting other servers, saving time and reducing network traffic.

Each DNS record has an associated Time To Live (TTL) value, which specifies how long the record should be stored in the cache. TTL is measured in seconds, and once the TTL expires, the cached information is removed to ensure that outdated information is not used.

## 3. Negative caching
Negative caching is the process of caching the non-existence of a DNS record. When a resolver receives a query for a non-existent domain or record, it caches this information as a negative response, preventing repeated queries for the same non-existent resource. This reduces the load on DNS servers and improves overall performance.

In short, the DNS resolution process involves converting a domain name into its corresponding IP address using recursive and iterative queries. Resolvers and servers cache the results of previous queries to speed up the resolution process, with TTL values determining how long the records are stored. Negative caching helps improve performance by caching the non-existence of DNS records.