# SystemDesign
> Many think that system design interview is all about a person's technical design skills. It is much more than that. An effective system design interview gives strong signals about a person's ability to collaborate, to work under pressure, and to resolve ambiguity constructively. The ability to ask good questions is also an essential skill, and many interviewers specifically look for this skill.

> Many things in SW engineering is all about trade offs and choices are not always black and white

> CAP theorem considers 100% of C or A or Pbut in real world its about degrees of consistency and availability


## 4 steps
1. Understand the problem and establish design scope
   1. This is very important
   2. Ask clarifying questions
   3. If the interviewer ask you to make assumptions, write down assumptions
   4. Check if you need back of the end envelope
2. Propose high-level design and get buy-in
   1. Come up with an initial blueprint for the design. Ask for feedback. Treat your interviewer as a teammate and work together. Many good interviewers love to talk and get involved.
   2. Draw box diagrams with key components on the whiteboard or paper. This might include clients (mobile/web), APIs, web servers, data stores, cache, CDN, message queue, etc.
   3. If possible, go through a few concrete use cases. This will help you frame the high-level design. It is also likely that the use cases would help you discover edge cases you have not yet considered.
   4. API and schema ->  depends on the problem, for design google search engine not necessary, for multiplayer poker game, it makes sense.
3. Design deep dive
   1. Had some initial ideas about areas to focus on in deep dive based on her feedback You shall work with the interviewer to identify and prioritize components in the architecture.
   2. Add more details to the system(look into news feed system diagram below)
   3. Talk about bottlenecks
   4. **Talk about Game days to simulate failure in each component and see how can we improve. **
4. Wrap up
   1. Recap the system if necessary
   2. Error cases (server failure, network loss, etc.) are interesting to talk about.
   3. Metrics and error logging
   4. How to handle the next scale curve is also an interesting topic. For example, if your current design supports 1 million users, what changes do you need to make to support 10

### Talk about
- Database scaling
- High concurrency
- Failure scenarios
- After choosing database talk about indexing options
- 

### Dos
- Always ask for clarification. Do not assume your assumption is correct. 
- Understand the requirements of the problem. 
- There is neither the right answer nor the best answer. A solution designed to solve the problems of a young startup is different from that of an established company with millions of users. Make sure you understand the requirements. 
- Let the interviewer know what you are thinking. Communicate with your interviewer. 
- Suggest multiple approaches if possible. 
- Once you agree with your interviewer on the blueprint, go into details on each component. Design the most critical components first. 
- Convey ideas to the interviewer

### Don'ts 
- Don’t go into too much detail on a single component in the beginning. Give the high-level design first then drills down.
- Communicate. Don't think in silence.

### Time
- Step 1 Understand the problem and establish design scope: 3 - 10 minutes 
- Step 2 Propose high-level design and get buy-in: 10 - 15 minutes 
- Step 3 Design deep dive: 10 - 25 minutes 
- Step 4 Wrap: 3 - 5 minutes

### Concurrency
- Higher concurrency means more open connections, more active threads, more messages being processed at the same time, and more CPU context switches.
- 

### Scalability
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
- geoDNS is a DNS service that allows domain names to be resolved to IP addresses based on the location of a user.
- Users are geoDNS-routed, also known as geo-routed, to the closest data center
- In the event of any significant data center outage, we direct all traffic to a healthy data center.
- Several technical challenges must be resolved to achieve multi-data center setup: 
	- Traffic redirection: Effective tools are needed to direct traffic to the correct data center. 
	- Data synchronization: Users from different regions could use different local databases or caches. 
	- In fail-over cases, traffic might be routed to a data center where data is unavailable.
	- Test and deployment: With multi-data center setup, it is important to test your website/application at different locations. Automated deployment tools are vital to keep services consistent through all the data centers


## Load balancer
- Improves system availability
- A load balancer evenly distributes incoming traffic among web servers that are defined in a load-balanced set.
- The load balancer communicates with web servers through private IPs.
- ![image](https://github.com/vin0010/SystemDesign/assets/10086767/a5eb623c-d907-47ad-b94b-4ca2e1d4ef5c)


## Redundancy

## Message Queue
- To further scale our system, we need to decouple different components of the system so they can be scaled independently. Messaging queue is a key strategy employed by many real-world distributed systems to solve this problem.
- The basic architecture of a message queue is simple. Input services, called producers/publishers, create messages, and publish them to a message queue. Other services or servers, called consumers/subscribers, connect to the queue, and perform actions defined by the messages.
- Decoupling makes the message queue a preferred architecture for building a scalable and reliable application. With the message queue, the producer can post a message to the queue when the consumer is unavailable to process it. The consumer can read messages from the queue even when the producer is unavailable.
- Partition is a queue
- Consumers
  - Consumers are very lightweight and you can have as many as you want. ( because Kafka maintains offset for each consumer group) 
  - Consumer group with bunch of consumers will not share partitions.
- Retention policy
  - TTL/age limit
- Fault tolerant & durable
- Kafka replicates partitions, so when a broker goes down, backup partition takes over and resume.    

## Logging, metrics, automation
- Metrics: Collecting different types of metrics help us to gain business insights and understand the health status of the system. Some of the following metrics are useful: • Host level metrics: CPU, Memory, disk I/O, etc.
	- Aggregated level metrics: for example, the performance of the entire database tier, cache tier, etc. 
	- Key business metrics: daily active users, retention, revenue, etc.
- Automation: When a system gets big and complex, we need to build or leverage automation tools to improve productivity. Continuous integration is a good practice, automating your build, test, deploy process, etc. could improve developer productivity significantly.

## API performance
- Identify bottlenecks through load tests and profiling requests
- Caching
  - In many layers as possible
- SQL
  - Connection pooling
    - Keep active connections rather than opening a new database connection everytime which involves lots of handshaking.
    - Reuse connections to improve throughput
    - This is a common pitfall in serverless architecture as each serverless components might handle it differently.
    - Tuning the database connection pool size based on the application behaviour. (Large number doesn't always mean more performance)
  - Connection pooling
  - Pagination
  - Purging stale data will improve query performance
  - N+1 problem or tools to identify inefficient queries. 
- Lazy loading
- Lightweight json serializers
- Payload/response compression will save time
- Asynchronous logging


### Organize
- Build confidence by doing game day testing and deliberately fail components and check how the system holding up and if it require any fine tuning/fix.
- SLA agreements by checking SLA latencies(P99, 95 and 50) to improve customer confidence and also know how much you can scale further
- P99 through the roof
- 

