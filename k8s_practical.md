## Kubernetes Deployment

In Kubernetes, a **Deployment** is an object that manages a set of identical pods, ensuring they are running and available according to the desired state defined in the deployment configuration. Deployments are a higher-level abstraction that allows you to declaratively manage replica sets and pods, making it easy to handle application updates and scaling.

### Example of a Deployment

Suppose you have a simple web application that consists of a single container running an Nginx web server. You want to deploy this application to a Kubernetes cluster using a Deployment.

1. **Create a Deployment YAML file** (e.g., `nginx-deployment.yaml`):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
```


## Kubernetes Service Explained

In Kubernetes, a **Service** is an abstraction that defines a logical set of pods and a policy to access them. Services provide a stable endpoint for accessing applications running in a Kubernetes cluster, enabling seamless communication between different parts of the application or with external clients.

### Types of Services

Kubernetes offers different types of services to cater to various use cases:

1. **ClusterIP**: The default type. Exposes the service on an internal IP address that is only accessible within the cluster. This is useful for internal communication between pods.

2. **NodePort**: Exposes the service on a static port on each node's IP address. The service can be accessed externally (outside the cluster) using the node's IP and the static port.

3. **LoadBalancer**: Automatically provisions an external load balancer (in supported cloud environments) and assigns a fixed external IP address to the service. It allows external clients to access the service through the load balancer.

4. **ExternalName**: Maps the service to an external DNS name. It does not provide any proxying or load balancing; instead, it allows the service to act as a CNAME record to an external name.

### Creating a Service

To create a service, you define a Service manifest in YAML format. Here's an example of creating a ClusterIP service for an application named "my-app" that runs on port 8080:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

## Ingress in Kubernetes

In Kubernetes, an **Ingress** is an API object that manages external access to services within a cluster. It acts as an entry point for incoming traffic, routing requests to the appropriate services based on the specified rules. Ingress allows you to expose multiple services through a single external IP address and port, simplifying the management of external access to your applications.

### How Ingress Works

When a client sends a request to access a service exposed through an Ingress, the request is first directed to the Ingress controller, which is responsible for processing the Ingress rules. The Ingress controller examines the request's host and path information, then forwards the request to the corresponding service based on the rules defined in the Ingress.

Ingress can perform various functions, including:

- **Load Balancing**: Distributing incoming traffic across multiple pods of a service to ensure optimal resource utilization and high availability.

- **Path-Based Routing**: Directing requests to different services based on the request path.

- **SSL Termination**: Terminating SSL/TLS encryption and forwarding the plain HTTP request to the backend service.

- **Name-Based Virtual Hosting**: Handling requests for multiple domain names and routing them to different services.

### Creating an Ingress

To create an Ingress, you define an Ingress resource in YAML format. Here's an example of a basic Ingress configuration:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-service
                port:
                  number: 80
```
