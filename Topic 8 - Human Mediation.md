**Append-Only DAG**

Similar to Append-Only Ledger but a record can have more than one parent. In Git, Append-Only DAG is the implementation of the <u>commit history</u>. If a commit has two parents, it means that two branches joined together.

**Merkle Tree**

Hashes point towards leaves instead of parents. Represents a file tree in distributed version control (DVC).

![](images/Pasted%20image%2020230430213419.png)

**Sync Operation in DVC**

1. Receiver tells sender which branches it has. 
2. For each branch in common, the sender computes which commits the receiver does not have.
3. For each branch not owned by receiver, the sender computes the youngest ancestor commit that the receiver has.
4. Sender transmit everything the receiver does not have.

**ActivityPub**

Protocol behind the decentralized social network.

<u>Follow Request</u>

Following actor and followed actor on different servers.

![](images/Pasted%20image%2020230430211354.png)

<u>Post Distribution</u>

Home instance for the user tracks all his followers. For each remote server with followers, retrieve the user details and post to their inboxes.

<u>Post Boosting</u>

Announcing instance tells the followers from remote instances to fetch the data from the owner instance.

![](images/Pasted%20image%2020230430211824.png)
