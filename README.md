# Docker-documentation-cheat-sheet
Docker cheat sheet
Docker Image

The docker images command in Docker is used to list all locally available Docker images on the host system. It provides a comprehensive overview of the images that have been pulled from a registry (like Docker Hub) or built locally using a Dockerfile.

Docker images are lightweight, standalone, executable packages that include everything needed to run a piece of software, including the code, a runtime, libraries, environment variables, and config files.
When you execute docker pull <image_name>[:<tag>], Docker connects to the specified registry (Docker Hub by default) and downloads the image with the given name and optional tag (e.g., ubuntu:latest, nginx:1.21). If no tag is specified, it defaults to latest.
```powershell
docker images
```

Docker pull
The docker pull command is used to download Docker images from a Docker registry to your local machine. 

```powershell
docker pull nignx
```
docker run

to run image for example - 
```
docker run nignx:latest
```
Docker ps
The command docker ps is used in Docker to list and display information about running Docker containers. The "ps" in docker ps stands for "Process Status"

```powershell
docker ps
```



