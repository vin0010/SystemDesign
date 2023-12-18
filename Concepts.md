Sure, here is a compact list of all three sections to prepare for system design interviews:

Concepts

## Non Functional Requirements
- CAP-based tradeoffs   
- Availability
  - Data centers - Geo(partitioning?)
    - To improve availability and provide a better user experience across wider geographical areas, supporting multiple data centers is crucial.
    - geoDNS is a DNS service that allows domain names to be resolved to IP addresses based on the location of a user.
    - Users are geoDNS-routed, also known as geo-routed, to the closest data center
    - In the event of any significant data center outage, we direct all traffic to a healthy data center.
    - Several technical challenges must be resolved to achieve multi-data center setup:
      - Traffic redirection: Effective tools are needed to direct traffic to the correct data center.
      - Data synchronization: Users from different regions could use different local databases or caches.
      - In fail-over cases, traffic might be routed to a data center where data is unavailable.
        - Test and deployment: With multi-data center setup, it is important to test your website/application at different locations. Automated deployment tools are vital to keep services consistent through all the data centers
- Consistency
- Partition tolerance
  - Redundancy
- Failover and fault tolerance mechanisms
- Distributed consensus protocols
  - RAFT
- Scalability
- [Concurrency](Concurrency.md)

## Data Storage and management
- Databases
  - SQL
  - NoSQL
  - Key-value
  - Document
  - Graph
  - Column store
  - Time Series
    - Using time series DB is useful for read, write and data visualization
  - Data Replication: Master-slave replication, Multi-master replication, Paxos algorithm
  - Data Partitioning
    - Sharding
    - Range partitioning
    - Hash partitioning
    - Geo partitioning
  - Data Durability and Fault Tolerance: ACID properties, BASE/CAP theorem
  - Redundancy: Creating multiple copies of data or components to ensure availability and fault tolerance
  - Distributed data storage and consistency
  - Data caching and eviction policies ( refer to caching )
  - Data modeling for high-performance and scalability
  - GeoData
    - Geohash for searching geodata
    - Postgres GIS extension for geospatial indexing and analysis
- Search

## Messaging
- Message brokers and queues
- Message ordering and reliability
- Event-driven architectures and systems
- Publish-subscribe messaging patterns

## Caching
- In-memory cache (Redis, Memcached)
- Cache types and strategies: LRU, LFU, LRU-MQ
- Cache invalidation and consistency
- Performance bottlenecks and optimization techniques
- Load balancing and scalability considerations

- A cache is a temporary storage area that stores the result of expensive responses or frequently accessed data in memory so that subsequent requests are served more quickly.
- The application performance is greatly affected by calling the database repeatedly. The cache can mitigate this problem.
- Here are a few considerations for using a cache system
   - Decide when to use cache. Consider using cache when data is read frequently but modified infrequently.
   - Expiration policy
      - It is advisable not to make the expiration date too short as this will cause the system to reload data from the database too frequently. Meanwhile, it is advisable not to make the expiration date too long as the data can become stale.
   - Consistency: This involves keeping the data store and the cache in sync. Inconsistency can happen because data-modifying operations on the data store and cache are not in a single transaction. When scaling across multiple regions, maintaining consistency between the data store and cache is challenging.
   - Mitigating failures: A single cache server represents a potential single point of failure
   - Another recommended approach is to overprovision the required memory by certain percentages.
   - Eviction policies
   - Stateless web tier by extracting user/session details to a data store

## Networking and Protocols
- Load balancers
  - Convey the type of load balancing ( Active passive etc )
  - Improves system availability
  - A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set.
  - The load balancer communicates with web servers through private IPs.
  - ![image](https://github.com/vin0010/SystemDesign/assets/10086767/a5eb623c-d907-47ad-b94b-4ca2e1d4ef5c)
- Reverse proxies and request routing
- Web sockets and real-time communication
- Remote procedure calls (RPC)
- Consistent hashing for load balancing
- Content delivery networks (CDNs)
    - A CDN is a network of geographically dispersed servers used to deliver static content.
    - Considerations
      - Cost
      - Expiration time
      - CDN fallback to fetch data from origin

## Big Data and Stream Processing
    - Big data processing frameworks: Hadoop, Spark, Kafka
    - Batch processing and data pipelines
    - Stream processing and real-time data analytics
      - Flink consumer
         - can keep a copy of local table so join with every message to move it to respective sub table/partition
         - Can handle messages in real time
      - Spark streaming consumer
         - can keep a copy of local table so join with every message to move it to respective sub table/partition
         - Can handle messages in mini batches.
    - Apache Kafka and its role in big data
    - Data ingestion, processing, aggregation and compression
    - Data Aggregation
       - Time based aggregation
       - Aggregation windows
          - Tumbling windows - Fixed length and fixed start time, non overlappting i.e start of every minute.
          - Hopping window - 0-5, 1-6, 2-7 etc, overlaps.
          - Sliding window - Maintain LL to find for any range
    - Data encoding frameworks
      - If you know the data format, you can use, ignore invalid data, you can use 
        - Avro
        - Protocol buffers
        - Thrift
   - Data visualization and dashboards

## Service Discovery and Orchestration
    - Service discovery protocols: ZooKeeper, Consul, etcd
    - Service registration and discovery
    - Distributed systems and microservices architecture
    - Container orchestration platforms: Kubernetes, Docker Swarm
    - Automated deployment and scaling
    - Monitoring and alerting for distributed systems

## Security and Reliability:
    - Authentication and authorization mechanisms
    - Data encryption and security protocols
    - Distributed transaction management
    - Resilience and fault tolerance strategies
    - Disaster recovery and backup plans
    - Performance monitoring and alerting



Technologies

1. Databases:
    - MySQL, PostgreSQL, Oracle
    - MongoDB, Cassandra, Redis
    - DynamoDB, Elasticsearch

2. Message Brokers and Queues:
    - Kafka, RabbitMQ, Amazon SQS
    - Azure Service Bus, Apache Pulsar

3. Load Balancers and Reverse Proxies:
    - ELB, NGINX, HAProxy
    - Azure Load Balancer, Google Cloud Load Balancing

4. Web Sockets and Real-time Communication:
    - Socket.io, WebRTC
    - Apollo Server, GraphQL subscriptions

5. RPC Frameworks:
    - gRPC, Thrift
    - Apache Thrift, Finagle

6. Big Data Frameworks:
    - Apache Hadoop, Apache Spark
    - Apache Kafka, Apache Flink

7. Service Discovery and Orchestration Platforms:
    - ZooKeeper, Consul, etcd
    - Kubernetes, Docker Swarm
    - HashiCorp Nomad, Amazon ECS

8. Monitoring and Alerting Tools:
    - Prometheus, Grafana
    - Splunk, DataDog
    - New Relic, ELK stack
