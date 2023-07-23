## Kubernetes (K8s)

Kubernetes, often abbreviated as K8s (since there are 8 letters between 'K' and 's'), is an open-source container orchestration platform. It was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF). Kubernetes simplifies the deployment, scaling, and management of containerized applications.

### Key Concepts

Kubernetes operates based on a few fundamental concepts:

1. **Node**: A worker machine in the Kubernetes cluster where containers can be run. Each node runs a container runtime, such as Docker, to manage containers.

2. **Pod**: The smallest deployable unit in Kubernetes, representing one or more containers that are co-located on the same host. Pods are used to encapsulate containers and share network and storage resources.

3. **Deployment**: A higher-level construct that manages the desired state of replicated pods. It ensures that the specified number of pod replicas are running and automatically handles scaling and rolling updates.

4. **Service**: An abstraction that exposes a set of pods to the network. It provides a stable IP address and DNS name for the pods, allowing other services to communicate with them without knowing their exact location.

5. **Namespace**: A logical partitioning mechanism in Kubernetes to separate resources into different virtual clusters. Namespaces help in organizing and managing resources within a cluster.

### How Kubernetes Works

1. **Desired State Management**: Users declare the desired state of their applications using YAML or JSON manifests. Kubernetes continuously works to ensure that the actual state of the system matches the desired state.

2. **Self-healing**: Kubernetes automatically restarts failed containers and reschedules them onto healthy nodes. This ensures high availability and fault tolerance.

3. **Scaling**: Kubernetes allows manual or automatic scaling of applications by adjusting the number of replicas in a deployment or using the Horizontal Pod Autoscaler (HPA) based on resource utilization metrics.

4. **Load Balancing**: Services provide load balancing capabilities across pods, distributing traffic to healthy instances.

5. **Rolling Updates**: Kubernetes can perform rolling updates on Deployments to ensure a smooth transition between different versions of applications.

### Use Cases

Kubernetes is widely used for various purposes, including:

- **Microservices**: Deploying, managing, and scaling microservices architectures effectively.

- **Continuous Deployment**: Facilitating the continuous deployment of applications and services.

- **Big Data and AI/ML**: Running data-intensive workloads and machine learning applications.

- **Hybrid and Multi-cloud Environments**: Managing applications across multiple cloud providers and on-premises infrastructure.


## Kubernetes Architecture

Kubernetes architecture follows a master-worker node model. It consists of several components that work together to manage containerized applications efficiently. Let's explore the key components:

### Master Components

1. **API Server**: The central control point for the Kubernetes cluster. All administrative tasks and communication with the cluster are handled through the API server. It validates and processes RESTful API requests, updating the state of objects in the etcd datastore.

2. **etcd**: A distributed and highly available key-value store that stores the cluster's configuration data. It serves as Kubernetes' primary database and ensures that the cluster state is consistent across all nodes.

3. **Scheduler**: Responsible for distributing pod workloads across worker nodes based on resource requirements, node capacity, and other constraints. It ensures high availability and efficient resource utilization.

4. **Controller Manager**: Manages various control loops that continuously monitor the cluster's state and make necessary changes to maintain the desired state. Examples of controllers include the Replication Controller, Deployment Controller, and Node Controller.

5. **Cloud Controller Manager** (optional): Provides an interface for managing the underlying cloud infrastructure. It interacts with cloud-specific APIs to perform tasks like creating load balancers or managing volumes.

### Node Components

1. **Kubelet**: The primary node agent that runs on each worker node. It communicates with the API server and manages pods and containers on the node, ensuring they are running and healthy.

2. **Container Runtime**: The software responsible for running containers, such as Docker, containerd, or rkt. Kubernetes supports different container runtimes, providing flexibility in choosing the most suitable one for your environment.

3. **Kube Proxy**: Manages network routing on each node. It maintains network rules and ensures communication between different pods and services within the cluster.

### Architecture of K8s


![K8s Diagram](https://phoenixnap.com/kb/wp-content/uploads/2021/04/full-kubernetes-model-architecture.png)

### Add-ons

Kubernetes also includes optional add-ons that enhance its capabilities:

1. **DNS**: A cluster-wide DNS service that allows pods to communicate with each other using their DNS names. This enables service discovery within the cluster.

2. **Dashboard**: A web-based user interface that provides a graphical view of the cluster, allowing users to manage and monitor resources easily.

3. **Ingress Controller**: Manages external access to services within the cluster by routing incoming traffic based on rules defined in the Ingress resource.

4. **Metrics Server**: Collects resource utilization metrics from nodes and pods, which can be used for monitoring and autoscaling.

### How Components Interact

The master components communicate with each other and with the nodes through the API server. They use etcd to store and retrieve configuration data, ensuring consistency across the cluster.

Nodes interact with the master components through the Kubelet, which communicates with the API server to receive instructions and report the node's status. Kube Proxy handles network routing on each node to facilitate pod-to-pod communication.

### Conclusion

Kubernetes architecture is designed for scalability, high availability, and ease of management. By understanding the roles of each component, you can effectively deploy and manage containerized applications in a Kubernetes cluster.
