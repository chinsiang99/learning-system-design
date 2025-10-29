- we need to quickly do it within small amount of time, normally within 5 minutes to finish the estimation

# normally we will discuss be low four
- traffic
- storage
- bandwidth
- memory

and normally they said that traffic and storage is enough to score in an estimation, but here, it is better for me to know bandwidth and memory as well, because I am for greatness, and i believe i have endless potential

- the input we need from interview (ask the interviewer)
- how many daily active users (DAU) ?
- number of users, -> requests
- how will a typical user use the service
- how many write and read request per day?

we need to check whether it is read heavy or write heave
- mostly is read heavy rather than write heavy (unless monitering, analytics, logging, etc)
- check the ratio, maybe 50 : 1, 1 is write, 50 is read


then, we will calculate the RPS (request per second)

- lets say write request per day is 1 million, which is 1 * 10^6
- we need to convert it to per second
- divide by (24 * 60 *60) which is divide by (24 * 3600) , and for simplicity, we can say it is 20 * 4000 and for simplicity yet again we can say it is actually 100000
- so it would be 10 request per second

- so if the ratio is 50 : 1
- we can say read request per second is actually 50 * 10
- which is 500 per second

- this ends for the traffic side

- below is for storage side
- for example pastebin

- because user normally use it for code, logs etc
- we can say average it will contain 200 lines of text, each line contains 10 words, each word 5 letters/characters, each character consume 1 byte of storage, if we sum it up one pastebin would be 200 * 10 * 5 = 10000 = 10kB
- so lets say just now we mention we assume it would be 10 request per second for write operation and it would be average 1 million per day, so meaning that the total of amount of data that we gonna store would be 1 million * 10kb, we can calculate it as 10GB per day
- so we need to have retention period of our data as well, maybe 5 years? 10 years? etc
- 5 * 365 days * 10GB, which we can say it is 5 * 400 * 10GB, which is 2k * 10GB, which is 20TB
- so in order to have 5 years of new paste, it will require 20TB
- and normally we will have replication of data, it will be 3 or 5 times 20TB, so those are the amount of data that we need to store

- and thats the end of storage side

- now we will proceed with the bandwidth side (if we choose to proceed with it)
- bandwidth is the amount of data transferred per second
- incoming data per second (write) = 10kb * 10 = 100kb per second
- outgoing data per second (read) = 500 * 10kb = 5MB per second

- and thats all for the bandwidth side

- now we will go for the memory side
- it is basically caching
- normally we use 80 20 rule, which we assume that it will have 20% of the paste will be so popular, it will generate 80 percent of the traffic
- so we would like to cache those 20 percents
- lets say we are having 50 Million daily reads having 10kb paste size and 20% of it
- it would be 50M * 10kb * 0.2
- so it would be 100GB
- but it would not need that much, because some of them would be the same paste, actual memory usage will be lesser than this
- and thats all for the memory side

- now we will proceed with a question here
- how many app services do we actually need in this case?
- first we need to know the number of requests per second that we should support, which in this case is 500

- number of requests per second to handle / number of requests per second a single server can handle = 500 / x
- it is also important to know that the request is either CPU bound, I/O bound or memory bound
- at a very very high level, if the request is cpu bound, x = number of physical cores / time to process request
- so if we use server with 8 cores, and the time to process one request is 0.5
- meaning that the server 8 / 0.5 meaning that the server can handle 16 requests per second
- in this case single core can perform 2 request per second

- so in our case, it would be 500 / 16, which we would need about 30 - 50 server to handle this


now we will have some common size for system design interview
- which is language & media
- it is sueful for document sizes, storage sizes, index sizes

Language
- 500k words in English
- A line of text contains 10 words
- a word contains 5 chars

Media
- HD image = 3MB approximately (height * width * bit width)
- it is around 1280 * 720 * 3B, so we will consider it 1k * 1k * 3B
- so it would be 3MB

- profile image (300 * 300) = 300kb

- 1 minute of HD Video = 50MB
- Frame size * frame rate (fps) * compression ratio * duration (seconds)
- 3mb * 30 * (1/100) * 60
= 54MB
- and it would be around 50MB

since a video has 1080p, 480p 360p 240p 144 p, so in order to store everything, we would need 50MB * 2, because 480p is 1080/2, 360 is 1080p / 4, if we add up all lower resolution, it would eventually be a hd video as well, so we will need to consider a 2 * 50MB