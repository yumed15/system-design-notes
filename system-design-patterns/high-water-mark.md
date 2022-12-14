# High-Water Mark

### Motivation

To achieve strong consistency:

* use a leader-follower setup, where the leader is responsible for serving all the writes, and the followers replicate data from the leader.
* each transaction on the leader is committed to a write-ahead log (WAL), so that the leader can recover from crashes or failures.
* a write request is considered successful as soon as it is committed to the WAL on the leader.
* the replication can happen asynchronously:
  * the leader can push the mutation to the followers
  * or the follower can pull it from the leader
* in case the leader crashes and cannot recover, one of the followers will be elected as the new leader
  * this new leader can be a bit behind the old leader, as there might be some transactions that have not been completely propagated before the old leader crashed.
  * we do have these transactions in the WAL on the old leader, but those log entries cannot be recovered until the old leader becomes alive again, so those transactions are considered lost.

<figure><img src="../.gitbook/assets/Diana Playground (6).jpg" alt=""><figcaption></figcaption></figure>

### Solution

Keep track of the last log entry on the leader, which has been successfully replicated to a quorum of followers. The index of this entry in the log is known as the <mark style="background-color:yellow;">**High-Water Mark index**</mark>. The leader exposes data only up to the high-water mark index.

1. for each data mutation, the leader first appends it to WAL and then sends it to all the followers.
2. upon receiving the request, the followers append it to their respective WAL and then send an acknowledgment to the leader.
3. the leader keeps track of the indexes of the entries that have been successfully replicated on each follower. The high-water mark index is the highest index, which has been replicated on the quorum of the followers.
4. the leader can propagate the high-water mark index to all followers as part of the regular Heartbeat message
5. the leader and followers ensure that the client can read data only up to the high-water mark index.

<figure><img src="../.gitbook/assets/Diana Playground (7).jpg" alt=""><figcaption></figcaption></figure>

### Applications&#x20;

**Kafka**: To deal with non-repeatable reads and ensure data consistency, Kafka brokers keep track of the high-water mark, which is the largest offset that all In-Sync-Replicas (ISRs) of a particular partition share. Consumers can see messages only until the high-water mark.\
