**Layered Model of Failure Resiliency**

If failure event is detected at one level of the system, the higher level handle the event so that the levels above are unaware of the problem. For example, If packet loss occurs at IP or lower layer, timeout and retransmission occurs at TCP level and the application is unaware of the packet loss.

However, not all failures can be masked. For example, if there is a cache miss on a disconnected client, there is no feasible solution.

**Failure Detection**

Transient failures only manifest in unlikely combination of circumstances. Retrying usually corrects the problem.

Persistent failures continues until explicitly repaired. Means of distributions are MTBF and MTTR.

![](images/Pasted%20image%2020230429141245.png)

- Availability (Single) = MTBF / (MTBF + MTTR)
- Availability (Series) = Availability x Availability x ...
- Availability (Parallel) = 1 - (1 - Availability) x (1 - Availability) x ...

**Triple Modular Redundancy (TMR)**

3 independent units perform identical operation. Voting unit compares the results of the 3 units and the majority wins.

Assumes that the voting mechanism never fails undetected.

**Fail Fast Components**

Simple and clean failure model. Software either gives a correct result or does not give a result.

**Byzantine Failures**

Undetected erroneous computation. Difficult to detect and confine this class of failures.

**Byzantine General Problem**

`BGP(n, m)` is the problem with n generals and m traitors. It is solvable if and only if n >= (3m + 1). Hence TMR is insufficient for Byzantine failures.

**Failure Containment**

A transaction is a group of actions such that all succeed or none succeed.

Every transaction has a commit point. Before the commit point, undo should be possible. The commit point is the single point of transition from "transient state" to "committed state".

**ACID Property of Transactions**

- <u>Atomicity</u>: All or nothing.
- <u>Consistency</u>: Execution of a consistent state leaves data consistent.
- <u>Isolation</u>: As if only one transaction is running.
- <u>Durability</u>: Effects of a committed transaction are preserved forever.

**Shadowing**

Carefully construct a shadow copy that contains all modification and use <u>an atomic pointer</u> swing that atomically commits a transaction.

Crash recovery is only garbage collection of unreachable pages. Slow forward processing during transaction but fast recovery.

**Intention List**

Keep a list of proposed changes in the stable storage. On commit, write <u>a completion record</u> to the list and gradually apply changes to the stable storage. On abort, delete the intention list instead.

On crash recovery, discard incomplete intention lists and reapply complete intention lists. There is no undo-ing. The intention lists must be idempotent.

**Log-Based Recovery**

Optimized version of intention list. Append-only log that is preserved until log truncation.

During crash recovery, log entries may be ignored/ redone/ undone.

<u>Logical Logging</u>: More compact but requires application support.

<u>Physical Logging</u>: Less compact but more general.

<u>Undo Rule</u>: If and only if uncommitted transactions can modify committed state.

<u>Redo rule</u>: If and only if committed transactions have outstanding modifications to committed state.
