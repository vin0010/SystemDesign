# Problems

https://excalidraw.com/#json=430FBILICn5gUOHNEzWDw,ZLJ9la7U2IbLqVzNm26sSw

|    | Problem                         | Attempted          | Confident | Key Concepts                                                        |
|----|---------------------------------|--------------------|-----------|---------------------------------------------------------------------|
| 1  | Distributed Metrics/Logging     | :x:                | :x:       | - Distributed Systems<br>- Logging<br>- Metrics<br>- Event Sourcing |
| 2  | Rate Limiter                    | :x:                | :x:       | - Rate Limiting<br>- Distributed Systems                            |
| 3  | Consistent Hashing              | :x:                | :x:       | - Hashing<br>- Consistent Hashing<br>- Distributed Systems          |
| 4  | KV store                        | :x:                | :x:       | - Key-Value Store<br>- NoSQL Databases                              |
| 5  | UID generator                   | :x:                | :x:       | - Unique Identifier<br>- Distributed Systems                        |
| 6  | URL shortener                   | :white_check_mark: | :x:       | - URL Shortening<br>- Hashing<br>- Redirects                        |
| 7  | Web crawler                     | :x:                | :x:       | - Web Crawling<br>- Distributed Systems                             |
| 8  | Notification System             | :x:                | :x:       | - Notifications<br>- Pub/Sub<br>- Distributed Systems               |
| 9  | News feed system                | :x:                | :x:       | - News Feed<br>- Social Networks<br>- Algorithms                    |
| 10 | Chat                            | :x:                | :x:       | - Real-time Messaging<br>- Websockets<br>- Pub/Sub                  |
| 11 | Search autocomplete             | :x:                | :x:       | - Search Algorithms<br>- Autocomplete<br>- Data Structures          |
| 12 | Youtube                         | :x:                | :x:       | - Video Streaming<br>- Content Delivery<br>- Recommendation Systems |
| 13 | Drive                           | :x:                | :x:       | - File Storage<br>- Cloud Storage<br>- Distributed Systems          |
| 14 | Swiggy/Doordash                 | :x:                | :x:       | - Food Delivery<br>- Geolocation<br>- Order Management              |
| 15 | Kids safety                     | :x:                | :x:       | - Child Safety<br>- Parental Controls<br>- Monitoring               |
| 16 | Proximity service               | :x:                | :x:       | - Proximity Detection<br>- Location-based Services                  |
| 17 | Nearby friends                  | :x:                | :x:       | - Location Sharing<br>- Social Networks                             |
| 18 | Google map                      | :x:                | :x:       | - Maps<br>- Geolocation<br>- Routing<br>- API                       |
| 19 | Distributed Message Queue       | :x:                | :x:       | - Message Queues<br>- Pub/Sub<br>- Distributed Systems              |
| 20 | Metrics Monitoring and alerting | :x:                | :x:       | - Monitoring<br>- Alerting<br>- Distributed Systems                 |
| 21 | Ad click event aggregation      | :x:                | :x:       | - Ad Tech<br>- Event Aggregation<br>- Analytics                     |
| 22 | Hotel reservation               | :x:                | :x:       | - Reservation Systems<br>- Booking Platforms                        |
| 23 | Distributed Email service       | :x:                | :x:       | - Email<br>- SMTP<br>- Distributed Systems                          |
| 24 | S3 like blob storage            | :x:                | :x:       | - Object Storage<br>- AWS S3<br>- Distributed Systems               |
| 25 | Payment                         | :x:                | :x:       | - Payment Gateways<br>- Transactions<br>- Financial Systems         |
| 26 | Digital wallet                  | :x:                | :x:       | - Digital Payments<br>- Wallets<br>- Cryptocurrency                 |
| 27 | Stock exchange                  | :x:                | :x:       | - Stock Trading<br>- Financial Markets<br>- Exchange Platforms      |
| 28 | Job Scheduler                   | :white_check_mark: |           |                                                                     |


## Problems from Leetcode
- Ad click aggregation system 
- Top 10 songs played on spotify (top-k problem)
- Design web crawler 
- Deisgn online chess 
- Design whatsapp 
- Design price alert system similar to camelcamelcamel.com
- Design proximity server.
- Design the Facebook post privacy functionality. In other words, if I make a Facebook post, and I have 3 privacy options to choose from (Only Me, Friends Only, Public), design how would you get the visibility for any Faceook user (ie. can a FB user see the post or not)
- Design an online judge like leetcode
- Netflix
- Yelp
- Ticketmaster
  - Ticket booking workflows
  - Design a system to store images for FB and insta that would require 1000 uploads per sec and handle duplication
- TAG management (https://leetcode.com/discuss/interview-experience/4351482/Design-a-tagging-system-or-HLD-or-LLD)
- File download (https://leetcode.com/discuss/interview-experience/1263830/Facebook-product-design)
- Apply discount on Nth order (https://leetcode.com/discuss/interview-question/system-design/459593/Facebook-or-System-Design-or-E-commerce-Apply-discount-on-every-nth-order)
- Design Leaderboard ( Bharath )
- Realtime gaming ranking (https://leetcode.com/discuss/interview-question/system-design/625918/Amazon-or-System-Design-or-Design-a-real-time-gaming-ranking-system)
- Distributed counters
- System to give prices of stack ( https://leetcode.com/discuss/interview-question/system-design/431712/Bloomberg-or-Design-a-system-to-give-prices-of-a-stock )
- Design FigJam/Miro
- Enterprise service bus (https://leetcode.com/discuss/interview-question/system-design/734303/Microsoftor-Design-an-Enterprise-Service-Bus)
- 

## Tips
- Don't talk anything about database during estimation and clarification
- 
## 1. Distributed Metrics/Logging
- Use message broker
  - In memory message broker Vs Log based message broker
  - Stateless consumers
  - Time based aggregation
    - Aggregation windows
      - Tumbling windows - Fixed length and fixed start time, non overlappting i.e start of every minute. 
      - Hopping window - 0-5, 1-6, 2-7 etc, overlaps. 
      - Sliding window - Maintain LL to find for any range
  - Logs can be moved to S3
  - You cannot do data processing from S3, so need to move it to Hadoop cluster and run spark on that data.
  - Spark is a batch processing service widely used, better than map reduce 
    - Supports complicated processing and format sot hat you can throw to data warehouse
    
  <details>
    <summary>Architecture</summary>
    <img src="image/img.png" width="50%" alt="Architecture">
  </details>

## 6. Tiny URL / Pastebin
- Clarification and Estimation
  - Clarification
    - How long is the shortened URL? - Clarification
        - If they as short as possible, we should define length to avoid collision.
        - Chars allowed in hash
          - Chars - a, A 0-9 => 10+26+26 = 62. So 62^n combinations possible
        - Find smallest n such that 62^n < total URL writes ( 365 billion )
    - URL deleted/updated?
    - NFR
      - Missed NFR, never talked about Availability, Consistency and Fault tolerance
    - Never mentioned read or write heavy -> mention "READ > WRITE need to optimize this"
- Problems/Critical part/Deep dives
    - Address if we are going to create a unique ID and assign it to column (id, short URL hash, long URL) or search just hash
    - How to make long hashed value short from sha/MD hash
      - <details>
            <summary>Hash Shortening</summary>
            <img src="image/img_14.png" width="50%" alt="Hash Shortening">
        </details>
      - Hash + Collision resolution ( Hashed short URL needs to be verified if it exists in the system. Its costly process )
        - So use Bloom filters(A bloom filter is a space-efficient probabilistic technique to test if an element is a member of a set).
        - In case of collision 
          - Chaining
            - Not possible to store LL in DB
          - Probing
              - Or 32fz18 -> try next 32fz19 and so on.
      - Base 62 conversion ( represent values based on 0-9, a-z, A-Z => 0-61 base)
    - Redirection ( browser http status 302)
    - Partitioning
      - by range
          - Shard based on hash/short URL first char. a-d, e-h, i-s, t-z. This will relatively work since key is already hashed and this will be evenly distributed.
      - Consistent hashing for hash/short URL
    - Lock rows when writing an entry(short and long URL)
      - 1. Predicate locks to lock row that doesn't exist. (Costly but indexing short URL will make it faster)
      - 2. Create all precomputed hashes and use them.
    - Indexing types ( what engine to use)
      - Since read heavy use B-Tree. ( Look [engine selection](Database.md#performance) )
    - DB choice
      - Single leader, partitioned and Btree based -> MySQL, Postgres
      - Mongo DB could make an argument but above make sense considering the simple data model.
    - Read speed
      - Caching for hot links. Partitioning the cache by shortURL lead to fewer cache misses.
        - Write ahead cache suitable option.
        - LRU eviction
    - Pastebin 
      - Use S3 to store blob and everything else is same.
      - Write will be 2 phase commit to store in MySQL/Postgres and S3. 
    - Extras
      - Analytics
        - column for clicks ( address race condition without locks )
        - Kafka. So use log based message broker to aggregate later (no need for DB or in memory message broker).
        - Spark streaming with mini batch since no real time required.
      - Delete expired jobs
        - Use batch jobs with CRON
- Mentions
  - Monotonically increasing sequence is not a good idea since locking and indexing performance.
  - <details>
        <summary>Replication strategy</summary>
        <img src="image/img_15.png" width="50%" alt="Replication strategy">
    </details>
  
## Distributed Locking
- What is fencing token? 
  - Use it to make sure only eligible node releasing the lock.
  - 

## Processing
- Apache Parquet 
  - is an open source, column-oriented data file format designed for efficient data storage and retrieval. It provides efficient data compression and encoding schemes with enhanced performance to handle complex data in bulk.
- Columns store data or similar data compression
  - Dictionary encoding bitmap encoding

## Huge historical data, irrelevant
- Do "Sub Sampling" to take periodic portions of data 
- Archiving solution ( historical DB, move to S3/AWS glacier)


## Job Scheduler
- https://youtu.be/WTxG5880EH8?t=321



1. **Design a social media platform:**
    - Scalability, high availability
    - Data storage and replication
    - User authentication and authorization
    - Message delivery and real-time updates

2. **Design a content delivery network (CDN):**
    - Scalability, geographic distribution
    - Content caching and optimization
    - Load balancing and efficient routing
    - Delivery of static and dynamic content

3. **Design an e-commerce website:**
    - User authentication, payment processing
    - Product catalog, search and filtering
    - Order management, inventory handling
    - Real-time order tracking and updates

4. **Design a real-time chat application:**
    - Scalability, low latency
    - User authentication, message delivery
    - Real-time updates, group chat features
    - Data persistence and synchronization

5. **Design a distributed system for handling large amounts of data:**
    - Data partitioning and replication
    - Fault tolerance and consistency
    - Load balancing and scalability