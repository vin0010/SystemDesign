# Phrases

- Some queries might require computationally intense server side resources.
- We will build geographically distributed network of CDNs to decrease load latency
- Users are geoDNS-routed, also known as geo-routed, to the closest data center
- https://github.com/vin0010/SystemDesign/blob/2d96e97199dab42f294144bbc4c183d6c4ab0fac/Concepts.md?plain=1#L13
- Distributed transactions ( commit across multiple services/databases, covered in database section)
- For a system that receives more data than it can process, we can use Message Queue. Our data is persisted before being processed, Help decoupling.
- Distribution of partitions across brokers is the key to high scalability
- Memcache - Only in memory. This makes it lightweight and fast but unsuitable for scenarios where data durability is critical. But multi-threading to fully utilize multi-core CPUs.
- Consider using cache when data is read frequently but modified infrequently.
- Inconsistency can happen because data-modifying operations on the data store and cache are not in a single transaction.
- When scaling across multiple regions, maintaining consistency between the data store and cache is challenging.
- This service can become stateless by storing user and session details in a data store.
- Consistency make database harder to scale.
- We need to implement proper isolation levels and either row-level locking or Optimistic Concurrency Control (OCC) to fully prevent double bookings.
- Keeping the Elasticsearch index synchronized with PostgreSQL can be complex and requires a reliable mechanism to ensure data consistency.
- Maintaining an Elasticsearch cluster adds additional infrastructure complexity and cost.
- CDNs are relatively expensive. To address this, it is common to be strategic about what files are cached and for how long. We can use a cache control header to specify how long the file should be cached in the CDN. We can also use a cache invalidation mechanism to remove files from the CDN when they are updated or deleted. This way, only files that are frequently accessed are cached and we don't waste money caching files that are rarely accessed



## Common one 
- I like to start with a broad overview of the primary entities. At this stage, it is not necessary to know every specific column or detail. We will focus on these intricacies later when we have a clearer grasp of the system (during the high-level design).
- I am going to outline some simple APIs, but may come back and improve them as we delve deeper into the design.
- 