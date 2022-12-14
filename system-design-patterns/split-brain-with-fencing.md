# Split Brain with Fencing

### Motivation

In the case of zombie leader where the leader is considered dead and the system elects a new leader, we need to make sure the old leader is not running and possibly issuing conflicting commands.&#x20;

### Solution

Put a fence around a previously active leader so that it cannot access cluster resources and hence stop serving any read/write request:

* **resource fencing -** the system blocks the previously active leader from accessing resources needed to perform essential tasks.
* **node fencing** - the system stops the previously active leader from accessing all resources.

### Applications

**HDFS** uses fencing to stop the previously active NameNode from accessing cluster resources, thereby stopping it from servicing requests.
