## Types of communications paradigms.

### Direct communication (Coupled)
- **Interprocess communication** (Low-Level & Doens't hide distibution aspects)
  - **Message Passing**
    - Main 2 operations (Send & Receive)
    - It may be Synchronous and asynchronous.
      * Synchronous: Both send and receive are **blocking** (When sending / receiving)
      * Asynchronous: The send operation is **non-blocking**. The receive operation can be **either** blocking (Most Used) or non-blocking
    - Message Destination: (Internet address, local port) pairs.
      - Port: one receiver but can have many senders **except: Multicast ports**
      - Internet address: client uses a **fixed Internet address** to refer to a service, then the service has to always run on the same computer. *Solution (location transparency)*
    - Reliability 
      - Validity: messages are guaranteed to be delivered with ‘reasonable’ lost.
      - Integrity: messages must arrive uncorrupted and **without duplication**.
    - Ordering: **failure** if a sender messages are received **out of order**. (TCP ensures oredering
  - **Socket Programming**.

- **Remote Invocation** (Request-Reply Protocol / Access & Location Transparency / Most common used in DS)
  - **RPC (Remote procedure call)**
    - Procedures in processes on remote computers can be called as if they are procedures in the local address space.
    - Call from one function to another function, where caller and callee function reside in different processes.
    - underlying RPC system hides important aspects of distribution (e.g. encoding and decoding of parameters and results)  
    <a href="https://ibb.co/CKwxJqb"><img src="https://i.ibb.co/WvHSDQk/image.png" alt="image" border="1"></a>
  - **RMI (Remote Method Invocation)**
    - Resembles remote procedure calls but in a world of distributed **objects**

### Direct communication (Decoupled)
- **Indirect Communication** (strong degree of *decoupling* between senders and receivers in time & space)
  * Space decoupling: Senders do not need to know who they are sending to
  * Time decoupling: Senders and receivers do not need to exist at the same time
  * Example: **Publish-Subscribe (Event based Architecture)**
     * Processes communicate through events propagation (Middleware make sure events are being recived)
     
## Consenus
#### Agreement: processes to agree on a value after one or more of the processes has proposed what that value should be
- Examples
  - mutual exclusion: agree on which process to enter critical section
  - election: agree on which is the elected process
### Consensus in Synchronous Systems
- Synchronous DS / Reliable channels / Crash failures of up to **f of the N processes**.
- Algorithm used in Consensus: `( f + 1)` rounds 
> - At each round of `( f + 1)` round, each process does the following:

     - It multicasts the set of values known to process `i` that it has not sent in previous rounds
     - Then it records any new values delivered from other’s multicasts
>  - After `( f + 1)` rounds, all correct (non-faulty) processes arrives at the same set of values (they all can select the minimum for example)

   ### Consensus using Paxos
- Used when: (DS is eventually synchronous & Minority of processes can crash)
- How it works?
  - Work on rounds
  - In each round we have **one proposer (leader)**, others are **acceptors (witnesses)**.
  - Each round has **three phases**:
    - Prepare/Promise (request leadership, learn what witnesses have seen, 
    - Proposal/Acceptance (select a value)
    - Decision (only if **majority accepts proposal**)
- Problems?
  - Processes have to know each other.
  - failures are **not allowed**.
  - To overcome we can use **BLOCKCHAIN** (Like in Bitcoins).







  

  
