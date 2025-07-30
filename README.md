# Docker-documentation-cheat-sheet
Docker Image

The docker images command in Docker is used to list all locally available Docker images on the host system. It provides a comprehensive overview of the images that have been pulled from a registry (like Docker Hub) or built locally using a Dockerfile.

Docker images are lightweight, standalone, executable packages that include everything needed to run a piece of software, including the code, a runtime, libraries, environment variables, and config files.

```powershell
docker images
```

Docker pull
The docker pull command is used to download Docker images from a Docker registry to your local machine. When you execute docker pull <image_name>[:<tag>], Docker connects to the specified registry (Docker Hub by default) and downloads the image with the given name and optional tag (e.g., ubuntu:latest, nginx:1.21). If no tag is specified, it defaults to latest.

```powershell
docker pull nginx
```
docker run
The docker run command is used to create and start a new Docker container from a specified Docker image. It is a fundamental command in Docker for launching applications within isolated environments. 
terminal gets freezed and when you close the terminal it also stops running container.

```
docker run nginx:latest
```
start a new container from a Docker image in detached mode. When you include -d, Docker starts the container in the background. Your terminal prompt will return immediately, and the container will continue to run even if you close the terminal session. This is ideal for running services, web applications, databases, or any long-running process that doesn't require direct interaction with your terminal.

```powershell
docker run -d nginx:latest
```
docker container -
command is used to list Docker containers.
This specifies that you are working with Docker containers.
ls: This is short for "list" and indicates that you want to list the specified Docker objects, in this case, containers.
By default, docker container ls will only show you running containers.
```powershell
docker container ls
```
Docker ps
The command docker ps is used in Docker to list and display information about running Docker containers. The "ps" in docker ps stands for "Process Status"

```powershell
docker ps
```
```powershell
docker ps -a 
```
-a (or --all): list all Docker containers, regardless of their current state (running, stopped, or exited).
```powershell
docker ps -aq
```
-a (or --all): This flag tells Docker to show all containers, whether they are running, stopped, or exited.
-q (or --quiet): This flag tells Docker to display only the numeric IDs of the containers. It suppresses all other information like image name, command, status, ports, and names.


Common Use Cases:

Removing all stopped/exited containers:

```powershell
docker rm $(docker ps -aq -f "status=exited")
```
docker ps -aq -f "status=exited": This part lists the IDs of only containers that have exited.
docker rm $(...): The $(...) syntax captures the output of the inner command and passes it as arguments to docker rm, effectively removing all those exited containers.

Stopping all running containers:
```powershell
docker stop $(docker ps -aq)
```
In this case, since docker stop can only stop running containers, docker ps -aq will provide the IDs of all containers (running or not). docker stop will simply ignore the IDs of containers that are already stopped. If you wanted only running ones, you'd use docker ps -q.

Removing all containers (running and stopped):
```powershell
docker rm -f $(docker ps -aq)
```
The -f (force) flag with docker rm is important here, as docker rm cannot remove running containers without it. This command will stop and then remove all containers.
In summary, docker ps -aq is a powerful and concise way to get a list of container IDs for further processing in the Docker CLI


-p or --publish: This is the flag that indicates you want to publish (map) a port.
```powershell
docker run -p <host_port>:<container_port> <image_name>
```
Without -p, your container/apartment has an internal door (its container port), but no one from outside the building knows about it.
Examples:
```powershell
docker run -p 8080:80 nginx
```
This starts an Nginx container.
Traffic to http://localhost:8080 on your host will be routed to port 80 inside the Nginx container.

Mapping to a Random Host Port:
```
docker run -p 80 nginx
```


