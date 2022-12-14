# Heartbeat

### Motivation

Servers should know if other servers are alive and working:

* whenever a request arrives at a server, the server should have enough information to decide which server is responsible for solving that request.
* also enables the system to take corrective actions and route the work to another healthy server.

### Solution

Each server periodically sends a heartbeat message to a central monitoring server or other servers in the system to show that it is still alive and functioning. If there is no heartbeat within a configured timeout period, the system can conclude that the server is not alive anymore and stop sending requests to it and start working on its replacement.

<figure><img src="../.gitbook/assets/Diana Playground (8).jpg" alt=""><figcaption></figcaption></figure>

\
