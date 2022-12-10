# Quorum/Consensus

{% hint style="info" %}
_to ensure strong consistency in a distributed system_
{% endhint %}

<mark style="background-color:yellow;">In a distributed environment, a quorum is the minimum number of servers on which a distributed operation needs to be performed successfully before declaring the operation’s overall success.</mark>

\
Suppose a database is replicated on five machines. In that case, quorum refers _to the minimum number of machines_ that perform the same action (commit or abort) for a given transaction in order to decide the final operation for that transaction. So, in a set of 5 machines, three machines form the majority quorum, and if they agree, we will commit that operation. Quorum enforces the consistency requirement needed for distributed operations.

In systems with multiple replicas, there is a possibility that the user reads inconsistent data. For example, when there are three replicas, `R1`, `R2`, and `R3` in a cluster, and a user writes value `v1` to replica `R1`. Then another user reads from replica `R2` or `R3` which are still behind `R1` and thus will not have the value `v1`, so the second user will not get the consistent state of data.

Quorum is achieved when nodes follow the below protocol:&#x20;

<mark style="background-color:yellow;"></mark>$$R+W>N$$where:&#x20;

* $$N$$ = nodes in the quorum group
* $$W$$ = minimum write nodes&#x20;
* $$R$$ = minimum read nodes

If a distributed system follows $$R+W>N$$ rule, then every read will see at least one copy of the latest value written. For example, a common configuration could be $$N=3, W=2, R=2$$ to ensure strong consistency. Here are a couple of other examples:

* $$N=3, W=1, R=3$$: fast write, slow read, not very durable
*   $$N=3, W=3, R=1$$: slow write, fast read, durable



### Applications

* For leader election, **Chubby** uses <mark style="background-color:yellow;">Paxos</mark>, which use quorum to ensure strong consistency.
* As stated above, quorum is also used to ensure that at least one node receives the update in case of failures. For instance, in **Cassandra**, to ensure data consistency, each write request can be configured to be successful only if the data has been written to at least a quorum (or majority) of replica nodes.
* **Dynamo** replicates writes to a <mark style="background-color:yellow;">**sloppy quorum**</mark> of other nodes in the system, instead of a strict majority quorum like Paxos. All read/write operations are performed on the first NN healthy nodes from the preference list, which may not always be the first NN nodes encountered while walking the consistent hashing ring.
