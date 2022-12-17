# Gossip Protocol

### Motivation

Where we do not have any central node that keeps track of all nodes to know if a node is down or not, we could have every node maintain a heartbeat with every other node. This means $$O(N^2)$$ messages get sent every tick (where $$N$$ is the total number of nodes)

### Solution

Each node keeps track of state information about other nodes in the cluster and gossip (i.e., share) this information to one other random node every second.

Nodes periodically exchange state information about themselves and about other nodes they know about. Each node initiates a gossip round every second to exchange state information about themselves and other nodes with one other random node. This means that any state change will eventually propagate through the system, and all nodes quickly learn about all other nodes in a cluster.

<figure><img src="../.gitbook/assets/Diana Playground (9).jpg" alt=""><figcaption></figcaption></figure>

Gossip protocol is based on how epidemics spread. It starts from one random node and fans out to several other nodes. Eventually all nodes are “infected”. The animation below shows how the Gossip Protocol works in a cluster of servers.

<figure><img src="../.gitbook/assets/Untitled_2.gif" alt=""><figcaption><p>Courtesy of <a href="https://flopezluis.github.io/gossip-simulator/">https://flopezluis.github.io/gossip-simulator/</a></p></figcaption></figure>

### Applications

**Dynamo & Cassandra** use gossip protocol which allows each node to keep track of state information about the other nodes in the cluster, like which nodes are reachable, what key ranges they are responsible for, etc.

**Ethereum**, **Cassandra** and **Redis** all use Gossip for P2P (Peer-to-Peer) communication.
