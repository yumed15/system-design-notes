# Load Balancer

* helps to spread the traffic across a cluster of servers to improve responsiveness and availability of applications, websites or databases.
*   **Benefits**: faster, uninterrupted service, less downtime and higher throughput, predictive analytics that predict traffic bottlenecks (smart LB), fewer failed or stressed components.



    <figure><img src="../.gitbook/assets/3.webp" alt=""><figcaption></figcaption></figure>
* **Algorithms**:
  * **Least Connection Method** (directs traffic to the server with the fewest active connections)
  * **Least Response Time Method** (directs traffic to the server with the fewest active connections)
  * **Least Bandwidth Method** (selects the server that is currently serving the least amount of traffic)
  * **Round Robin Method** (cycles through a list of servers and sends each new request to the next server)
  * **Weighted Round Robin Method** (servers with higher weights (= an integer value that indicates the processing capacity) receive new and more connections before those with less weights)
    * to handle servers with different characteristics (e.g. processing power, availability, load)
  * **IP Hash** (a hash of the IP address of the client is calculated to redirect the request to a server)
