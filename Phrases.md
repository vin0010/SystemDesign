# Phrases

- Do cons outweight pros
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