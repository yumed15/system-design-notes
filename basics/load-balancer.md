# Load Balancer

* helps to spread the traffic across a cluster of servers to improve responsiveness and availability of applications, websites or databases.

### **Benefits**

* faster, uninterrupted service, less downtime and higher throughput
* predictive analytics that predict traffic bottlenecks (smart LB)
* fewer failed or stressed components.
* health checking - LBs use the [heartbeat protocol](../system-design-patterns/heartbeat.md) to monitor the health and, therefore, reliability of end-servers.
* TLS termination: LBs reduce the burden on end-servers by handling TLS termination with the client.
* Reduced human intervention: Because of LB automation, reduced system administration efforts are required in handling failures.
* Service discovery: An advantage of LBs is that the clients’ requests are forwarded to appropriate hosting servers by inquiring about the service registry.
*   Security: LBs may also improve security by mitigating attacks like denial-of-service (DoS) at different layers of the OSI model (layers 3, 4, and 7).



    <figure><img src="../.gitbook/assets/3.webp" alt=""><figcaption></figcaption></figure>

### **Algorithms**

* **Least Connection Method** (directs traffic to the server with the fewest active connections)
* **Least Response Time Method** (directs traffic to the server with the fewest active connections)
* **Least Bandwidth Method** (selects the server that is currently serving the least amount of traffic)
* **Round Robin Method** (cycles through a list of servers and sends each new request to the next server)
* **Weighted Round Robin Method** (servers with higher weights (= an integer value that indicates the processing capacity) receive new and more connections before those with less weights)
  * to handle servers with different characteristics (e.g. processing power, availability, load)
* **IP Hash** (a hash of the IP address of the client is calculated to redirect the request to a server)
* **URL Hash** (It may be possible that some services within the application are provided by specific servers only. In that case, a client requesting service from a URL is assigned to a certain cluster or set of servers. The URL hashing algorithm is used in those scenarios)

### **Stateful load balancing**

As the name indicates, **stateful load balancing** involves maintaining a state of the sessions established between clients and hosting servers. The stateful LB incorporates state information in its algorithm to perform load balancing.

Essentially, the stateful LBs retain a data structure that maps incoming clients to hosting servers. Stateful LBs increase complexity and limit scalability because session information of all the clients is maintained across all the load balancers. That is, load balancers share their state information with each other to make forwarding decisions.

### **Stateless load balancing**

**Stateless load balancing** maintains no state and is, therefore, faster and lightweight. Stateless LBs use consistent hashing to make forwarding decisions. However, if infrastructure changes (for example, a new application server joining), stateless LBs may not be as resilient as stateful LBs because consistent hashing alone isn’t enough to route a request to the correct application server. Therefore, a local state may still be required along with consistent hashing.\
