# docker start

The `docker start` command is used to start one or more stopped containers. This command will start the containers that are in the stopped state.

## Basic Syntax
```sh
docker start [OPTIONS] CONTAINER [CONTAINER...]
```

## Key Options and Parameters

1. **-a, --attach**: Attach STDOUT/STDERR and forward signals.
   ```sh
   docker start -a mycontainer
   ```

2. **-i, --interactive**: Attach container's STDIN.
   ```sh
   docker start -i mycontainer
   ```

## Examples

1. **Starting a Single Container**
   ```sh
   docker start mycontainer
   ```
   This command starts the container named `mycontainer`.

2. **Starting Multiple Containers**
   ```sh
   docker start container1 container2 container3
   ```
   This command starts the containers named `container1`, `container2`, and `container3`.

3. **Starting and Attaching to a Container**
   ```sh
   docker start -a mycontainer
   ```
   This command starts the container named `mycontainer` and attaches to its STDOUT/STDERR.

4. **Starting a Container Interactively**
   ```sh
   docker start -i mycontainer
   ```
   This command starts the container named `mycontainer` and attaches to its STDIN.

## Conclusion
The `docker start` command is essential for starting stopped containers. Understanding its options and parameters allows you to effectively manage the startup process of your Docker containers.