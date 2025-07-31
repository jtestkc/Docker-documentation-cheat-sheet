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
Docker will pick a random, available high-numbered port on your host and map it to container port 80.
You can then use docker ps to see which host port was assigned (e.g., 0.0.0.0:32768->80/tcp).

Mapping a Range of Ports:
You can map a range of host ports to a range of container ports.
```
docker run -p 8000-8005:80-85 my-app-image
```
Host 8000 maps to container 80, host 8001 maps to container 81, and so on.

Specifying Protocol (TCP/UDP):
By default, -p maps TCP ports. You can explicitly specify UDP if needed:
```
docker run -p 53:53/udp bind9-image
```
Binding to a Specific Host IP Address:
If your host machine has multiple IP addresses and you want the service to be accessible only on a particular one:
```
docker run -p 192.168.1.100:80:80 nginx
```
This maps host IP 192.168.1.100 port 80 to container port 80

Docker name 
--name flag in Docker is used with commands like docker run to assign a custom, human-readable name to your Docker container.
```
docker run --name <your_custom_name> <image_name>
```
Readability and Memorability:

Without --name: If you don't specify a name, Docker will automatically generate a random, often quirky, name for your container (e.g., stoic_murdock, jolly_bose, hungry_carson). While unique, these are hard to remember or identify.
With --name: You can give your container a descriptive name like my-web-server, database-dev, cms-app, making it immediately clear what the container's purpose is.

Network Aliasing (within Docker networks):
When containers are connected to user-defined Docker networks, the --name of a container also acts as a DNS alias within that network. This means other containers on the same network can reach your container simply by its name, rather than needing to know its IP address. This is crucial for multi-container applications (e.g., a web app container connecting to a database container).

# Create a network
```
docker network create my-app-network
```
# Run a database container in the network
```
docker run -d --name my-db --network my-app-network mysql:latest
```
# Run a web app container that connects to the database
```
docker run -d --name my-web --network my-app-network my-web-app:latest
```

docker ps --format provides immense flexibility for tailoring the output of your container list, making it invaluable for both interactive use and scripting.
```
docker ps--format="ID\t{{.ID}}\nNAME\t{{.Names}}\nIMAGE\t{{.Image}}\nPORTS\t{{.Ports}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSTATUS\t{{.Status}}\n"
```
Making it Permanent:

You can set a default format for docker ps in your Docker configuration file (~/.docker/config.json) by adding a psFormat entry:
```json
{
  "psFormat": "table {{.Names}}\t{{.Image}}\t{{.Status}}\t{{.Ports}}"
}
```
(Remember to escape backslashes if editing directly in JSON).

