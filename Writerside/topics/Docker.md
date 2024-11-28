# Docker

### What is Docker?

Docker is an open-source platform that automates the deployment, scaling, and management of applications using containerization. Containers are lightweight, portable, and self-sufficient units that include everything needed to run a piece of software, including the code, runtime, libraries, and system tools.

### History of Docker

- **2013**: Docker was released as an open-source project by Solomon Hykes and his team at dotCloud.
- **2014**: Docker 1.0 was released, marking its first production-ready version.
- **2015**: Docker Inc. raised significant funding and gained widespread adoption.
- **2017**: Docker introduced the Moby Project, an open-source framework to assemble specialized container systems.
- **2018**: Docker announced Kubernetes support, integrating it with Docker Enterprise.
- **2020**: Docker refocused on developers, spinning off its enterprise business to Mirantis.

### Basic Concepts

- **Image**: A read-only template with instructions for creating a Docker container. Images are built from a Dockerfile.
- **Container**: A runnable instance of an image. Containers are isolated from each other and the host system.
- **Dockerfile**: A text file with instructions to build a Docker image.
- **Docker Hub**: A cloud-based repository where Docker users can share and manage images.

### Getting Started with Docker

#### 1. Install Docker

Follow the instructions on the [Docker website](https://docs.docker.com/get-docker/) to install Docker on your operating system.

#### 2. Write a Dockerfile

Create a `Dockerfile` to define your container. Here is an example for a simple Python application:

```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

#### 3. Build the Docker Image

Navigate to the directory containing your `Dockerfile` and run the following command to build the image:

```sh
docker build -t my-python-app .
```

#### 4. Run the Docker Container

Run the container using the image you just built:

```sh
docker run -p 4000:80 my-python-app
```

This command maps port 4000 on your host to port 80 in the container.

#### 5. Verify the Application

Open a web browser and navigate to `http://localhost:4000`. You should see your application running.

### Summary

- **Install Docker**: Follow the official installation guide.
- **Write a Dockerfile**: Define your container's environment.
- **Build the Image**: Use `docker build` to create an image.
- **Run the Container**: Use `docker run` to start a container from the image.

Docker simplifies the process of deploying applications by using containers, which are portable and consistent across different environments.