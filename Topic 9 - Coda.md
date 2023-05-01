**Disconnected Operation in Coda**

Masks temporary isolation from servers by exploiting caching for availability.

<u>Hoarding</u>

Minimize the cost of disconnected cache misses by filling up the cache with high utility objects. The priority is calculated by combining a user-specified score and LRU reference score.

<u>Emulation</u>

If there are updates, they are buffered until the connectivity is restored. Client modification log (CML) is recorded in persistent storage.

If there are cache misses, they appear as failures to application programs.

The logs are shrank whenever possible for optimization. For example, a "create" operation followed by a "delete".

<u>Reintegration</u>

Cache is resync-ed and CML is replayed. The process is transparent to the user unless conflicts are detected.

<u>Conflict Resolution</u>

Coda uses syntactic approach for conflict detection. Version information is used to verify one-copy serializability of partitioned updates.

If conflicts are detected, it is the client's responsibility to trigger an appropriate semantic conflict resolution mechanism.
