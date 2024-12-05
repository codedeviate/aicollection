# docker build

The `docker build` command is used to build an image from a Dockerfile. This command reads the instructions from a Dockerfile and creates a Docker image based on those instructions.

## Basic Syntax
```sh
docker build [OPTIONS] PATH | URL | -
```

## Key Options and Parameters

1. **-t, --tag**: Name and optionally a tag in the 'name:tag' format.
   ```sh
   docker build -t myapp:latest .
   ```

2. **-f, --file**: Name of the Dockerfile (default is 'PATH/Dockerfile').
   ```sh
   docker build -f Dockerfile.dev -t myapp:dev .
   ```

3. **--build-arg**: Set build-time variables.
   ```sh
   docker build --build-arg VERSION=1.0 -t myapp:latest .
   ```

4. **--no-cache**: Do not use cache when building the image.
   ```sh
   docker build --no-cache -t myapp:latest .
   ```

5. **--rm**: Remove intermediate containers after a successful build (default is true).
   ```sh
   docker build --rm -t myapp:latest .
   ```

6. **--pull**: Always attempt to pull a newer version of the image.
   ```sh
   docker build --pull -t myapp:latest .
   ```

## Examples

1. **Building an Image from a Dockerfile**
   ```sh
   docker build -t myapp:latest .
   ```
   This command builds an image named `myapp` with the tag `latest` from the Dockerfile in the current directory.

2. **Specifying a Different Dockerfile**
   ```sh
   docker build -f Dockerfile.dev -t myapp:dev .
   ```
   This command builds an image using `Dockerfile.dev` instead of the default `Dockerfile`.

3. **Using Build Arguments**
   ```sh
   docker build --build-arg VERSION=1.0 -t myapp:latest .
   ```
   This command sets a build-time variable `VERSION` to `1.0`.

4. **Building Without Cache**
   ```sh
   docker build --no-cache -t myapp:latest .
   ```
   This command builds the image without using any cached layers.

5. **Pulling the Latest Base Image**
   ```sh
   docker build --pull -t myapp:latest .
   ```
   This command ensures that the latest version of the base image is used.

## Conclusion
The `docker build` command is essential for creating Docker images from a Dockerfile. Understanding its options and parameters allows you to effectively build and manage Docker images based on your requirements.