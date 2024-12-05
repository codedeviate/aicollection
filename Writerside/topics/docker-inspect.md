# docker inspect

The `docker inspect` command is used to return detailed information about Docker objects such as containers, images, volumes, and networks in JSON format. This command is useful for debugging and understanding the configuration and state of Docker objects.

## Basic Syntax
```sh
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```

## Key Options and Parameters

1. **-f, --format**: Format the output using a Go template.
   ```sh
   docker inspect -f '{{.State.Running}}' mycontainer
   ```

2. **--type**: Return JSON for specified type (e.g., container, image, volume, network).
   ```sh
   docker inspect --type container mycontainer
   ```

## Examples

1. **Inspecting a Container**
   ```sh
   docker inspect mycontainer
   ```
   This command returns detailed information about the container named `mycontainer`.

2. **Inspecting an Image**
   ```sh
   docker inspect myimage
   ```
   This command returns detailed information about the image named `myimage`.

3. **Inspecting a Volume**
   ```sh
   docker inspect myvolume
   ```
   This command returns detailed information about the volume named `myvolume`.

4. **Inspecting a Network**
   ```sh
   docker inspect mynetwork
   ```
   This command returns detailed information about the network named `mynetwork`.

5. **Formatting the Output**
   ```sh
   docker inspect -f '{{.State.Running}}' mycontainer
   ```
   This command returns the running state of the container named `mycontainer` using a Go template.

6. **Specifying the Type**
   ```sh
   docker inspect --type container mycontainer
   ```
   This command returns JSON formatted information specifically for the container named `mycontainer`.

## Conclusion
The `docker inspect` command is essential for retrieving detailed information about Docker objects. Understanding its options and parameters allows you to effectively debug and manage your Docker containers, images, volumes, and networks.