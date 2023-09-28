# Hinted Handoff

### Motivation

Depending upon the consistency level, a distributed system can still serve write requests even when nodes are down:&#x20;

* if we have the replication factor of three and the client is writing with a quorum consistency level
* if one of the nodes is down, the system can still write on the remaining two nodes to fulfill the consistency level, making the write successful.

But when the node that was down comes back we still need to write the data to it.

### Solution

For nodes that are down, the system **keeps notes (or hints)** of **all the write requests** they have missed. Once the failing nodes recover, the write requests are forwarded to them based on the hints stored.

* When a node is down or is not responding to a write request, the node which is coordinating the operation, writes a hint in a text file on the local disk.
* This hint contains the data itself along with information about which node the data belongs to.
* When the coordinating node discovers that a node for which it holds hints has recovered, it forwards the write requests for each hint to the target.

### Applications

* **Cassandra** nodes use Hinted Handoff to remember the write operation for failing nodes.
* **Dynamo** ensures that the system is “always-writeable” by using Hinted Handoff (and Sloppy Quorum).\
