# Sharding

- Horizontal scaling, also known as sharding, is the practice of adding more servers. Sharding separates large databases into smaller, more easily managed parts called shards. Each shard shares the same schema, though the actual data on each shard is unique to the shard.
  - <details>
        <summary>Sharding</summary>
        <img src="image/img_7.png" width="50%" alt="Sharding">
    </details>
  - Shards are physical servers, partitions happen on the data part
  - Decide sharding key based on load, access pattern and usecase.
  - A shard can have more than 1 partition
  - <details>
        <summary>Sharding with Partitions</summary>
        <img src="image/img_12.png" width="50%" alt="Sharding with Partitions">
    </details>

  - The most important factor to consider when implementing a sharding strategy is the choice of the sharding key. Sharding key (known as a partition key) consists of one or more columns that determine how data is distributed.
  - When choosing a sharding key, one of the most important criteria is to choose a key that can evenly distributed data.
  - Advantages
    - Handle large reads and writes.
    - Increase overall storage capacity
    - Higher availability
  - Disadvantages
    - Operational complexity 
    - Re-sharding data is hard. 
      - Re-sharding data is needed when
        - A single shard could no longer hold more data due to rapid growth. 
        - Certain shards might experience shard exhaustion faster than others due to uneven data distribution. When shard exhaustion happens, it requires updating the sharding function and moving data around. Consistent hashing, is a commonly used technique to solve this problem.
    - Celebrity/Hotspot Key problem
      - Excessive access to a specific shard could cause server overload. Imagine data for Katy Perry, Justin Bieber, and Lady Gaga all end up on the same shard. For social applications, that shard will be overwhelmed with read operations. To solve this problem, we may need to allocate a shard for each celebrity. Each shard might even require further partition.
    - Join and de-normalization / Cross shard queries
      - Once a database has been sharded across multiple servers, it is hard to perform join operations across database shards. A common workaround is to de-normalize the database so that queries can be performed in a single table.