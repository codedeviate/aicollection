# docker run

The `docker run` command is used to create and start a new container from a specified image. It is one of the most frequently used Docker commands. Here is an in-depth explanation of `docker run` along with examples and relevant switches and parameters.

## Basic Syntax
```sh
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

## Key Options and Parameters

1. **-d, --detach**: Run container in background and print container ID.
   ```sh
   docker run -d nginx
   ```

2. **-p, --publish**: Publish a container's port(s) to the host.
   ```sh
   docker run -d -p 80:80 nginx
   ```

3. **--name**: Assign a name to the container.
   ```sh
   docker run --name mynginx -d nginx
   ```

4. **-e, --env**: Set environment variables.
   ```sh
   docker run -e MY_ENV_VAR=value -d nginx
   ```

5. **-v, --volume**: Bind mount a volume.
   ```sh
   docker run -v /host/path:/container/path -d nginx
   ```

6. **--rm**: Automatically remove the container when it exits.
   ```sh
   docker run --rm -d nginx
   ```

7. **-it**: Run container in interactive mode with a terminal.
   ```sh
   docker run -it ubuntu /bin/bash
   ```

8. **--network**: Connect a container to a network.
   ```sh
   docker run --network mynetwork -d nginx
   ```

## Examples

1. **Running a Simple Container**
   ```sh
   docker run hello-world
   ```
   This command runs the `hello-world` image, which prints a message and exits.

2. **Running a Web Server**
   ```sh
   docker run -d -p 8080:80 nginx
   ```
   This command runs an Nginx web server in the background and maps port 80 of the container to port 8080 on the host.

3. **Running a Container with Environment Variables**
   ```sh
   docker run -d -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql
   ```
   This command runs a MySQL container with the root password set via an environment variable.

4. **Running a Container with a Volume**
   ```sh
   docker run -d -v /my/host/data:/var/lib/mysql mysql
   ```
   This command runs a MySQL container and mounts the host directory `/my/host/data` to `/var/lib/mysql` in the container.

5. **Running an Interactive Shell**
   ```sh
   docker run -it ubuntu /bin/bash
   ```
   This command runs an Ubuntu container and opens an interactive bash shell.

6. **Running a Container with a Custom Name**
   ```sh
   docker run --name mynginx -d nginx
   ```
   This command runs an Nginx container with the name `mynginx`.

7. **Running a Container on a Custom Network**
   ```sh
   docker network create mynetwork
   docker run --network mynetwork -d nginx
   ```
   This command first creates a custom network named `mynetwork` and then runs an Nginx container connected to this network.

## Conclusion
The `docker run` command is versatile and powerful, allowing you to configure and run containers with various options and parameters. Understanding these options helps you effectively manage and deploy your Docker containers.