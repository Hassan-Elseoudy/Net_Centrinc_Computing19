### Naming
- Identifier – a reference to an entity that is often unique and never reused.
- The name of entity is independent of its address.
- An identifier (name) refer to only one and same entity.

### Namespace
- The way that names in a particular system are organized. 
- The set of all possible names.
- Name space is a `directed graph` with a **single root node**.
- Direct graph:
  - **root node**.
  - **leaf nodes**: information on an entity.
  - **directory nodes**: a collection of named outgoing edges (which can lead to any other type of node).
- Examples
  - File system is a name space where leaf is a file.
  - Directory node represents file directory.
  - URL is identifier name for web services.
- Distrbution
  - **Global Layer**: It is the root node, not changed, It representes organizations (`.gov`, `.mil`, `.edu`)
  - **Adminstartional Layer**: Represents departments in such organization, relatively stable (`.eng`, `.cs`)
  - **Managerial layer**: Nodes change regularly, Represents shared files.
  
  <a href="https://ibb.co/7nJpjp2"><img src="https://i.ibb.co/bsgvQvz/image.png" alt="image" border="0">

### Name resolution
- The process of looking up a name is called name resolution.
- Two Common Approaches:
  1. Iterative Name Resolution. (Useful in LAN)
  2. Recursive Name Resolution. (Useful in WAN)

<a href="https://imgbb.com/"><img src="https://i.ibb.co/7KvwTtC/image.png" alt="image" border="0" width="47%" height="47%"></a>
<a href="https://imgbb.com/"><img src="https://i.ibb.co/1019vRr/image.png" alt="image" border="0" width="47%" height="47%"></a>

### Domain Name System (DNS)
- A subtree within DNS is referred to as a “domain”.
- A path name is referred to as a “domain name”.
- These can be relative or absolute.
- A DNS server operates at each node (except leafs).  Here, the information is organised into **resource records**.
- Root Name Severs: 13 World wide 13 root name servers, {a, b, c, … , m}.root-servers.org {Dubai, Paris, Monterry, NY, etc.)
- How to get to an IP?
  1. An application program on a host accesses the domain system through a DNS client, called the **resolver**.
  2. Resolver contacts DNS server, called **name server**.
  3. DNS server returns IP address to resolver which passes the IP address to application.

<a href="https://imgbb.com/"><img src="https://i.ibb.co/vqLbvMn/image.png" alt="image" border="0"></a>
