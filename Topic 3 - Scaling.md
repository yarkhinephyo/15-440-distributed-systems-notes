**Types of scaling**

1. Scale up - Add more resources to each individual node.
2. Scale out - Add more nodes and spread load across them.

<ins>Types of scaling out</ins>

1. Scale horizontally - Add more nodes that share the same function.
2. Scale vertically - Split a task of a single node into subtasks assigned to different nodes.

**Virtual Machine**

Software abstraction of OS-visible hardware. A virtual machine monitor implements the abstraction, to multiplex hardware among multiple VMs.

Type 1 hypervisor talks directly to hardware and type 2 hypervisor runs as an application inside a conventional OS.

**Container**

Containers run in the user space. They are isolated instances of programs. Instances only see the resources assigned to them.

However, containers have a more complex interface than VMs. They are harder to migrate. Container states can also leak into the host OS.

**Heuristics for Scaling**

- Monitor queue length.
- Use weighted moving averages.
- React faster to load increases than decreases.
- Predict today's workload from last week's load.

**Scaling by Cloud Providers**

SLAs that provide response time distribution. For example, 90% of responses in less than 200 ms time.

**Amdahl's Law**

Theoretical speed up is limited by the part of the task that cannot be parallelized.

![](images/Pasted%20image%2020230429133018.png)

**Scaling a Website**

<ins>1-tier Website</ins>

![](images/Pasted%20image%2020230429133130.png)

- Easy to add content but limited storage.
- Painful to maintain user accounts in the local disk.

<ins>2-tier website</ins>

![](images/Pasted%20image%2020230429133345.png)

- Improves administration with the database.
- More storage for content scalability.
- Web server likely to be the bottleneck as generating dynamic content consumers CPU cycles.

<ins>3-tier Website</ins>

![](images/Pasted%20image%2020230429133741.png)

- Adds a lot of processing power for application.
- Database is likely to be the bottleneck. One solution is to use databases with stringent consistency only for critical data. Another solution is to add a cache in front of the database.

**Scaling Simple Echo Server**

- Single-threaded implementation as baseline.
- Multi-threaded implementation offers higher throughput but fails at 2000 concurrent clients.
- Single-threaded epoll implementation scales to 5000 concurrent clients but offers lower throughput.
- Multi-threaded epoll is possible but is not shown.

![](../Pasted%20image%2020230429135546.png)