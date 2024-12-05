# docker ps

The `docker ps` command is used to list Docker containers. By default, it shows only running containers. Here is an in-depth explanation of `docker ps` along with examples and relevant switches and parameters.

## Basic Syntax
```sh
docker ps [OPTIONS]
```

## Key Options and Parameters

1. **-a, --all**: Show all containers (default shows just running).
   ```sh
   docker ps -a
   ```

2. **-q, --quiet**: Only display numeric IDs.
   ```sh
   docker ps -q
   ```

3. **--filter**: Filter output based on conditions provided.
   ```sh
   docker ps --filter "status=exited"
   ```

4. **--format**: Pretty-print containers using a Go template.
   ```sh
   docker ps --format "{{.ID}}: {{.Names}}"
   ```

5. **-n, --last**: Show n last created containers (includes all states).
   ```sh
   docker ps -n 5
   ```

6. **-s, --size**: Display total file sizes.
   ```sh
   docker ps -s
   ```

## Examples

1. **List Running Containers**
   ```sh
   docker ps
   ```
   This command lists all currently running containers.

2. **List All Containers**
   ```sh
   docker ps -a
   ```
   This command lists all containers, including those that are stopped.

3. **List Only Container IDs**
   ```sh
   docker ps -q
   ```
   This command lists only the IDs of all running containers.

4. **Filter Containers by Status**
   ```sh
   docker ps --filter "status=exited"
   ```
   This command lists only the containers that have exited.

5. **Format Output**
   ```sh
   docker ps --format "{{.ID}}: {{.Names}}"
   ```
   This command formats the output to show only the container ID and name.

6. **Show Last 5 Created Containers**
   ```sh
   docker ps -n 5
   ```
   This command lists the last 5 created containers, including all states.

7. **Display Total File Sizes**
   ```sh
   docker ps -s
   ```
   This command lists running containers and displays their total file sizes.

## Conclusion
The `docker ps` command is essential for managing and monitoring Docker containers. Understanding its options and parameters allows you to effectively list and filter containers based on your needs.