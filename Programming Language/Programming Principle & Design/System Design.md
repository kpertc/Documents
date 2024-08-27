#IT

### Tutorial
[System Design Course for Beginners](https://www.youtube.com/watch?v=MbjObHmDbZo&t=303s)

### Distribute Systems

![[Distributed System.jpg]]

-   Fallacies of Distributed Systems
-   Network is reliable
-   Latency is zero
-   Bandwidth is infinite
-   Transport cost is zero
-   Topology doesn't change
-   network is secure
-   only one administrator
  
### Distributed System Characteristics
-   No shared clock
-   No shared memory
-   Shared resources
-   Concurrency and Consistency
  
### Distributed System Communication
-   Different parts of Distributed System need to be able to talk
-   Requires agreed upon format or protocal

### Benefits
-   More reliable, fault tolerant (system will not creash by a single server crashed)
-   Scalability
-   Lower latency, increased performance (when server distributed everywhere)
-   Cost effective

# System Design Performance Metrics

##### Scalability
-   Ability of a system to grow and manage increased traffic
-   Increased volume of data or requests

##### Reliability
-   Probability a system will fail during a peroid of time
-   Slightly harder to define than hardware reliability

> [!tip] **Mean Time Between Failure**
> MTBF = ( Total Elaspsed Time - total downtime ) / number of failures
> ( 24 hrs - 4 hrs downtime ) / 4 failures = 5 hrs MTBF

##### Avaliability

-   Amount of time a system is operational during a period of time
    
-   Poorly designed software requiring downtime for updates is less available

> [!tip] **Availability Calculation**
> Availability % = ( avaiable time / total time ) x 100
> ( 23 hrs / 24 hrs ) x 100 = 95.83%

![[Availability.png]]

##### Reliable vs Available
-   Reliable system is always an available system
-   Availability can be maintained by redundancy, but system may not be reliable
-   Reliable software will be more profitable because providing the same service requires less backup resources
-   Requirement will depend on the function of the software

##### Efficieny
-   How well the system performs -> performance bottle neck
-   Latency and throughout are often used as metrics

##### Manageability
-   Speed and difficulty involved with maintaining system
-   Observably, how hard to track bugs
-   Difficulty of deploying updates
-   Want to abstract infrastructure away, so product engineers don't have to worry about it

### Latency Numbers

![[Latency-number-1.png]]
![[Latency-number-2.png]]

### Lactency Key Takeaways
-   Avoid Network calls whenever possible
-   Replicate data across data centers for disaster recovery as well as performance
-   Use CDNs to reduce latency
-   Keep frequently accessed data in memory if possible rather than seeking from disk, caching

> [!tip] **Data Conversions**
>8 bits -> 1 byte
>1024 bytes -> 1 Kilobyte
>1024 Kilobytes -> 1 Megabyte
>1024 Megabytes -> 1 Gigabyte
>1024 Gigabytes -> 1 Terabtye

> [!tip] Common Data Types
>Char - 1 byte
>Integer - 4 bytes
>UNIX Timestamp - 4 bytes

> [!tip] Time
>60 secs x 60 mins = 3600 secs per hour
>3600 x 24 hrs = 86400 secs per day
>86400 x 30 days = 2500000 secs per mons  

### LB Routing Methods

#####   Round Robin
-   Simplest type of routing
-   Can result in uneven traffic

#####   Least Connections
-   Routes based on number of client connections to server
-   Useful for chat or streaming applications

#####   Least Response Time
-   Routes based on how quickly servers respond

#####   IP Hash
-   Routes client to server based on IP
-   Useful for stateful sessions

  

### L4 vs L7

**Layer4**
-   Only has access to TCP and UDP data
-   Faster
-   Lack of information can lead to uneven traffic

**Layer7**
-   Full access to HTTP protocol and data
-   SSL termination
-   Check for authenticaion
-   Smarter routing options

Redundant LB Setup
![[Redundant LB Setup.png]]

### Caching
Improve performance and save money
![[Caching.png]]


### Speed and Performance
-   Reading from memory is much faster than disk, 50-200x faster
-   Can serve the same amount of traffic with fewer resources
-   Pre-calculate and cache data
-   Most apps have fat more reads than writes, perfect for caching    


### Caching Layers

DNS, CDN, Application, Database
![[Caching-Layers.png]]

##### Distributed Cache
Works same as traditional cache
Has built-in functionality to replicate data, shard data across servers, and locate proper server for each key


##### Cache Eviction
Preventing stale data
Caching only the most valuable data to save resources



##### Time to Live, TTL
Set a time period before a cache entry is deleted
Used to prevent stale data

  

##### Least Recently Used, LRU
Once cache is full, remove the last accessed key and add a new key

  

##### Least Frequently Used, LFU
-   Track number of times key is accessed
-   Drop least used when cache is full

  

### Caching Strategies
-   Cache Aside - most common
-   Read Through 从缓存中读
-   Write Through
-   Write Back
  

### Cache Consistency
-   How to maintain consistency between database and cache effciently
-   Importance depends on use case

  
# Database Scaling
Most web apps are mostly read heavy, around 95%+


### Basics Scaling Techniques
-   Indexes
-   Denormalization
-   Connection pooling
-   Caching
-   Vertical scaling