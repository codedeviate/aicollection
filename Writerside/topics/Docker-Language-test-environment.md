# Language test environment

This is a test environment for various programming languages (most of the languages found [here](Languages.md) can be found in this Dockerfile). The purpose of this document is to provide a consistent structure for documenting code snippets, examples, and instructions related to different programming languages. Each section will focus on a specific language and include relevant information such as code examples, explanations, and instructions for running programs.

## Dockerfile
Here is a Dockerfile based on a lightweight Linux distribution (Alpine) that includes GCC, Fortran, Java, and several other compilers:

```Docker
# Use the official lightweight Alpine Linux image
FROM alpine:latest

# Install necessary packages and compilers
RUN apk update && apk add --no-cache \
    nano \
    build-base \
    gfortran \
    openjdk11-jdk \
    python3 \
    py3-pip \
    ruby \
    rust \
    go \
    nodejs \
    npm \
    perl \
    bash \
    nasm

# Verify installations
RUN gcc --version >> /installed_compilers.txt && \
    gfortran --version >> /installed_compilers.txt && \
    as --version >> /installed_compilers.txt && \
    nasm --version >> /installed_compilers.txt && \
    java -version && >> /installed_compilers.txt \
    python3 --version && >> /installed_compilers.txt \
    ruby --version && >> /installed_compilers.txt \
    rustc --version && >> /installed_compilers.txt \
    go version && >> /installed_compilers.txt \
    node --version && >> /installed_compilers.txt \
    perl --version >> /installed_compilers.txt

# Set the default command to run when starting the container
CMD ["/bin/bash"]
```

## Instructions to Build and Run the Docker Container

1. **Save the Dockerfile**: Save the above Dockerfile in a file named `Dockerfile`.

2. **Build the Docker Image**: Open a terminal and navigate to the directory containing the Dockerfile. Run the following command to build the Docker image:

   ```sh
   docker build -t multi-compiler-env .
   ```

   This command builds the Docker image and tags it as `multi-compiler-env`.

3. **Run the Docker Container**: After the image is built, run the following command to start a container from the image:

   ```sh
   docker run -it multi-compiler-env
   ```

   This command starts the container and opens an interactive terminal session with the Bash shell. You can now use the installed compilers within the container.

## Makefile

Here is a `Makefile` to build and run the Docker container described in the `Dockerfile`:

```Make
# Makefile for building and running the Docker container

# Image name
IMAGE_NAME = multi-compiler-env

# Build the Docker image
build:
	docker build -t $(IMAGE_NAME) .

# Run the Docker container
run:
	docker run -it $(IMAGE_NAME)

# Clean up the Docker image
clean:
	docker rmi $(IMAGE_NAME)

# Default target
all: build run
```

### Explanation
- **IMAGE_NAME**: Defines the name of the Docker image.
- **build**: Target to build the Docker image.
- **run**: Target to run the Docker container.
- **clean**: Target to remove the Docker image.
- **all**: Default target that builds and runs the Docker container.


## Change shell
To change the shell to `sh` or `zsh` in the Docker container, you can use the following command:

```sh
docker run -it --entrypoint /bin/zsh multi-compiler-env
```

Or you could change the `CMD` in the Dockerfile to use a different shell:

```Docker
CMD ["/bin/zsh"]
```

### Makefile for Changing the Shell

Here is the updated `Makefile` to include ways to use `sh`, `zsh`, and `tcsh` as the shell:

```Make
# Makefile for building and running the Docker container

# Image name
IMAGE_NAME = multi-compiler-env
MOUNT_CODE = -v ./opt:/opt

# Build the Docker image
build:
	docker build -t $(IMAGE_NAME) .

# Run the Docker container with default shell (bash)
run:
	docker run -it $(MOUNT_CODE) $(IMAGE_NAME)

# Run the Docker container with sh shell
run-sh:
	docker run -it --entrypoint /bin/sh $(MOUNT_CODE) $(IMAGE_NAME)

# Run the Docker container with zsh shell
run-zsh:
	docker run -it --entrypoint /bin/zsh $(MOUNT_CODE) $(IMAGE_NAME)

# Run the Docker container with tcsh shell
run-tcsh:
	docker run -it --entrypoint /bin/tcsh $(MOUNT_CODE) $(IMAGE_NAME)

# Clean up the Docker image
clean:
	docker rmi $(IMAGE_NAME)

# Default target
all: build run

```

### Explanation of updated Makefile
- **MOUNT_CODE**: Mounts the `opt` directory to the container to share code between the host and the container.
- **run-sh**: Target to run the Docker container with `sh` shell.
- **run-bash**: Target to run the Docker container with `bash` shell. (This is the default behavior and the same ad `run`.)
- **run-zsh**: Target to run the Docker container with `zsh` shell.
- **run-tcsh**: Target to run the Docker container with `tcsh` shell.
