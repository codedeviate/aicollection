# docker images

The `docker images` command is used to list all the images on your local Docker host. It provides information about the images, such as their repository, tag, image ID, creation date, and size.

## Basic Syntax
```sh
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

## Key Options and Parameters

1. **-a, --all**: Show all images (default hides intermediate images).
   ```sh
   docker images -a
   ```

2. **--digests**: Show digests.
   ```sh
   docker images --digests
   ```

3. **-q, --quiet**: Only show numeric IDs.
   ```sh
   docker images -q
   ```

4. **--filter**: Filter output based on conditions provided.
   ```sh
   docker images --filter "dangling=true"
   ```

5. **--format**: Pretty-print images using a Go template.
   ```sh
   docker images --format "{{.Repository}}: {{.Tag}}"
   ```

## Examples

1. **List All Images**
   ```sh
   docker images
   ```
   This command lists all images on the local Docker host.

2. **List All Images Including Intermediate Images**
   ```sh
   docker images -a
   ```
   This command lists all images, including intermediate images used in the build process.

3. **List Only Image IDs**
   ```sh
   docker images -q
   ```
   This command lists only the IDs of all images.

4. **Filter Images by Dangling Status**
   ```sh
   docker images --filter "dangling=true"
   ```
   This command lists only the images that are not tagged and are not referenced by any container.

5. **Show Digests**
   ```sh
   docker images --digests
   ```
   This command lists images along with their digests.

6. **Format Output**
   ```sh
   docker images --format "{{.Repository}}: {{.Tag}}"
   ```
   This command formats the output to show only the repository and tag of each image.

## Conclusion
The `docker images` command is useful for managing and inspecting Docker images on your local host. Understanding its options and parameters allows you to effectively list and filter images based on your needs.