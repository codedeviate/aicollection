# docker tag

The `docker tag` command is used to create a tag for an existing Docker image. This command allows you to add a new name to an existing image, which can be useful for versioning and organizing your images.

## Basic Syntax
```sh
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

## Parameters

1. **SOURCE_IMAGE[:TAG]**: The name (and optionally a tag) of the source image.
2. **TARGET_IMAGE[:TAG]**: The name (and optionally a tag) of the target image.

## Examples

1. **Tagging an Image with a New Name**
   ```sh
   docker tag myimage:latest myrepository/myimage:latest
   ```
   This command tags the image `myimage:latest` with a new name `myrepository/myimage:latest`.

2. **Tagging an Image with a New Version**
   ```sh
   docker tag myimage:latest myimage:v1.0
   ```
   This command tags the image `myimage:latest` with a new version `myimage:v1.0`.

3. **Tagging an Image with a Different Repository**
   ```sh
   docker tag myimage:latest myrepository/myimage:v1.0
   ```
   This command tags the image `myimage:latest` with a new repository and version `myrepository/myimage:v1.0`.

## Conclusion
The `docker tag` command is essential for managing Docker image names and versions. Understanding its parameters allows you to effectively organize and version your Docker images.