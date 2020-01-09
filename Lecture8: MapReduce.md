## Map Reduce

### Big Data
- Characteristics: (Volume, Velocity, Variety, Veracity)
- Types of Data: Relational Data, Graph Data, Streaming Data (Scanable)
- Processing on data: Aggregation,Indexing, Searching, Mining, etc.

### Parallelism Vs Concurrency
- Parallelism (Dividing into sub-problems, *Main concern*: speed)
  - Challnges:
    - Data parallelism: the same independent operation is applied repeatedly to different data
    - Task parallelism: independent work encapsulated in functions to be mapped to individual threads, which execute asynchronously
    - Load balancing
    - Failure handling
- Concurrency (Different synchronized processes run concurrently, *Main concern*: modularity, responsivenes)

### MapReduce 
- **Advantages**: allows programmers to easily utilize the resources of a large distributed system with parallelism.
- **Programming technique**: Functional Programming.
- **Main functions** 
  - Map: (in_key, in_value) -> list(out_key, intermediate_value)
  - Reduce: (out_key, list(intermediate_values)) -> list(out_values)
  - Exmaple: Count word occurances, Reverse Web-Link Graph, Count URL frequency, etc ..

<a href="https://ibb.co/z5GTJgx"><img src="https://i.ibb.co/g7zLV89/152b7931555b284af0dbd3446636b059.png" alt="152b7931555b284af0dbd3446636b059" border="0"></a>
  - **Programming**
    - Externally: For user
      - Write a Map program (short), write a Reduce program (short)
      - Specify number of Maps and Reduces (parallelism level)
      - Submit job; wait for result
      - Need to know very little about parallel/distributed programming!
    - Internally: For the Paradigm and Scheduler
      - Parallelize Map
      - Transfer data from Map to Reduce (shuffle data)
      - Parallelize Reduce
      - Implement Storage for Map input, Map output, Reduce input, and Reduce output
   - **Locality**
      - Mapreduce attempts to schedule a map task on a machine that contains a replica of corresponding input data.
      - GFS divides each file into 64 MB blocks, and stores several copies of each block (typically 3 copies) on different machines
      - Master scheduling policy:
        - Asks GFS for locations of replicas of input file blocks
        - Map tasks typically split into 64MB (== GFS block size)
        - Map tasks scheduled so GFS input block replica are on same machine or same rack
      - An optional **Combiner** function that does partial merging maybe used with the reduce functions if **significant repetition in intermediate keys**
      - Users specify number of reduce tasks `R` default technique: hashing.
    
    
### Hadoop
- Open source software framework designed for storage and processing of large scale data on clusters 
- Store in **HDFS** (Hadoop Distributed File System) and uses **MapReduce**.

<a href="https://ibb.co/G2g04Rd"><img src="https://i.ibb.co/QNsf3MJ/image.png" alt="image" border="0" width = "45%" height = "45%"></a>  <a href="https://ibb.co/WHw8GdR"><img src="https://i.ibb.co/cyHfkps/image.png" alt="image" border="0" width = "45%" height = "45%"></a>

- Default replication is **3-fold**.

- **Hadoop 1 Limitations**: Lacks support for Paradigms, Scalability (Max Cluster Nodes: 5000, Max Tasks: 40000), Axailabiliy, Hard Partition.
- **Schedulers**
    - **Hadoop Capacity Scheduler**: Multiple queues, Each queue contains multiple jobs & guaranteed some cluster capacity
    - **Hadoop Fair Scheduler**: all jobs get equal share of resources, As jobs arrive, each job given equal % of cluster
    - **Yarn Scheduler on Hadoop 2.x**: Treats each server as a collection of containers (fixed CPU + fixed memory)
      - Main components 
        - Resource Manager (RM) : Scheduling (Cluster resources)
        - Node Manager (NM) : server-specific functions (Each node resources)
        - Application Master (AM) : Container negotiation with RM and NMs, Detecting task failures of that job.
        - Extermely useful because it deals with data **IN ONE PLACE**.
     - To estimate time length: Calculate running time of task as proportional to size of its input.
 - **Fault tolerance in Hadoop**:
    - it comes with its cost!
    - Reading/writing to disk is 100 x slower than in memory
    - Network communication is 1000,000 x slower than in memory

### Spark
- Inherited from functional programming: **keep data in-memory and immutable**
- if task is done by two workers, only one takes effect, When a  Reduce task completes, (atomically) rename file to final.
- Fault tolerance is maintained by
    - keeping the **lineage** of transformations
    - when failures happen, **replay functions transformations** over original datasets
- Spark is **100x** faster than Hadoop
- **Fault tolerance in Spark**:
  - Server Failure
    1. NM heartbeats to RM
      - If server fails: RM times out & lets all affected AMs take appropriate action
    2. NM keeps track of each task running at its server
      - If task fails while in-progress, mark the task as idle and restart it
    3. AM heartbeats to RM
        On failure, RM restarts AM, which then syncs it up with its running tasks
  - RM Failure
    - Use old checkpoints and bring up secondary RM.
  - Worker failure:
    - Detect failure via periodic heartbeats
    - Re-execute both completed and in-progress map tasks
    - Re-execute only in progress reduce tasks
  - Master failure:
    - Could handle, but (master failure unlikely)
  - Stragglers (Slow Tasks):
    - Near end of phase, spawn backup copies of tasks & Whichever one finishes first, wins. Approach name's (Speculative Execution)


