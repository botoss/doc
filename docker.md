There are several advantages of using docker images for deploying our apps:
  1. App health-checking for free: if app crashes, Docker Swarm just restarts it again.
  2. We could use one Jenkins template for all projects, because building a project into Docker image can be universal, despite using different programming languages and platforms (JVM, Python, C++, etc.)
  3. Universal approach in managing apps lifecycle: we don't need to know app platform to start, stop, restart it, get its status, etc. Though, it can be achieved using systemd or something similar.

Though, there are disadvantages too:
  1. Seems like it's a bit difficult to start to work with Docker.
  2. Docker logs command sometimes doesn't show all logs due to some reason.

# DevOps

## Docker Swarm services operations

### Create service

`docker service create --name $SERVICE_NAME $CREATE_PARAMS $IMAGE_PATH`

### Update service

`docker service update $UPDATE_PARAMS $SERVICE_NAME`

### Remove service

`docker service rm $SERVICE_NAME`

### Show service logs

`docker service logs $SERVICE_NAME`
