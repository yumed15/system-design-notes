# Segmented Log

### Motivation

A single log can become difficult to manage:&#x20;

* it can become a performance bottleneck, especially when it is read at the startup
* older logs need to be cleaned up periodically or, in some cases, merged
* doing these operations on a single large file is difficult to implement.

### Solution

Break down the log into smaller segments for easier management, such that the log data is divided into equal-sized log segments. The system can roll the log based on a rolling policy (by time e.g. every 4 hours or size every 1GB)

### Applications

* **Cassandra** uses the segmented log strategy to split its commit log into multiple smaller files instead of a single large file for easier operations. As we know, when a node receives a write operation, it immediately writes the data to a commit log. As the Commit Log grows in size and reaches its threshold in size, a new commit log is created. Commit log segments are truncated when Cassandra has flushed corresponding data to SSTables. A commit log segment can be **archived**, **deleted**, or **recycled** once all its data has been flushed to SSTables.
* **Kafka** uses log segmentation to implement storage for its partitions.
