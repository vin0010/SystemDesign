# Scalability, Concurrency and Performance

## Scalability
- To further scale our system, we need to decouple different components of the system, so they can be scaled independently.
- If your system is very tightly interconnected, you may struggle to scale your engineering team
- Once your application reaches the limits of your server (due to increase in traffic, amount of data processed, or concurrency levels), you must decide how to scale further
    - Vertical Scaling
        - It is often the simplest solution for shortterm scalability
        - Vertical scalability becomes extremely expensive beyond a certain point.
    - Horizontal scaling
- To Scale a system
    - Build redundancy at every tier
    - Cache data as much as you can
    - Support multiple data centers
    - Host static assets in CDN
    - Scale your data tier by sharding
    - Split tiers into individual services
    - Monitor your system and use automation tools to identify problems

## Performance 
- Memory
  - Improving I/O access times by switching to solid-state drives (SSDs). Solid-state drives are becoming more and more popular as the technology matures and prices continue to fall.
  - Random reads and writes using SSDs are between 10 and 100 times faster,
- Data Compression
- Throttling from client side/Server side
- Client side validation

# Concurrency
> Concurrency in the context of system design refers to the ability of a system to handle multiple tasks or processes simultaneously. It is essential for improving system performance and responsiveness, but it also introduces challenges related to concurrency issues. Concurrency issues occur when multiple threads or processes access shared resources concurrently, leading to unpredictable and potentially incorrect behavior. Here are some common concurrency issues and strategies to deal with them in system design:

> - Higher concurrency means more open connections, more active threads, more messages being processed at the same time, and more CPU context switches.

### Race Conditions
Issue: A race condition occurs when the behavior of a system depends on the relative timing of events, and the outcome is unpredictable.
Solution: Use synchronization mechanisms such as locks, semaphores, or mutexes to control access to shared resources. Implement atomic operations to ensure that critical sections are executed without interruption.

### Deadlocks:
Issue: A deadlock happens when two or more processes are unable to proceed because each is waiting for the other to release a resource.
Solution: Implement deadlock detection and resolution mechanisms. Use a timeout mechanism to prevent indefinite waiting. Design systems to acquire resources in a consistent order to avoid circular dependencies.

### Starvation:
Issue: Starvation occurs when a thread or process is unable to access a resource it needs for a prolonged period due to competition with other threads.
Solution: Implement fairness mechanisms to ensure that all threads or processes have a fair chance to access shared resources. Use techniques such as priority scheduling or resource allocation policies to prevent starvation.

### Data Consistency:
Issue: In a multi-threaded environment, data inconsistencies can arise when one thread is reading or modifying data while another thread is concurrently modifying it.
Solution: Use atomic operations and transactions to maintain data consistency. Employ isolation levels in databases to control the visibility of changes made by concurrent transactions. Consider using optimistic or pessimistic locking strategies.

### Thread Interference:
Issue: Thread interference occurs when the execution of one thread impacts the correct execution of another thread.
Solution: Implement thread-safe data structures and algorithms. Use synchronization primitives to protect critical sections. Avoid shared mutable state whenever possible, favoring immutable data structures or thread-local storage.

### Concurrency Control in Databases:
Issue: In database systems, multiple transactions may attempt to read or modify the same data concurrently, leading to conflicts.
Solution: Employ techniques such as locking, timestamp ordering, or optimistic concurrency control to manage concurrent access to the database. Choose an appropriate isolation level to balance consistency and performance.