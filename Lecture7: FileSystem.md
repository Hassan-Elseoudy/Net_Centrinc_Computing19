## File System

### File
- A file is a collection of data with a user view (file structure) and a physical view (blocks).
- Files contain both data and attributes 
- File = Name + Attributes + Data
- A directory is a file that provides a **mapping from text names to internal file identifiers**.
- Contents:
  - **Timestamps**: creation, read, write, header
  - **File type**: e.g., .c, .java
  - **Access Control List**: who can access this file and in what mode
  
### File System
- File system is the **interface to disk storage**
- File systems implement **file management**:
  - Naming and locating a file
  - Accessing a file – create, delete, open, close, read, write
  - Physical allocation of a file.
  
### Distributed File System
- File system with **distributed storage and users**. 
- Files may be located remotely on servers.
- Examples: NFS & AFS
- **Architecture**:
  - **Client Server Architecture**: Network File System (NFS)
  - **Cluster Based Architecture**: Google File System (Has 2 types)
    1. distributing whole files across several servers.
    2. striping files for parallel access.
- **Concurrent Accesses in DFS**
  - **One-copy update semantics**: when file is replicated,it has no different from when the file has exactly 1 replica.
  - At most once operation vs. At least once operation
- **Requirements**
  - **Access transparency**: A single set of operations is provided for access to local/remote files.
  - **Location Transparency**:  All client processes see a uniform file name space.
  - **Migration Transparency**: When files are moved from one server to another, users should not see it
  - **Performance Transparency**
  - **Scaling Transparency**
  - **File Replication** : A file may be represented by several copies for service efficiency and fault tolerance.
  - **Concurrent File Updates**: Changes to a file by one client should not interfere with the operation of other clients simultaneously accessing the same file.

### Network File System (NFS)
- Unix-based.
- In NFS, each file server provides a view for its local file system
- NFS can use both TCP and UDP
- NFS come with communication protocol allows clients with different OS and machines to access files on server is called **Open Network Computing Protocol ONC**
- Independent of OS
- NFS Access
  - **Remote Access model**: that client request to file client unaware of actual location of file. (Left)
  - **Upload/download model**: is that client download file from server and access it locally. (Right)
  <a href="https://ibb.co/gSk1k6W"><img src="https://i.ibb.co/ZBqsqNg/image.png" alt="image" border="0"></a>
- Client in NFS
  - Integrated with the kernel.
  - Transfers blocks of files to and from server via RPC. 
  - Caches the blocks in the local memory.
  - May support file descriptors
- Server in NFS
  - Mounting of sub-trees of remote filesystems by clients is supported by a separate mount service process on each NFS server.
- NFS Communications (Iterative V3 vs Recursive V4)

<a href="https://ibb.co/b6y00yC"><img src="https://i.ibb.co/rQLjjLz/image.png" alt="image" border="0" width = "50%" height="50%"></a>

- Naming in NFS

<a href="https://ibb.co/56y3nCg"><img src="https://i.ibb.co/g3p8PQL/image.png" alt="image" border="0" width = "50%" height="50%"></a>

- File Handlers in NFS
  - In Unix, file handle references a file in NFS , created by server (128 byte in V4)
- NFS Operations

  <a href="https://ibb.co/fHW4yF2"><img src="https://i.ibb.co/w4qMPgR/image.png" alt="image" border="0"></a>
  
- File Attributes in NFS
  - **TYPE**: The type of the file (regular, directory, symbolic link)
  - **SIZE**: The length of the file in bytes
  - **CHANGE**: Indicator for a client to see if and/or when the file has changed
  - **FSID**: Server-unique identifier of the file's file system
- Semantics of File Sharing
  - **UNIX semantics**: Every operation on a file is instantly visible to all processes
  - **Session semantics**: No changes are visible to other processes until the file is closed
  - **Immutable files**: No updates are possible; simplifies sharing and replication
  - **Transaction**: All changes occur atomically
- Server Caching (3 Methods)
  - **delayed-write**: new contents are written back to the disk only when the buffer page is required.
  - **Unix sync operation**: writes pages to disk every 30 seconds
  - **write-through**: data in write operations is stored in the memory cache at the server and written to disk before a reply is sent to the client.

<a href="https://ibb.co/mHFjW2V"><img src="https://i.ibb.co/CnscGY3/image.png" alt="image" border="0" width = "50%" height="50%"></a>
