### Time
- Time synchronization is required for both Correctness, Fairness.
- Physical Clock Systems
  - **TAI**: International Atomic Time = avg of cesium 133 clocks. 
  - **UTC**: Universal Coordinated Time = TAI ± Leap Second.
- **Cristian’s Algorithm for Time Synchronization**
  - External source `S` (May cause Single point of failure)
  - Denote clock value at process `X` by `C(X)`
  - Periodically, a process `P`:
    - send message to `S`, requesting time.
    - Receive message from `S`, containing time `C(S)`
    - Adjust `C` at `P`

<a href="https://imgbb.com/"><img src="https://i.ibb.co/2y95t8n/image.png" alt="image" border="0"></a>

- **The Network Time Protocol (NTP)**
  - The primary server at the root synchronizes with the UTC.
  - The next level contains secondary servers, which act as a backup to the primary server.
  - At the lowest level is the synchronization subnet which has the clients.

- **The Berkeley Algorithm for Synchronization**
  -  Uses an `elected master` to synchronize.
  - The elected master pools or broadcasts to all machines for their time, adjusts times received for RTT & latency, `averages` times, and tells each machine how to adjust.

- **Lamport’s notion of logical time**
  - Ordering of events is **needed** to avoid ambiguities.
  - All processes use a counter (clock) with initial value of zero.
  - The counter is incremented by and assigned to each event, as its timestamp.
  - A send (message) event carries its timestamp.
  -  For a receive (message) event the counter is updated by `Max(receiver-counter, message-timestamp) + 1`.

  <a href="https://imgbb.com/"><img src="https://i.ibb.co/yYJcPg6/image.png" alt="image" border="0" width="40%" height="40%"></a>
  <a href="https://imgbb.com/"><img src="https://i.ibb.co/nMB2pwF/image.png" alt="image" border="0" width="50%" height="50%"></a>
  
- **Vector Logical time**
  - All hosts use a vector of counters (logical clocks), `i`th element is the clock value for host `i`, initially all zero.
  - Each host `i`, increments the `i`th element of its vector upon an event, and assigns the vector to the event.
  - A send(message) event carries its vector timestamp (counter vector)
  - For a receive(message) event, 
	  - Max(receiver[j] , messag[j]),   if j is not self
		- receiver[j] + 1		otherwise
    
 <a href="https://imgbb.com/"><img src="https://i.ibb.co/5r2j0gm/image.png" alt="image" border="0"></a>
