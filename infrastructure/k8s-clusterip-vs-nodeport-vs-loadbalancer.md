# K8S - ClusterIP vs NodePort vs LoadBalancer

Kubernetes services provide three different types to allow clients to establish network connections while not exposing services to unnecessary traffic.

* `ClusterIP`
* `NodePort`
* `LoadBalancer`

### The ClusterIP service type <a href="#the-clusterip-service-type" id="the-clusterip-service-type"></a>

_(within k8s cluster)_\
A ClusterIP service is the default Kubernetes service. It gives you a service inside your cluster that other apps **inside** your cluster can access. There is **no external access.**

```yaml
apiVersion: v1
kind: Service
metadata:  
  name: my-internal-service
spec:
  selector:    
    app: my-app
  type: ClusterIP
  ports:  
  - name: http
    port: 80
    targetPort: 80
    protocol: TCP
```

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

**How to access**

Exposes&#x20;

* `spec.clusterIp:spec.ports[*].port`

You can only access this service while inside the cluster. It is accessible from its `spec.clusterIp` port. If a `spec.ports[*].targetPort` is set it will route from the port to the targetPort. The CLUSTER-IP you get when calling `kubectl get services` is the IP assigned to this service within the cluster internally.

### The NodePort service type <a href="#the-nodeport-service-type" id="the-nodeport-service-type"></a>

_(within cluster external to k8s cluster)_

`NodePort` services expose pods **internally** the same way a `ClusterIP` service does. In addition, a `NodePort` service allows **external clients to access pods via network ports** opened on the Kubernetes nodes. These ports are typically in the range 30000-32768, although that range is customizable.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: web
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
      nodePort: 30007
```

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

**How to access**

A NodePort exposes the following:

* `<NodeIP>:spec.ports[*].nodePort`
* `spec.clusterIp:spec.ports[*].port`

If you access this service on a nodePort from the node's external IP, it will route the request to `spec.clusterIp:spec.ports[*].port`, which will in turn route it to your `spec.ports[*].targetPort`, if set. This service can also be accessed in the same way as ClusterIP.

Your NodeIPs are the external IP addresses of the nodes. You cannot access your service from `spec.clusterIp:spec.ports[*].nodePort`.

### The LoadBalancer service type

_(external world or whatever you defined in your LB)_

`LoadBalancer` services expose pods **internally** the same way a `NodePort` service does. In addition, `LoadBalancer` services **create external network infrastructure to direct network requests to pods in the cluster**.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: LoadBalancer
  selector:
    app: web
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

**How to access**

A LoadBalancer exposes the following:

* `spec.loadBalancerIp:spec.ports[*].port`
* `<NodeIP>:spec.ports[*].nodePort`
* `spec.clusterIp:spec.ports[*].port`

You can access this service from your load balancer's IP address, which routes your request to a nodePort, which in turn routes the request to the clusterIP port. You can access this service as you would a NodePort or a ClusterIP service as well.

**Cons**

* The big downside is that **each** **service** you expose with a LoadBalancer will get **its own IP address**, and you have to pay for a LoadBalancer per exposed service, which can get expensive!

| `Feature`         | `ClusterIP`                                                                                   | `NodePort`                                                                                                                                                    | `LoadBalancer`                                                                                                                          |
| ----------------- | --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| **Exposition**    | Exposes the Service on an internal IP in the cluster.                                         | Exposing services to external clients                                                                                                                         | Exposing services to external clients                                                                                                   |
| **Cluster**       | This type makes the Service only reachable from within the cluster                            | A NodePort service, each cluster node opens a port on the node itself (hence the name) and redirects traffic received on that port to the underlying service. | A LoadBalancer service accessible through a dedicated load balancer, provisioned from the cloud infrastructure Kubernetes is running on |
| **Accessibility** | It is **default** service and Internal clients send requests to a stable internal IP address. | The service is accessible at the internal cluster IP-port, and also through a dedicated port on all nodes.                                                    | Clients connect to the service through the load balancer’s IP.                                                                          |
| **Yaml Config**   | `type: ClusterIP`                                                                             | `type: NodePort`                                                                                                                                              | `type: LoadBalancer`                                                                                                                    |
| **Port Range**    | Any public ip form Cluster                                                                    | 30000 - 32767                                                                                                                                                 | Any public ip form Cluster                                                                                                              |
| **User Cases**    | For internal communication                                                                    | Best for testing public or private access or providing access for a small amount of time.                                                                     | widely used For External communication                                                                                                  |

### **Ingress** <a href="#the-nodeport-service-type" id="the-nodeport-service-type"></a>

Ingress is actually NOT a type of service. Instead, it sits in front of multiple services and acts as a “smart router” or entrypoint into your cluster.

The default GKE ingress controller will spin up a [HTTP(S) Load Balancer](https://cloud.google.com/compute/docs/load-balancing/http/) for you. This will let you do both path based and subdomain based routing to backend services.

The YAML for a Ingress object on GKE with a [L7 HTTP Load Balancer](https://cloud.google.com/compute/docs/load-balancing/http/) might look like this:

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: my-ingress
spec:
  backend:
    serviceName: other
    servicePort: 8080
  rules:
  - host: foo.mydomain.com
    http:
      paths:
      - backend:
          serviceName: foo
          servicePort: 8080
  - host: mydomain.com
    http:
      paths:
      - path: /bar/*
        backend:
          serviceName: bar
          servicePort: 8080

```

<figure><img src="../.gitbook/assets/Microservice Communication (2).jpg" alt=""><figcaption></figcaption></figure>

**Pros**

* most useful if you want to expose multiple services under the same IP address, and these services all use the same L7 protocol (typically HTTP).&#x20;
* you only pay for one load balancer if you are using the native GCP integration, and because Ingress is “smart” you can get a lot of features out of the box (like SSL, Auth, Routing, etc)

### **Resources** <a href="#the-nodeport-service-type" id="the-nodeport-service-type"></a>

* [What's the difference between ClusterIP, NodePort and LoadBalancer service types in Kubernetes?](https://stackoverflow.com/questions/41509439/whats-the-difference-between-clusterip-nodeport-and-loadbalancer-service-types)
* [Kubernetes NodePort vs LoadBalancer vs Ingress? When should I use what?](https://medium.com/google-cloud/kubernetes-nodeport-vs-loadbalancer-vs-ingress-when-should-i-use-what-922f010849e0)
