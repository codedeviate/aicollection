# docker pull

The `docker pull` command is used to download Docker images from a registry, such as Docker Hub. This command fetches the specified image and its layers from the registry and stores them in your local Docker host.

## Basic Syntax
```sh
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```

## Key Options and Parameters

1. **--all-tags, -a**: Download all tagged images in the repository.
   ```sh
   docker pull -a ubuntu
   ```

2. **--disable-content-trust**: Skip image verification (default is true).
   ```sh
   docker pull --disable-content-trust ubuntu
   ```

## Examples

1. **Pulling a Specific Image**
   ```sh
   docker pull nginx
   ```
   This command pulls the latest version of the `nginx` image from Docker Hub.

2. **Pulling a Specific Tag**
   ```sh
   docker pull ubuntu:20.04
   ```
   This command pulls the `ubuntu` image with the tag `20.04`.

3. **Pulling All Tags**
   ```sh
   docker pull -a ubuntu
   ```
   This command pulls all available tags of the `ubuntu` image.

4. **Pulling an Image by Digest**
   ```sh
   docker pull ubuntu@sha256:12345abcde...
   ```
   This command pulls the `ubuntu` image with the specified digest.

## Conclusion
The `docker pull` command is essential for downloading images from a registry to your local Docker host. Understanding its options and parameters allows you to effectively manage and retrieve Docker images based on your needs.