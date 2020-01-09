## Election in Distributed Systems

#### Garbage Collection 
An object is considered as **garbage** if there are no longer any references to it anywhere in distributed system

#### Bully algorithm
- The process `P` sends election message to **all processes with higher number**
  - If no one answer, `P` wins
  - If one answer, it takes over
- Message types
  - coordinator: announcement to all processes with lower IDs.
  - election: sent to processes with higher IDs.
  - answer: answer to election.
  
<a href="https://imgbb.com/"><img src="https://i.ibb.co/pjBx85K/image.png" alt="image" border="0"></a>

#### Ring Election
- `N` Processes are organized in a logical ring.
- All messages are sent clockwise around the ring. 
- Any process that discovers a coordinator has failed initiates an `election` message that contains its own `id`.
- When a process receives an election message, it compares the `id` in the message with its own.
  - If the arrived `id` is greater, the receiver `forwards` the message.
  - If the arrived `id` is smaller and the receiver has not forwarded an election message earlier, it substitutes its own `id` in the message and forwards it. 
  - If the arrived `id` is that of the receiver
    - it becomes the new coordinator.
    - This process then sends an `elected` message to its neighbor announcing the election result.
- When a process `i` receives an elected message, it sets its variable elected = `id` of the message & forwards the message if it is not the new coordinator.
- Worst case O(3N - 1)

<a href="https://ibb.co/G35ST6y"><img src="https://i.ibb.co/Vpq4m1R/image.png" alt="image" border="0"></a>

#### Election in Google Chubby 
- Master lease can be renewed by the master as long as it continues to win a **majority voting** each time
- Ensures automatic re-election on master failure

### Mutual Exclusion
- Semaphores, mutexes, etc. in local operating systems.
- Message-passing-based protocols in distributed systems:

#### Centralized Algorithm
- A central coordinator 
  - Grants permission to enter process & keeps a **queue** of requests to enter the other processes.
  - Ensures only one process at a time can access the data
  - To enter a process Send a request to the server & wait for token.
  - On exiting the CS Send a message to the server to release the token.
- **Features**: Safety, liveness and order are guaranteed.
- **Disadvantages**: The coordinator becomes performance bottleneck and single point of failure.

<a href="https://imgbb.com/"><img src="https://i.ibb.co/m9Jzyqm/image.png" alt="image" border="0"></a>

#### Distributed Algorithm
- The process send message with `critical region`, `process number`, and `current time` to all other process (multicast)
- For all ather processes:
  - If the receiver in not in critical region and does not want it, send `OK`
  - If receiver is in critical region, `not reply`
  - If receiver wants to enter critical region, compares `time stamp`, **lowest** one wins

<a href="https://imgbb.com/"><img src="https://i.ibb.co/yQjBwqc/image.png" alt="image" border="0"></a>

#### Token-Ring Algorithm
- Wait for token to pass, save it to `enter()`, release it to neighbor when done

<a href="https://imgbb.com/"><img src="https://i.ibb.co/bskdh3N/image.png" alt="image" border="0"></a>

<a href="https://imgbb.com/"><img src="https://i.ibb.co/Ltp3T3y/image.png" alt="image" border="0"></a>





