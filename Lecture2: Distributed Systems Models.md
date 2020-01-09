### Distributed Systems
- A distributed system is a collection of independent computers that appears to its users as a single system.

### Distributed Systems Models
- Physical Models
  - Describe the hardware composition of a system
- Architectural models
  - Describe computational and communication tasks performed by its computational elements
  - E.g., Client-Server and Peer-to-Peer
- Fundamental Models
  - Describe solutions to individual issues faced by most distributed systems.
  - E.g., interaction (timing), failure, and security models.
  
  <a href="https://imgbb.com/"><img src="https://i.ibb.co/2dsSD3H/image.png" alt="image" border="0"></a>
  
### Distributed Systems Properties
- **Connect** users and resources
- **Transparency**: To hide the fact that machines are physically distributed and how much the distributed system appears as single system

<a href="https://ibb.co/TP1bFsz"><img src="https://i.ibb.co/DwY8SZ3/image.png" alt="image" border="0"></a>
  - **Note**: Replication transparency is the term used to describe the fact that the user should be unaware that data is replicated

- **Scalability**: System scalability to size means easily add more users & resources.
  - Problems
    - Machines make decisions based only on local information.
    - Failure of one machine does not ruin the algorithm.
- **Openness**: means easy to configure system for different developers.
- **Reliability**: Distributed system should be more reliable than single system.
- **Fault Tolerance**
  - Fault detection (Checksums, heartbeat)
  - Fault masking (Retransmission of corrupted messages, redundancy)
  - Fault toleration (Exception handling, timeouts)
  - Fault recovery (Rollback mechanisms)
- **Security**
  - Confidentiality (protection against disclosure to unauthorized individuals).
  - Integrity (protection against alteration or corruption).
  - Availability (protection against interference with the means of accessing the resources).
  
### Hardware Architecture
  - Multiprocessors (*Tightly coupled* -> {short delay, high data rate}, Shared memory)
    - Bus-based: cache memory, hit rate.
    - Switch based.
  - Multicomputers (*Loosely coupled* -> {long delay, low data rate}, Private memory)
    - Bus-based
    - Switch-based

### Software Concepts

<a href="https://imgbb.com/"><img src="https://i.ibb.co/MCsL797/image.png" alt="image" border="0"></a> 

### Distributed shared memory
(DSM) provides the illusion of a single shared memory: it spares the programmer the concerns of message passing. in Tightly coupled Systems.

### Network Operating Systems
- loosely-coupled software on loosely-coupled hardware.
- A network of workstations connected by LAN.
- each machine has a high degree of autonomy.

### Distributed Operating Systems
- a single, global interprocess communication mechanism.

### Middleware
- a software layer that provides a programming abstraction to mask the heterogeneity of the underlying platforms (networks, languages, hardware)
- E.g., CORBA, Java RMI

<a href="https://ibb.co/rbTwr6B"><img src="https://i.ibb.co/HN1H8zc/image.png" alt="image" border="0"></a>
 
  
  
