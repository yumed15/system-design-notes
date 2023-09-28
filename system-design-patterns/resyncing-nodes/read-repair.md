# Read Repair

### Motivation

Repairing stale data for nodes that were down and now are back online.

### Solution

**Read Repair** = mechanism during which the stale date is repaired during the read operation, since at that point, we can read data from multiple nodes to perform a comparison and find nodes that have stale data. Once the node with old data is known, the read repair operation pushes the newer version of data to nodes with the older version.

* Based on the quorum, the system reads data from multiple nodes.
* For Quorum=2, the system reads data from one node and digest of the data from the second node.
* The digest is a checksum of the data and is used to save network bandwidth.
* If the digest does not match, it means some replicas do not have the latest version of the data.
* In this case, the system reads the data from all the replicas to find the latest data.
* The system returns the latest data to the client and initiates a **Read Repair** request.
* The read repair operation pushes the latest version of data to nodes with the older version.

<figure><img src="../../.gitbook/assets/Diana Playground (12).jpg" alt=""><figcaption></figcaption></figure>

### Applications

**Cassandra** and **Dynamo** use ‘Read Repair’ to push the latest version of the data to nodes with the older versions.
