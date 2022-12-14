# Phi Accrual Failure Detection

### Motivation

A heartbeat only tells you is a system is down or up, no in between, but in reality it might just be overwhelmed. Heartbeating uses a fixed timeout, and if there is no heartbeat from a server, the system, after the timeout assumes that the server has crashed, which makes the **value of the timeout critical**.

### Solution

We can use <mark style="background-color:yellow;">**an adaptive failure detection algorithm**</mark>**:**

* accrual = accumulation or the act of accumulating over time
* uses <mark style="background-color:yellow;">**historical**</mark> heartbeat information to make the threshold adaptive
* instead of telling you is a server is alive or not, it <mark style="background-color:yellow;">**outputs the suspicion level about a server**</mark>
* if a node does not respond, its suspicion level is increased and could be declared dead later
* as a node’s suspicion level increases, the system can gradually stop sending new requests to it
* makes a system efficient as it takes into account fluctuations in the network environment and other intermittent server issues before declaring a system completely dead.

### Application

**Cassandra** uses the Phi Accrual Failure Detector algorithm to determine the state of the nodes in the cluster.

