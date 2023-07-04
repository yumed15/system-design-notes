# Consistent hashing

### Motivation

When it comes to data partitioning, aka distributing data across a set of nodes, there are a couple of challenges:

* How do we know on which node a particular piece of data will be stored?
* When we add or remove nodes, how do we know what data will be moved from existing nodes to the new nodes? Additionally, how can we minimize data movement when nodes join or leave?

The naive approach of using a hash function (like modulo) that maps the data to a server number would be hard to maintain. When we add or remove a server, we have to remap all the keys and move our data based on the new server count, which can get messy quite quickly.

### Solution

<mark style="background-color:yellow;">**Consistent Hashing**</mark> maps data to physical nodes and ensures that <mark style="background-color:yellow;">**only a small set of keys move when servers are added or removed**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">by storing the data managed by a distributed system in a</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**ring**</mark><mark style="background-color:yellow;">. Each node in the ring is assigned a range of data.</mark>

<figure><img src="../.gitbook/assets/Diana Playground (2).jpg" alt=""><figcaption><p>Consistent Hashing ring</p></figcaption></figure>

With consistent hashing, the ring is divided into smaller, predefined ranges. <mark style="background-color:yellow;">Each node is assigned one of these ranges. The start of the range is called a</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**token**</mark><mark style="background-color:yellow;">.</mark> This means that each node will be assigned one token. The range assigned to each node is computed as follows:

{% hint style="info" %}
**Range start:**  Token value\
**Range end:**    Next token value - 1
{% endhint %}

The nodes from the above example would have the following tokens:

<table><thead><tr><th align="center">Server</th><th align="center">Token</th><th width="151" align="center">Range Start</th><th align="center">Range End</th></tr></thead><tbody><tr><td align="center">Server 1 </td><td align="center">1</td><td align="center">1</td><td align="center">25</td></tr><tr><td align="center">Server 2</td><td align="center">26</td><td align="center">26</td><td align="center">50</td></tr><tr><td align="center">Server 3</td><td align="center">51</td><td align="center">51</td><td align="center">75</td></tr><tr><td align="center">Server 4</td><td align="center">76</td><td align="center">76</td><td align="center">100</td></tr></tbody></table>

### Adding/Reading data

Whenever the system needs to read or write data:

1. the first step it performs is to apply the <mark style="background-color:yellow;">**MD5 hashing algorithm**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">to the</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**key**</mark>
2. <mark style="background-color:yellow;">the output of this hashing algorithm determines</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**within which range**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">the data lies</mark> and hence, on which node the data will be stored.&#x20;

<figure><img src="../.gitbook/assets/Diana Playground (3).jpg" alt=""><figcaption><p>Distributing data on the Consistent Hashing ring</p></figcaption></figure>

### Adding/Removing Nodes

* When adding a new node, only the next node is affected.
* When a node is removed, the next node becomes responsible for all of the keys stored on the outgoing node.

**Issues:**

* **non uniform data and load distribution**&#x20;
* **adding or removing nodes** - will result in recomputing the tokens causing a significant administrative overhead for a large cluster.
* **hotspots -** since each node is assigned one large range, if the data is not evenly distributed, some nodes can become hotspots.
* **node rebuilding** - since each node’s data might be replicated (for fault-tolerance) on a fixed number of other nodes, when we need to rebuild a node, only its replica nodes can provide the data. This puts a lot of pressure on the replica nodes and can lead to service degradation.

Instead of assigning a single token to a node, the hash range is divided into multiple smaller ranges, and each physical node is assigned several of these smaller ranges. Each of these subranges is considered a <mark style="background-color:yellow;">**virtual node (vNode)**</mark>.

<figure><img src="../.gitbook/assets/Diana Playground (4).jpg" alt=""><figcaption><p>Comparing Consistent Hashing ring with and without Vnodes</p></figcaption></figure>

Vnodes are <mark style="background-color:yellow;">**randomly distributed**</mark> across the cluster and are generally <mark style="background-color:yellow;">**non-contiguous**</mark> so that no two neighboring Vnodes are assigned to the same physical node or rack.&#x20;

Advantages:

1. As Vnodes help spread the load more evenly across the physical nodes on the cluster by dividing the hash ranges into smaller subranges, this speeds up the rebalancing process after adding or removing nodes. When a new node is added, it receives many Vnodes from the existing nodes to maintain a balanced cluster. Similarly, when a node needs to be rebuilt, instead of getting data from a fixed number of replicas, many nodes participate in the rebuild process.
2. Vnodes make it easier to maintain a cluster containing heterogeneous machines. This means, with Vnodes, we can assign a high number of sub-ranges to a powerful server and a lower number of sub-ranges to a less powerful server.
3. In contrast to one big range, since Vnodes help assign smaller ranges to each physical node, this decreases the probability of hotspots.

### Applications

**Dynamo** and **Cassandra** use Consistent Hashing to distribute their data across nodes.
