## Replication
- Replication is Maintenance of copies at multiple sites 
- Advantages of replications
  - Performance Enhancement
    - Dividing the work among multiple servers (load balancing - scalability)
    - Geographically replicated server
    - Caching of data (e.g., proxy servers, DNS)
  - Increased Availability
    - time for which a service is accessible with reasonable response times
    - the availability of an object replicated on all servers is `(1 – p)^n`
    - **Note**: caching does not count as a method of increasing availability
  - Fault Tolerance
    - Stronger than availability
    - guarantees strictly correct behavior despite a certain number and type of faults.
    - Probability of failure `(1 / n - 1)` n: number of copies.
> Your boss says to you, “Our system is too slow, make it faster.”
You decide that replication of servers is the answer. What do you do next? What are the questions that need to be answered?
Where to place servers?
Where to place content?

  - Placing server
    - We use minimum k-median greedy algorithm.
  - Permenant replicas
    - Initial set of replicas, Other replicas can be created from them
- Requirements
  - **Replication transparency**: Clients should not be aware that multiple copies of the data exist with same experience.
  - **Consistency**
    - **Impractical definition**: copies are always the same.
    - **Practical definition**: the operations performed replicated objects meet the specification of correctness (consistency models).
- Shared Objects Replicas
  - There are **physical copies** (replicas) of **logical objects** in the system.
  - Operations are specified on **logical objects**, but translated to operate on physical objects.
  <a href="https://ibb.co/kJkQBC7"><img src="https://i.ibb.co/MfWMS0v/image.png" alt="image" border="0"></a>
  
### Replica Managers 
  - an RM contains replicas on a computer and access them directly
  - RMs apply operations to replicas recoverably
  - objects are copied at all RMs unless stated otherwise
  - static systems are based on a fixed set of RMs

### Basic Mode of Replication
  - Replication Transparency
    - User need **not** know that multiple physical copies of data exist.
  - Replication Consistency
    - Data is consistent on all of the replicas

### Transaction using Replication
  - **One-copy serializability**: The effect of transactions performed by clients on replicated objects should be the same as if they had been performed one at a time on a single set of objects (i.e., 1 replica per object).

### Handling Requests on a Replicated Object
  1. Request: a request is issued to **one or more replica manager**.
  2. Coordination: replica managers coordinate to decide.
    - **FIFO ordering**: Clock Synchronous.
    - **Causal ordering**: Asynchronous (e.g. Lampart).
  3. Execution: execute the request (atomically)
  4. Agreement: reach a consensus on the final decision (e.g., committing/aborting a transaction).
  5. Response: One or more replica managers responds to the front end.
  
### Consistency Models
  - **Strict consistency**
    - **Impossible** to implement in a distributed system !
    - assumes all writes are instantaneously visible to all processes.
    - A replicated shared object service is **linearizable** if for any execution, there is some interleaving of operations issued by all clients with the real times at which each operation occurred during the execution 
    - Any `R(x)` returns a value corresponding to most recent `W(x)`
    - (a) Strict Consistent (b) Non-Strict Consistent
    
<a href="https://ibb.co/6WdTTBj"><img src="https://i.ibb.co/hmq44f3/image.png" alt="image" border="0" width="50%" height="50%"></a>
   
  - **Sequential consistency**
    - is consistent with the program order in which each individual client executes those operations.
    
<a href="https://ibb.co/f0c2MLm"><img src="https://i.ibb.co/3hJ71Qt/image.png" alt="image" border="0" width="50%" height="50%"></a>
   
  - **Casual consistency**
    - Writes that are potentially casually related must be seen by all processes in the same order.
    - Concurrent writes may be seen in a different order on different machines.
    
<a href="https://ibb.co/XxSjpsn"><img src="https://i.ibb.co/N2Ztpj0/image.png" alt="image" border="0" width="50%" height="50%"></a>

  - **FIFO consistency**
    - Writes done by a single process are seen by all other processes in the order in which they were issued.
    - but writes from different processes may be seen in a different order by different processes.
    
<a href="https://imgbb.com/"><img src="https://i.ibb.co/bsRXtf4/image.png" alt="image" border="0" width="50%" height="50%"></a>
    
  - **Weak consistency**
    - No operation on a synchronization variable is allowed to be performed until all previous writes have been completed everywhere.
    - but writes from different processes may be seen in a different order by different processes.
    
<a href="https://ibb.co/z5FShY5"><img src="https://i.ibb.co/vBhJxGB/image.png" alt="image" border="0" width="50%" height="50%"></a>  
  
  - **Release consistency**
    - Before a read or write operation on shared data is performed, all previous acquires done by the process must have completed successfully.
    - Before a release is allowed to be performed, all previous reads and writes by the process must have completed
    - **Eager** 
        - After a process is granted `Acquire`:It can perform reads & writes locally
        - After `release`: the updates are propagated and each recipient responds with an ACK
        - After all processes ACK, the sync. manager is informed of the `Release` 
    - **Lazy**
        - Upon Release, nothing is sent out.
        - Upon Acquire, the process has to get the most recent values of the required data
    
    <a href="https://ibb.co/hXx1yGT"><img src="https://i.ibb.co/dbsJrNH/image.png" alt="image" border="0" width="50%" height="50%"></a>
    
### Monotonic Reads vs Write
  <a href="https://imgbb.com/"><img src="https://i.ibb.co/RBNgKyT/image.png" alt="image" border="0" width="50%" height="50%"></a>
  <a href="https://imgbb.com/"><img src="https://i.ibb.co/hywQ6yY/image.png" alt="image" border="0" width="50%" height="50%"></a>
  
### Write follows Reads
  - Any successive write will be performed on a copy that is up-to-date with the value most recently read by the process.
  <a href="https://imgbb.com/"><img src="https://i.ibb.co/4JJ0PC0/image.png" alt="image" border="0" width="50%" height="50%"></a>




