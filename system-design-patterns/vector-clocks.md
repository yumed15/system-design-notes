# Vector Clocks

### Motivation

When a distributed system allows concurrent writes, it can result in multiple versions of an object. Different replicas of an object can end up with different versions of the data.

On a single machine, all we need to know about is the absolute or **wall clock** time: suppose we perform a write to key `k` with timestamp `t1`, and then perform another write to `k` with timestamp `t2`. Since `t2 > t1`, the second write must have been newer than the first write, and therefore, the database can safely overwrite the original value.

In a distributed system, this assumption does not hold true. The problem is **clock skew** – different clocks tend to run at different rates

### Solution

Use Vector clocks to keep track of value history and reconcile divergent histories at read time.&#x20;

A vector clock is effectively a `(node, counter)` pair. One vector clock is associated with every version of every object.&#x20;

* If the counters on the first object’s clock are less-than-or-equal to all of the nodes in the second clock, then the first is an ancestor of the second and can be forgotten.&#x20;
* Otherwise, the two changes are considered to be in conflict and require reconciliation.&#x20;
  * Such conflicts are resolved at read-time, and if the system is not able to reconcile an object’s state from its vector clocks, it sends it to the client application for reconciliation

### Applications

Amazon’s **Dynamo** uses Vector Clocks to reconcile concurrent updates.
