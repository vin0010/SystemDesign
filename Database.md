## Database
### Questions
- Decide based on Data access patterns, structure of data and Read/write ratio
- Need ACID?
- Structured data?

| Database             | Usecase                                                               |
|----------------------|-----------------------------------------------------------------------|
| GraphDB              | Whenever there is a followers, friends or graph                       |
| Document DB          | Different data types + Queries(limited support)                       |
| Column DB            | Ever increasing data + finite queries, Cassandra(light weight), Hbase |
| Time series database | Sequencial/append only write mode(InfluxDB, openTS DB)                |
| Analytics database   | Hadoop                                                                |
| Blob storage         | S3 + CDN (region based surving)                                       |

![image](https://github.com/vin0010/SystemDesign/assets/10086767/17f4b25d-2e29-4350-a5fa-46e4d6131b5d)

- Non-relational databases might be the right choice if: • Your application requires super-low latency.
- Your data are unstructured, or you do not have any relational data.
- You only need to serialize and deserialize data (JSON, XML, YAML, etc.).
- RDBMS
  - Replication
    - Single leader replication -> All write to once DB and reads from any
    - Multiple leader replication -> All write goes to small group, read from any
    - Leaderless replication -> write to all, read to all. 
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
  - RDBMS uses complex two way locking mechanism to achieve correctness and maintain ACID property.
- NoSQL
   - Instead of storing data in rows, we can store data in documents with IDs and I can store nested documents. We can store ton of data in this collection. 
   - Limited querying capabilities. 
   - Storing denormalized duplicate data lead to inconsistency ( need to sync)
   - Most support transactions.
   - Better for read intensive and non structured data
- Time Series Database
  - Very high write throughput
  - Regular and irregular writes
  - Data needs to be highly compressed
  - Large range scans of many records, so need to handle rollup and aggregation mechanism before if it make sense.
  - Write latest time entry only
  - Using time series DB is useful for read, write and data visualization
- Databases
  - MongoDB
    - Support transactions and Btrees
  - Cassandra
    - Fast writes, slower reads, little compromise a little on consistency adn occasional data is lost on overwritten 
    - Wide column data store like spreadsheet
    - Support multi leader and leaderless replication ( configurable )
    - Support quorum writes
      - Each data operation, such as read or write, requires a certain number of nodes to acknowledge the operation before it is considered successful. This number is called the quorum and is usually a majority of the nodes.
    - Write conflicts - cassandra let last write wins. There can be issues if lower time stamps write processed later
    - Use LSM tree and SSM tables for indexing
    - Slower reads
    - Ideal for chat applications where chat ID is used to decide the shard and all of the messages are ordered by timestamp as sort key
    - Weakness - 
      - Conflict resolution ( last write wins)
      - SLower reads
  - RIAK
    - Key Value store 
    - Same as cassandra ( cassandra is wide column store )
    - Use CRDTS(conflict free replicated data types) in order to deal with conflict resolution
    - Aggregating conflicting writes and process them
    - Handy when dealing with counters and sets in multi leader or leaderless replication 
    - eventually consistent
  - Apache Hbase
    - Wide column as cassandra
    - Built on top of Hdfs/Hadoop. 
    - Only single leader replication
    - No need to worry about write conflicts
    - Used column wide storage to store data. Helpful for column based locality. 
    - Useful for fast reads on columns. 
  - MemCache and Redis
    - Key value stores
    - Implemented in memory
    - Redis rich feature set-> geo sharding, sorted sets, 
    - Built using hashmap internally. 
    - Worse for range queries
    - Useful small data sets since in memory
    - Useful in geo spatial index in uber and swiggy, constantly update driver locations. 
  - Neo4j
    - Graph databse
    - We can use Graph in SQL with many to many relationships but very slow. 
    - Graph with SQL capabilities
    - Pointers to actual location of adjacent nodes, fetch in constant time opposed to SQL based constant time.
    - Map data, modelling friends. 
  - TimeScaleDB/Apache Druid
    - Append only database is one option
    - LSM Tree + SS Tables for indexing -> fast writes
    - Multiple LSM indexes with time indexed data
    - Use tombstone method to delete irrelevent data
    - Useful for logs, sensor data, ingestion etc
    - Instead of one large index for one table, they split the table to bunch of mini index. SO write and read will be effective
    - They also delete certain data once its old.
    
### Performance of MYsql
#### Concurrency
- Pessimistic concurrency control vs Optimistic concurrency control
  - Database handle these locks in row level. If a single row is being concurrently handled by 1000s of queries, that's a really a bad design.
  - If data access conflicts are very rare, go with optimistic or use pessimistic. 
  - In pessimistic, locks are used. 


### Organize
- Tune memory size
- Migrating live prod database is very complex and costly
- Cassandra handle high volume of writes

### Check 
- What is read after write consistency


### Number
So 9.3 million rows + 1 m and expected increase of 3-5 million rows every year. So I'm wondering if I will regret this decision in 2 years time or will PostgreSQL be still doing fine with 20M rows, 40M rows, 100M rows, ...
I'm running General Purpose, 8 vCore(s), 50 GB Azure PostgreSQL barely scratching 40% CPU (I will be downscaling it soon)