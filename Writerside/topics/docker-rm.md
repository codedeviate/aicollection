# docker rm

The `docker rm` command is used to remove one or more Docker containers. This command deletes the specified containers from the local Docker host.

## Basic Syntax
```sh
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

## Key Options and Parameters

1. **-f, --force**: Force the removal of a running container (uses SIGKILL).
   ```sh
   docker rm -f mycontainer
   ```

2. **-v, --volumes**: Remove the volumes associated with the container.
   ```sh
   docker rm -v mycontainer
   ```

3. **-l, --link**: Remove the specified link.
   ```sh
   docker rm -l mylink
   ```

4. **--force**: Force the removal of a container even if it is running.
   ```sh
   docker rm --force mycontainer
   ```

## Examples

1. **Removing a Single Container**
   ```sh
   docker rm mycontainer
   ```
   This command removes the container named `mycontainer`.

2. **Removing Multiple Containers**
   ```sh
   docker rm container1 container2 container3
   ```
   This command removes the containers named `container1`, `container2`, and `container3`.

3. **Forcing the Removal of a Running Container**
   ```sh
   docker rm -f mycontainer
   ```
   This command forcefully removes the running container named `mycontainer`.

4. **Removing a Container and Its Volumes**
   ```sh
   docker rm -v mycontainer
   ```
   This command removes the container named `mycontainer` and its associated volumes.

5. **Removing a Link**
   ```sh
   docker rm -l mylink
   ```
   This command removes the link named `mylink`.

## Conclusion
The `docker rm` command is essential for removing Docker containers. Understanding its options and parameters allows you to effectively manage and clean up containers on your Docker host.