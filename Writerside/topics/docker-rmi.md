# docker rmi

The `docker rmi` command is used to remove one or more Docker images from your local Docker host. This command deletes the specified images, freeing up space and helping to manage your local image repository.

## Basic Syntax
```sh
docker rmi [OPTIONS] IMAGE [IMAGE...]
```

## Key Options and Parameters

1. **-f, --force**: Force the removal of an image.
   ```sh
   docker rmi -f myimage
   ```

2. **--no-prune**: Do not delete untagged parent images.
   ```sh
   docker rmi --no-prune myimage
   ```

## Examples

1. **Removing a Single Image**
   ```sh
   docker rmi myimage
   ```
   This command removes the image named `myimage`.

2. **Removing Multiple Images**
   ```sh
   docker rmi image1 image2 image3
   ```
   This command removes the images named `image1`, `image2`, and `image3`.

3. **Forcing the Removal of an Image**
   ```sh
   docker rmi -f myimage
   ```
   This command forcefully removes the image named `myimage`.

4. **Removing an Image Without Pruning Parent Images**
   ```sh
   docker rmi --no-prune myimage
   ```
   This command removes the image named `myimage` but does not delete any untagged parent images.

## Conclusion
The `docker rmi` command is essential for removing Docker images from your local Docker host. Understanding its options and parameters allows you to effectively manage and clean up images on your Docker host.