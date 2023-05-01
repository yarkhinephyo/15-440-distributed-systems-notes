**Federated System**

There are clients and servers. Allows delegation of authority across organization boundaries. For example, DNS has a chain of delegation from the root server.

**P2P System**

Every node is equal. For example, Exterior Gateway Protocol is a mechanism for combining computer networks with each being run by a different organization.

<u>EGP</u>

Each autonomous system has one or more gateways. Each gateway is configured with a set of neighbors.

If a node has an update, it only sends the update to neighbor nodes in an "overlay" graph. The cost is distributed over all nodes and transmissions occur in parallel.

**Overlay Networks**

Define a routing graph among physical hosts. Communicate with only nodes that shared an edge.

Enables store-and-forward propagation to spread update load over the entire network. Abstracts away the physical network location. 

However, the overlay topology may not match the physical topology which may increase latency. The double layer routing tables also means more components prone to failure.

**Onion Routing**

Uses an overlay network. Wraps TCP stream in three layers of encryption. Each relay can only decrypt one layer to learn the next destination.

![](images/Pasted%20image%2020230430183049.png)

**P2P Storage**

Identifies files by the cryptographic hash of the contents. Automatically assign files to nodes in an overlay network.

**BitTorrent**

<u>With Tracker</u>

1. Node contacts tracker to get the list of peers.
2. Node contacts peers and requests chunks in parallel.
3. Node will serve other peers at the same time.

<u>Without Tracker</u>

Without tracker, a directory is needed to figure out what files map to what peers.

A distributed hash table to store the peers for a particular chunk. BitTorrent uses "infohash" for each torrent which includes the hash of every chunk of the content.

![](images/Pasted%20image%2020230430184709.png)

**DHT - Chord**

![](images/Pasted%20image%2020230430185505.png)

Structured as a ring, corresponding to hash space of key. Items are stored in the successor nodes. For example, key 12 is stored in node 19.

Each node contains "finger tables" that tracks successor at +1, +2, +4, +8... positions to improve the lookup to log(n) complexity.

When a new node joins the system, it finds the position in the ring and takes responsibility of a subset of items from its successor. All the finger tables are updated.

Replication can be done by storing copies on subsequent successor nodes.

**DHT - Kademlia**

Each node tracks up to "k" number of nodes for each bit in the node ID. For the example below, node 110 tracks { 111 }, { 100, 101 } and { 000, 001 }.

The tracked nodes at each bit have:

1. Different value for the bit.
2. The same value for the bits on the left.

![](images/Pasted%20image%2020230430190403.png)

The lookup process is as follows:

1. Contact any node with the hash of the content.
2. The node either returns the data or the addresses of "k" nodes close to the hash.

**Append-Only Ledger**

Each record is digitally signed and includes cryptographic hash of a previous record. Once a record is public, it is not possible to forge the previous records.

<u>Nakamoto Consensus</u>

- Solves who gets to write the next record for a distributed ledger.
- Makes all nodes solve a difficult computational problem. 
- Provides incentive for strangers to join so that it is hard for malicious actors to control more than a small fraction of the nodes.

