# docker login

The `docker login` command is used to log in to a Docker registry. This command stores the credentials in the Docker configuration file, allowing you to interact with the specified registry.

## Basic Syntax
```sh
docker login [OPTIONS] [SERVER]
```

## Parameters

1. **OPTIONS**: Various options to customize the login process, such as `--username` and `--password`.
2. **SERVER**: The registry server to log in to. If not specified, Docker defaults to Docker Hub (`https://index.docker.io/v1/`).

## Examples

1. **Logging in to Docker Hub**
   ```sh
   docker login
   ```
   This command prompts for your Docker Hub username and password.

2. **Logging in to a Private Registry**
   ```sh
   docker login myprivateregistry.com
   ```
   This command prompts for your username and password for the specified private registry.

3. **Logging in with Username and Password**
   ```sh
   docker login --username myusername --password mypassword myprivateregistry.com
   ```
   This command logs in to the specified private registry using the provided username and password.

## Conclusion
The `docker login` command is essential for authenticating with Docker registries. Understanding its parameters allows you to effectively manage your Docker registry logins.