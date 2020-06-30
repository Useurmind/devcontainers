# devcontainers

This repository provides a dev container and example code of how to start it for development.

You can use the visual studio code remote containers extension to develop inside the container.

https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers

# Use only docker

Build and run the container 

Powershell
```ps
docker build .\go_ansible\ -q | foreach { docker run -it $_ }
```

Build and run the container with a bind mount to preserve data between starts:

Powershell
```ps
$pwd = (Get-Location).Path; docker build .\go_ansible\ -q | foreach { docker run -it --mount type=bind,source=$pwd/data/dev,target=/home/dev $_ }
```

# Use a compose file

You can also use a docker compose file to start the dev container. See the example [docker-compose.yml](docker-compose.yml)

To run the dev container use 

    docker-compose run --name dev dev

You can also start other container in the same compose file which you can work with from the dev container.

    docker-compose run --name docker_server docker_server