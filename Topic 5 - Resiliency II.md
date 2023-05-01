**Two-Phase Commit Protocol**

Simplest of many consensus protocols. 2PC aims for the highest level of consensus - <ins>unanimity</ins>.

![](images/Pasted%20image%2020230430104612.png)

If a site votes "Yes", it is blocked indefinitely until the outcome is communicated by the coordinator.

The protocol prioritizes safety over liveness.

**Replica Control Algorithms**

Transparent data replication requires one-copy semantics which is achieved via replica control algorithm. However, consistency is achieved by losing availability in the presence of network partitions. Else, by increasing latency.

![](images/Pasted%20image%2020230430105905.png)

**Weighted Voting by Gifford**

Peer-to-peer voting scheme, there is no master. Pessimistic replica control algorithm. Generalization of "read-one, write-all" scheme.

1. Each replica has a version number. Timestamps can be used for this.
2. Each replica is assigned a number of votes.
3. For read, contact as many replicas as possible. If votes > read quorum, use the content from the replica with the highest version.
4. For write, contact as many replicas as possible. If votes > write quorum, use two-phase commit for the update.

<ins>Read-quorum + Write-quorum > Sum-of-all-votes</ins> - Ensures that each read contains at least one replica with the latest update.

<ins>Write-quorum > Half-of-all-votes</ins> - Ensures that the writes require the majority of votes.

If the write-quorum is higher, the availability of writes will be lower and the availability of reads will be higher.

**Master-Slave Replication**

The master handles all updates, the slaves only handle reads.

<ins>Read-Only Master-Slave Replication</ins>

Asynchronous updates to slaves allows for stale reads. There are no update conflicts.

<ins>Read-Write Master-Slave Replication</ins>

Slave servers cache from the master server. Cache consistency protocols such as callbacks and leases can be used. There are no update conflicts and no stale reads.

Good option when the inter-server network is better than the server to clients.

**Paxos**

Leader election that achieves a weaker consensus - <ins>simple majority</ins>.

- At most one node is elected as the leader.
- Majority of the nodes accept the new leader.
- Guarantees safety but not liveness.

Any node can play the role of proposer and acceptor. The proposer must respect any commitments made earlier. The acceptor must store commitments in a stable storage.

<ins>Steps</ins>

![](images/Pasted%20image%2020230430120029.png)
