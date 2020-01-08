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





