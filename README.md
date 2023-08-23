# SystemDesign
> Many think that system design interview is all about a person's technical design skills. It is much more than that. An effective system design interview gives strong signals about a person's ability to collaborate, to work under pressure, and to resolve ambiguity constructively. The ability to ask good questions is also an essential skill, and many interviewers specifically look for this skill.

Concurrency
- Higher concurrency means more open connections, more active threads, more messages being processed at the same time, and more CPU context switches.

Scalability
- To further scale our system, we need to decouple different components of the system so they can be scaled independently.
- If your system is very tightly interconnected, you may struggle to scale your engineering team
- Once your application reaches the limits of your server (due to increase in traffic, amount of data processed, or concurrency levels), you must decide how to scale further
	- Vertical Scaling
		- It is often the simplest solution for shortterm scalability
		- Vertical scalability becomes extremely expensive beyond a certain point.
- To Scale a system
  - Build redundancy at every tier 
  - Cache data as much as you can 
  - Support multiple data centers 
  - Host static assets in CDN 
  - Scale your data tier by sharding 
  - Split tiers into individual services 
  - Monitor your system and use automation tools




Memory
- Improving I/O access times by switching to solid-state drives (SSDs). Solid-state drives are becoming more and more popular as the technology matures and prices continue to fall.
- Random reads and writes using SSDs are between 10 and 100 times faster,




------- 
## General Design template
<img width="636" alt="image" src="https://github.com/vin0010/SystemDesign/assets/10086767/b0db6ecc-d776-4eae-9131-ae3afd85f07c">



## Database
- Non-relational databases might be the right choice if: • Your application requires super-low latency.
- Your data are unstructured, or you do not have any relational data.
- You only need to serialize and deserialize data (JSON, XML, YAML, etc.).
- RDBMS
	- Master/Slave
		- A master database generally only supports write operations. A slave database gets copies of the data from the master database and only supports read operations. All the data-modifying commands like insert, delete, or update must be sent to the master database. Most applications require a much higher ratio of reads to writes; thus, the number of slave databases in a system is usually larger than the number of master databases.
		- Advantages of database replication: 
			- Better performance: In the master-slave model, all writes and updates happen in master nodes; whereas, read operations are distributed across slave nodes. This model improves performance because it allows more queries to be processed in parallel. 
			- Reliability: If one of your database servers is destroyed by a natural disaster, such as a typhoon or an earthquake, data is still preserved. You do not need to worry about data loss because data is replicated across multiple locations. 
			- High availability: By replicating data across different locations, your website remains in operation even if a database is offline as you can access data stored in another database server.
		- If the master database goes offline, a slave database will be promoted to be the new master. All the database operations will be temporarily executed on the new master database. A new slave database will replace the old one for data replication immediately. In production systems, promoting a new master is more complicated as the data in a slave database might not be up to date. The missing data needs to be updated by running data recovery scripts.
  - **Scaling**
    - Vertical scaling
      - Add more power to existing machine. AWS RDS can support upto 24Tb of memory. 
      - Stackoverflow in 2013 with one master shards handled 10 million unique users.
      - Drawbacks
        - Hardware limits
        - SPOF
        - High cost
    - **Horizontal scaling / Sharding**
      - Horizontal scaling, also known as sharding, is the practice of adding more servers. Sharding separates large databases into smaller, more easily managed parts called shards. Each shard shares the same schema, though the actual data on each shard is unique to the shard.
      - <img width="594" alt="image" src="https://github.com/vin0010/SystemDesign/assets/10086767/27f0fe1f-7e53-45b7-918e-3a68ead928c7">
      - The most important factor to consider when implementing a sharding strategy is the choice of the sharding key. Sharding key (known as a partition key) consists of one or more columns that determine how data is distributed.
      - When choosing a sharding key, one of the most important criteria is to choose a key that can evenly distributed data.
      - Problems with sharding
        - Resharding data: Resharding data is needed when 1) a single shard could no longer hold more data due to rapid growth. 2) Certain shards might experience shard exhaustion faster than others due to uneven data distribution. When shard exhaustion happens, it requires updating the sharding function and moving data around. Consistent hashing, which will be discussed in Chapter 5, is a commonly used technique to solve this problem. 
        - Celebrity problem: This is also called a hotspot key problem. Excessive access to a specific shard could cause server overload. Imagine data for Katy Perry, Justin Bieber, and Lady Gaga all end up on the same shard. For social applications, that shard will be overwhelmed with read operations. To solve this problem, we may need to allocate a shard for each celebrity. Each shard might even require further partition. 
        - Join and de-normalization: Once a database has been sharded across multiple servers, it is hard to perform join operations across database shards. A common workaround is to de-normalize the database so that queries can be performed in a single table.




## Cache
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
## CDN
- A CDN is a network of geographically dispersed servers used to deliver static content.
- Considerations
	- Cost
	- Expiration time
	- CDN fallback to fetch data from origin

## Data centers - Geo(partitioning?)
- To improve availability and provide a better user experience across wider geographical areas, supporting multiple data centers is crucial.
- Users are geoDNS-routed, also known as geo-routed, to the closest data center
- geoDNS is a DNS service that allows domain names to be resolved to IP addresses based on the location of a user.
- In the event of any significant data center outage, we direct all traffic to a healthy data center.
- Several technical challenges must be resolved to achieve multi-data center setup: 
	- Traffic redirection: Effective tools are needed to direct traffic to the correct data center. 
	- Data synchronization: Users from different regions could use different local databases or caches. 
	- In failover cases, traffic might be routed to a data center where data is unavailable.
	- Test and deployment: With multi-data center setup, it is important to test your website/application at different locations. Automated deployment tools are vital to keep services consistent through all the data centers


## Load balancer
- Improves system availability
- A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set.
- The load balancer communicates with web servers through private IPs.


## Message Queue
- To further scale our system, we need to decouple different components of the system so they can be scaled independently. Messaging queue is a key strategy employed by many real-world distributed systems to solve this problem.
- The basic architecture of a message queue is simple. Input services, called producers/publishers, create messages, and publish them to a message queue. Other services or servers, called consumers/subscribers, connect to the queue, and perform actions defined by the messages.
- Decoupling makes the message queue a preferred architecture for building a scalable and reliable application. With the message queue, the producer can post a message to the queue when the consumer is unavailable to process it. The consumer can read messages from the queue even when the producer is unavailable.

## Logging, metrics, automation
- Metrics: Collecting different types of metrics help us to gain business insights and understand the health status of the system. Some of the following metrics are useful: • Host level metrics: CPU, Memory, disk I/O, etc.
	- Aggregated level metrics: for example, the performance of the entire database tier, cache tier, etc. 
	- Key business metrics: daily active users, retention, revenue, etc.
- Automation: When a system gets big and complex, we need to build or leverage automation tools to improve productivity. Continuous integration is a good practice, automating your build, test, deploy process, etc. could improve developer productivity significantly.




