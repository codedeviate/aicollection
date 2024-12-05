# docker push

The `docker push` command is used to upload a Docker image to a Docker registry. This command is essential for sharing images with others and deploying applications.

## Basic Syntax
```sh
docker push [OPTIONS] NAME[:TAG]
```

## Parameters

1. **NAME[:TAG]**: The name (and optionally a tag) of the image to push. If no tag is specified, `latest` is used by default.

## Examples

1. **Pushing an Image to Docker Hub**
   ```sh
   docker push myrepository/myimage:latest
   ```
   This command pushes the image `myrepository/myimage:latest` to Docker Hub.

2. **Pushing an Image with a Specific Tag**
   ```sh
   docker push myrepository/myimage:v1.0
   ```
   This command pushes the image `myrepository/myimage:v1.0` to Docker Hub.

3. **Pushing an Image to a Private Registry**
   ```sh
   docker push myprivateregistry.com/myrepository/myimage:latest
   ```
   This command pushes the image `myprivateregistry.com/myrepository/myimage:latest` to a private registry.

## Conclusion
The `docker push` command is essential for uploading Docker images to a registry. Understanding its parameters allows you to effectively share and deploy your Docker images.