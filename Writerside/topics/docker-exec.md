# docker exec

The `docker exec` command is used to run a command in a running container. This allows you to execute commands inside a container that is already running.

## Basic Syntax
```sh
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

## Key Options and Parameters

1. **-d, --detach**: Run command in the background.
   ```sh
   docker exec -d mycontainer touch /tmp/execWorks
   ```

2. **-i, --interactive**: Keep STDIN open even if not attached.
   ```sh
   docker exec -i mycontainer bash
   ```

3. **-t, --tty**: Allocate a pseudo-TTY.
   ```sh
   docker exec -t mycontainer bash
   ```

4. **-u, --user**: Username or UID to run the command as.
   ```sh
   docker exec -u root mycontainer bash
   ```

5. **-e, --env**: Set environment variables.
   ```sh
   docker exec -e "ENV_VAR=value" mycontainer bash
   ```

6. **-w, --workdir**: Working directory inside the container.
   ```sh
   docker exec -w /app mycontainer ls
   ```

## Examples

1. **Running a Command in a Container**
   ```sh
   docker exec mycontainer ls /app
   ```
   This command lists the contents of the `/app` directory inside the container named `mycontainer`.

2. **Running a Command in the Background**
   ```sh
   docker exec -d mycontainer touch /tmp/execWorks
   ```
   This command creates a file named `execWorks` in the `/tmp` directory inside the container named `mycontainer` and runs in the background.

3. **Running an Interactive Shell**
   ```sh
   docker exec -it mycontainer bash
   ```
   This command starts an interactive bash shell inside the container named `mycontainer`.

4. **Running a Command as a Different User**
   ```sh
   docker exec -u root mycontainer bash
   ```
   This command starts a bash shell inside the container named `mycontainer` as the root user.

5. **Setting Environment Variables**
   ```sh
   docker exec -e "ENV_VAR=value" mycontainer printenv ENV_VAR
   ```
   This command sets the environment variable `ENV_VAR` to `value` and prints it inside the container named `mycontainer`.

6. **Specifying a Working Directory**
   ```sh
   docker exec -w /app mycontainer ls
   ```
   This command lists the contents of the `/app` directory inside the container named `mycontainer`.

## Conclusion
The `docker exec` command is essential for running commands in a running container. Understanding its options and parameters allows you to effectively manage and interact with your Docker containers.