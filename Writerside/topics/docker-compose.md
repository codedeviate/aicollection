# docker-compose

The `docker-compose` command is used to define and run multi-container Docker applications. With `docker-compose`, you can use a YAML file to configure your application's services, networks, and volumes, and then start all the services with a single command.

## Basic Syntax
```sh
docker-compose [OPTIONS] COMMAND
```

## Key Commands and Options

1. **up**: Create and start containers.
   ```sh
   docker-compose up [OPTIONS] [SERVICE...]
   ```

   **Options:**
    - **-d, --detach**: Run containers in the background.
      ```sh
      docker-compose up -d
      ```
    - **--build**: Build images before starting containers.
      ```sh
      docker-compose up --build
      ```

2. **down**: Stop and remove containers, networks, images, and volumes.
   ```sh
   docker-compose down [OPTIONS]
   ```

   **Options:**
    - **-v, --volumes**: Remove named volumes declared in the `volumes` section of the Compose file and anonymous volumes attached to containers.
      ```sh
      docker-compose down -v
      ```

3. **build**: Build or rebuild services.
   ```sh
   docker-compose build [OPTIONS] [SERVICE...]
   ```

   **Options:**
    - **--no-cache**: Do not use cache when building the image.
      ```sh
      docker-compose build --no-cache
      ```

4. **ps**: List containers.
   ```sh
   docker-compose ps [OPTIONS] [SERVICE...]
   ```

5. **logs**: View output from containers.
   ```sh
   docker-compose logs [OPTIONS] [SERVICE...]
   ```

   **Options:**
    - **-f, --follow**: Follow log output.
      ```sh
      docker-compose logs -f
      ```

6. **exec**: Execute a command in a running container.
   ```sh
   docker-compose exec [OPTIONS] SERVICE COMMAND [ARGS...]
   ```

   **Options:**
    - **-d, --detach**: Run command in the background.
      ```sh
      docker-compose exec -d web bash
      ```

## Examples

1. **Starting Services**
   ```sh
   docker-compose up
   ```
   This command starts all the services defined in the `docker-compose.yml` file.

2. **Starting Services in Detached Mode**
   ```sh
   docker-compose up -d
   ```
   This command starts all the services in the background.

3. **Stopping and Removing Services**
   ```sh
   docker-compose down
   ```
   This command stops and removes all the services, networks, and volumes defined in the `docker-compose.yml` file.

4. **Building Services**
   ```sh
   docker-compose build
   ```
   This command builds the images for the services defined in the `docker-compose.yml` file.

5. **Listing Running Containers**
   ```sh
   docker-compose ps
   ```
   This command lists all the running containers for the services defined in the `docker-compose.yml` file.

6. **Viewing Logs**
   ```sh
   docker-compose logs
   ```
   This command shows the logs for all the services defined in the `docker-compose.yml` file.

7. **Executing a Command in a Running Container**
   ```sh
   docker-compose exec web bash
   ```
   This command opens a bash shell in the running container for the `web` service.

## Conclusion
The `docker-compose` command is essential for managing multi-container Docker applications. Understanding its commands and options allows you to effectively define, start, stop, and manage your Docker services.