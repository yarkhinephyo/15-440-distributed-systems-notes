**Cache Metrics**

1. Miss ratio = Misses / References
2. Hit Ratio = 1 - Miss ratio
3. Expected cost of reference = (Miss ratio x Cost of miss) + (Hit ratio x Cost of hit)
4. Cache Advantage = Cost of miss / Cost of hit

**Double Win of Caching**: Caching site wins by avoiding end-to-end latency. The rest of distributed system also wins due to lower utilization of shared resources such as network and server load.

**Full replication**

- Storage for the entire subtree consumed on every replica.
- High traffic on hotspots.
- Machines receive updates whether they care or not.

**On-demand caching**

- Fetch file only if needed.
- Requires integration with the operating system.

![](images/Pasted%20image%2020230429112607.png)

**One-copy Semantics**

A caching system has one-copy semantics if are no externally observable functional differences relative to the same system without caching.

<u>Difficult in practice</u>

- Physical master copy may not exist.
- Network may break between some users and master copy.
- There may be intense read or write sharing which generates cache propagation traffic.

**Caching Policy 1 - Broadcast Invalidation**

Every cache site is notified on updates. No checks to verify it the site actually contains object. At the cache site, the next reference to the object will cause a miss.

Strict emulation of "one-copy semantics" but not a scalable design.

**Caching Policy 2 - Check on use**

Reader checks master copy before each use. Has to be done at coarse granularity such as "session semantics" to avoid reading from the server every call.

Server does not need to know of caching sites and there is strict consistency at coarse granularity. However, checks are almost always successful which slows read access on loaded servers.

**Caching Policy 3 - Callback**

Targeted notification of caching sites on updates. Typically done at coarse granularity. Biases read performance in favor of write performance.

Zero network traffic for reading cache-valid objects. However, the server has to maintain state and there is complexity of tracking cached state on clients. Silence is also ambiguous for client.

**Caching Policy 4 - Leases**

Caching site obtains finite-duration control from master copy. Leases have to be renewed. Assumes that clocks tick at the same rate everywhere.

![](images/Pasted%20image%2020230429115927.png)

**Caching Policy 5 - Turn off caching during write-sharing**

When write-sharing is detected, turn off caching everywhere.

Precise one-copy semantics but the server has to be aware of every use of data.

**Caching Policy 6 - Faith-Based Caching**

Blindly assume that cached data is valid for a while. Periodically check for stale data.

Simple implementation but only provides a weak approximation to one-copy semantics. (Consistency offered by DropBox)

**Caching Policy 7 - Pass the Buck**

Let the user trigger cache invalidation. Otherwise, cache is assumed to be valid.

Trivial to implement but places burden on user.

**Prefetching**

Requires a concept of "Nearby" or "Next" for it to work. For example, files in the  same directory, successive elements in a linked list.

Initiates fetch of data in advance of need. If completion of fetch occurs before need, there is complete masking of latency. If it occurs after need, there is still reduced effective latency.

However, erroneous commitment will increase latency instead. For example, by delaying demand requests behind prefetching traffic. To solve this, the server can maintain separate queues. However, packets in the network will still cause the same problem in routers.

<u>When to use prefetching</u>

![](images/Pasted%20image%2020230429122250.png)

