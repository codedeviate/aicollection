# docker stop

The `docker stop` command is used to stop one or more running containers. This command sends a SIGTERM signal to the main process inside the container, giving it a chance to gracefully shut down.

## Basic Syntax
```sh
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

## Key Options and Parameters

1. **-t, --time**: Seconds to wait for the container to stop before killing it (default is 10 seconds).
   ```sh
   docker stop -t 5 mycontainer
   ```

## Examples

1. **Stopping a Single Container**
   ```sh
   docker stop mycontainer
   ```
   This command stops the container named `mycontainer`.

2. **Stopping Multiple Containers**
   ```sh
   docker stop container1 container2 container3
   ```
   This command stops the containers named `container1`, `container2`, and `container3`.

3. **Stopping a Container with a Custom Timeout**
   ```sh
   docker stop -t 20 mycontainer
   ```
   This command stops the container named `mycontainer` and waits 20 seconds for it to gracefully shut down before forcefully killing it.

## Conclusion
The `docker stop` command is essential for stopping running containers. Understanding its options and parameters allows you to effectively manage the shutdown process of your Docker containers.