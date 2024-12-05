# docker network

The `docker network` command is used to manage Docker networks. Docker networks allow containers to communicate with each other and with the outside world. This command provides various subcommands to create, inspect, list, and remove networks.

## Basic Syntax
```sh
docker network [OPTIONS] COMMAND
```

## Subcommands and Options

1. **create**: Create a new network.
   ```sh
   docker network create [OPTIONS] NETWORK
   ```

   **Options:**
    - **-d, --driver**: Driver to manage the network (default is `bridge`).
      ```sh
      docker network create -d bridge mynetwork
      ```
    - **--subnet**: Subnet in CIDR format.
      ```sh
      docker network create --subnet 192.168.1.0/24 mynetwork
      ```
    - **--gateway**: IPv4 or IPv6 gateway for the master subnet.
      ```sh
      docker network create --gateway 192.168.1.1 mynetwork
      ```

2. **inspect**: Display detailed information on one or more networks.
   ```sh
   docker network inspect NETWORK
   ```

3. **ls**: List all networks.
   ```sh
   docker network ls
   ```

4. **rm**: Remove one or more networks.
   ```sh
   docker network rm NETWORK
   ```

5. **connect**: Connect a container to a network.
   ```sh
   docker network connect [OPTIONS] NETWORK CONTAINER
   ```

6. **disconnect**: Disconnect a container from a network.
   ```sh
   docker network disconnect [OPTIONS] NETWORK CONTAINER
   ```

## Examples

1. **Creating a Network**
   ```sh
   docker network create mynetwork
   ```
   This command creates a network named `mynetwork` with the default `bridge` driver.

2. **Creating a Network with a Specific Subnet and Gateway**
   ```sh
   docker network create --subnet 192.168.1.0/24 --gateway 192.168.1.1 mynetwork
   ```
   This command creates a network named `mynetwork` with the specified subnet and gateway.

3. **Listing All Networks**
   ```sh
   docker network ls
   ```
   This command lists all the networks available on the Docker host.

4. **Inspecting a Network**
   ```sh
   docker network inspect mynetwork
   ```
   This command displays detailed information about the network named `mynetwork`.

5. **Removing a Network**
   ```sh
   docker network rm mynetwork
   ```
   This command removes the network named `mynetwork`.

6. **Connecting a Container to a Network**
   ```sh
   docker network connect mynetwork mycontainer
   ```
   This command connects the container named `mycontainer` to the network named `mynetwork`.

7. **Disconnecting a Container from a Network**
   ```sh
   docker network disconnect mynetwork mycontainer
   ```
   This command disconnects the container named `mycontainer` from the network named `mynetwork`.

## Conclusion
The `docker network` command is essential for managing Docker networks. Understanding its subcommands and options allows you to effectively create, inspect, list, and remove networks, as well as connect and disconnect containers to and from networks.