# PACEL Theorem

The PACELC theorem states that in a system that replicates data:

* if there is a partition (‘P’), a distributed system can tradeoff between availability and consistency (i.e., ‘A’ and ‘C’);
* else (‘E’), when the system is running normally in the absence of partitions, the system can tradeoff between latency (‘L’) and consistency (‘C’).

<figure><img src="../.gitbook/assets/Diana Playground (11).jpg" alt=""><figcaption></figcaption></figure>

**PA/EL** systems - **Dynamo and Cassandra** - **** They choose availability over consistency when a partition occurs; otherwise, they choose lower latency.

**PC/EC** systems - **BigTable and HBase** - They will always choose consistency, giving up availability and lower latency.

**PA/EC** systems - **MongoDB** - MongoDB works in a primary/secondaries configuration. In the default configuration, all writes and reads are performed on the primary. As all replication is done asynchronously (from primary to secondaries), when there is a network partition in which primary is lost or becomes isolated on the minority side, there is a chance of losing data that is unreplicated to secondaries, hence there is a loss of consistency during partitions. Therefore it can be concluded that **in the case of a network partition, MongoDB chooses availability, but otherwise guarantees consistency**. Alternately, when MongoDB is configured to write on majority replicas and read from the primary, it could be categorized as PC/EC.

