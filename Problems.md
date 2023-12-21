# Problems

|    | Problem                         | Attempted          | Confident | Key Concepts                                                        |
|----|---------------------------------|--------------------|-----------|---------------------------------------------------------------------|
| 1  | Distributed Metrics/Logging     | :x:                | :x:       | - Distributed Systems<br>- Logging<br>- Metrics<br>- Event Sourcing |
| 2  | Rate Limiter                    | :x:                | :x:       | - Rate Limiting<br>- Distributed Systems                            |
| 3  | Consistent Hashing              | :x:                | :x:       | - Hashing<br>- Consistent Hashing<br>- Distributed Systems          |
| 4  | KV store                        | :x:                | :x:       | - Key-Value Store<br>- NoSQL Databases                              |
| 5  | UID generator                   | :x:                | :x:       | - Unique Identifier<br>- Distributed Systems                        |
| 6  | URL shortener                   | :x:                | :x:       | - URL Shortening<br>- Hashing<br>- Redirects                        |
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
- System to give prices of stack ( https://leetcode.com/discuss/interview-question/system-design/431712/Bloomberg-or-Design-a-system-to-give-prices-of-a-stock )
- Design FigJam/Miro
- Enterprise service bus (https://leetcode.com/discuss/interview-question/system-design/734303/Microsoftor-Design-an-Enterprise-Service-Bus)
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
    <img src="img.png" width="50%" alt="Architecture">
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