# Write-ahead Log

### Motivation

A machine stops running while in the middle of performing a data modification. When it restarts, based on atomicity and durability needs, it might decide to redo or undo what it was doing. For this, it must know where it left off.&#x20;

### Solution

To guarantee durability and data integrity, <mark style="background-color:yellow;">each modification to the system is first written to an append-only log on the disk</mark> (known as <mark style="background-color:yellow;">Write-Ahead Log (WAL)</mark> or <mark style="background-color:yellow;">transaction log</mark> or <mark style="background-color:yellow;">commit log</mark>) Each log entry should contain enough information to redo or undo the modification. The log can be read on every restart to recover the previous state by replaying all the log entries.

Each node, in a distributed environment, maintains its own log. WAL is always sequentially appended, which simplifies the handling of the log. Each log entry is given a unique identifier; this identifier helps in implementing certain other operations like <mark style="background-color:yellow;">**log segmentation**</mark> or <mark style="background-color:yellow;">**log purging**</mark><mark style="background-color:yellow;">.</mark>

<figure><img src="../.gitbook/assets/Diana Playground (5).jpg" alt=""><figcaption></figcaption></figure>

### Applications

* **Cassandra**: To ensure durability, whenever a node receives a write request, it immediately writes the data to a commit log which is a WAL.
* **Kafka** implements a distributed Commit Log to persistently store all messages it receives.
* **Chubby**: For fault tolerance and in the event of a leader crash, all database transactions are stored in a transaction log
