# Docker Networks
Docker networks are a fundamental feature of Docker that enable communication between containers and between containers and the host system. When you run multiple containers within Docker, they are isolated by default. Docker networks provide a way to connect these containers, facilitating seamless communication and enabling them to work together as part of a larger application or system.

## Docker offers different types of network drivers, each with its specific use case:

1. **Bridge Network:** This is the default network created when you run a Docker container without specifying a network. Containers connected to the bridge network can communicate with each other using their IP addresses. You can also expose container ports to the host using this network type.

2. **Host Network:** When you use the host network driver, the container shares the host's network namespace, which means it uses the host's network stack directly. This provides the best performance for the container, but it also means the container's ports are directly exposed on the host.

3. **Overlay Network:** Overlay networks are used in Docker Swarm mode to allow communication between containers running on different Docker hosts within a swarm. It creates a secure, multi-host network for container communication.

4. **Macvlan Network:** Macvlan allows you to assign a MAC address to a container, making it appear as a physical device on the network. This enables containers to have their IP address and be reachable directly from the external network.

5. **None Network:** When you specify the "none" network driver, the container does not have access to any network resources, effectively disabling network communication.

6. **Custom Bridge Networks:** Apart from the default bridge network, you can create custom bridge networks using the docker network create command. Custom bridge networks provide isolation and control over container communication.

**Example of Using Docker Networks**
```bash
# Create a custom bridge network
docker network create my_network

# Run containers attached to the custom bridge network
docker run --name container1 --network my_network -d nginx
docker run --name container2 --network my_network -d nginx

# Access "container2" from "container1"
docker exec container1 ping container2

# Remove containers and network
docker stop container1 container2
docker rm container1 container2
docker network rm my_network
```

## Host Network in Docker
In Docker, the "host" network mode is a network driver that allows a container to share the network namespace with the host system. When you run a container using the host network mode, it uses the host's networking stack directly, meaning the container does not have its own isolated network namespace. As a result, the container's network interfaces are directly attached to the host's network interfaces, and they share the same IP address and port space.

Using the host network mode can provide better network performance for the container since it eliminates the overhead of virtualized network stacks. However, it also means that the container's network interfaces are exposed directly on the host, which may reduce isolation and security.

**Example of Using Host Network**
Let's run a simple container in the host network mode to illustrate how it works:
```bash
# Run a container in host network mode
docker run --name my_container --network host -d nginx
```
In this example, we start an Nginx web server container using the host network mode. The **--network host** option indicates that the container should share the host's network namespace.
**Cleanup**
After you're done experimenting, remember to clean up the container:
```bash
# Stop and remove the container
docker stop my_container
docker rm my_container
```
With this setup, the Nginx server inside the container is accessible using the host's IP address directly, and it can use any ports available on the host. For example, if the host's IP address is **192.168.1.100**, the Nginx server in the container can be accessed at **http://192.168.1.100.**

Keep in mind that using the host network mode may lead to port conflicts, especially if multiple containers are trying to use the same ports. Additionally, since the container shares the host's network namespace, any changes made to the network configuration inside the container will directly affect the host system.

## Custom Bridge Network in Docker

A custom bridge network in Docker is a user-defined bridge network that you can create to facilitate communication between containers in a controlled and isolated manner. Unlike the default bridge network, which is created automatically when you run containers, a custom bridge network provides more control over IP address assignment and container-to-container communication.

**Example of Creating and Using a Custom Bridge Network**
```bash
# Step 1: Create a custom bridge network
docker network create my_custom_network

# Step 2: Run containers attached to the custom bridge network
docker run --name container1 --network my_custom_network -d nginx
docker run --name container2 --network my_custom_network -d nginx
```
In this example, we've created a custom bridge network called "my_custom_network" using the `docker network create` command. Then, we ran two Nginx containers (container1 and container2) and attached them to this network using the `--network my_custom_network` option.

Now, since both containers are connected to the same custom bridge network, they can communicate with each other using their container names as hostnames. For example, container1 can access container2 by using the hostname "container2."

Let's create a custom bridge network named "my_custom_network" and run two containers attached to this network. The containers will be able to communicate with each other using their container names as hostnames.


