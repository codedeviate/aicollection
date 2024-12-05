# docker logout

The `docker logout` command is used to log out from a Docker registry. This command removes the credentials stored in the Docker configuration file, effectively ending the session with the specified registry.

## Basic Syntax
```sh
docker logout [SERVER]
```

## Parameters

1. **SERVER**: The registry server to log out from. If not specified, Docker defaults to Docker Hub (`https://index.docker.io/v1/`).

## Examples

1. **Logging out from Docker Hub**
   ```sh
   docker logout
   ```
   This command logs out from Docker Hub.

2. **Logging out from a Private Registry**
   ```sh
   docker logout myprivateregistry.com
   ```
   This command logs out from the specified private registry.

## Conclusion
The `docker logout` command is essential for securely ending sessions with Docker registries. Understanding its parameters allows you to effectively manage your Docker registry logins.