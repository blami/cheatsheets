# Docker
Docker cheatsheet.

## Build
``` sh
docker image build -t IMAGE:1.0.0 .
docker build -t IMAGE:1.0.0 .       # Build IMAGE:1.0.0 using Dockerfile in .
docker images
docker image ls                     # List all locally stored images
docker image rm IMAGE:1.0.0         # Remove local IMAGE:1.0.0
docker image prune [-a]             # Remove local unused dangling/[all] images
docker image history IMAGE          # Show history of IMAGE
```
NOTE: _Dangling_ image is image of fs layer that is not associated with any of
tagged images. _Unused_ image is any image that is not use by any container.


## Run
``` sh
docker run [--rm] IMAGE:1.0.0       # Run IMAGE:1.0.0 and clean up
docker run -d IMAGE:1.0.0           # Run IMAGE:1.0.0 in background
docker run -p DEST:SRC IMAGE:1.0.0  # Run IMAGE:1.0.0; expose port SRC as DEST
docker run --name NAME IMAGE:1.0.0  # Run IMAGE:1.0.0 as NAME
docker ps [-a]
docker container ls [-a]            # See running [-a] containers
docker stop|kill NAME               # Send SIGTERM|SIGKILL to container
docker rm -f $(docker ps -aq)       # Delete all (also stopped) containers
```
Run in background a container referred to as `NAME` using image `IMAGE:1.0.0`
exposing guest port `SRC` on host running Docker as `DEST`:
``` sh
docker run -d --name NAME -p DEST:SRC IMAGE:1.0.0
```


## Console and Logs
``` sh
docker exec -it NAME CMD            # Run CMD interactively in container NAME
docker attach NAME                  # Attach terminal to container NAME
docker container logs NAME
docker logs NAME                    # Show logs for container NAME
docker logs --tail N NAME           # Show last N lines of logs for NAME
```
Get `bash` in running container referred to as `NAME`:
``` sh
docker exec -it NAME /bin/bash
```


## Troubleshooting
#### Docker Desktop and WSL
- Enable _Expose daemon on tcp://localhost:2375 without TLS_
- In WSL `DOCKER_HOST=127.0.0.1:2375`
- To be able to pull images from Docker hub (to be able to `docker login`) in
  WSL inside your `$PATH` create `docker-credential-desktop` executable file
  with following contents:
  ``` sh
  #!/bin/sh
  /mnt/c/Program\ Files/Docker/Docker/resources/bin/docker-credential-desktop.exe $@
  ```
