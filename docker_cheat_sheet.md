# Docker Advanced Cheat Sheet

## 1. **Installation**

- **Install Docker Engine**: Follow the [official Docker installation guide](https://docs.docker.com/get-docker/).
- **Install Docker Compose**: Follow the [official Docker Compose installation guide](https://docs.docker.com/compose/install/).

## 2. **Docker Commands**

- **Check Docker Version**:
  ```sh
  docker --version
  ```

- **Check Docker Compose Version**:
  ```sh
  docker-compose --version
  ```

- **List Docker Images**:
  ```sh
  docker images
  ```

- **List Docker Containers**:
  ```sh
  docker ps
  ```

- **Stop a Running Container**:
  ```sh
  docker stop <container_id>
  ```

- **Remove a Container**:
  ```sh
  docker rm <container_id>
  ```

- **Remove an Image**:
  ```sh
  docker rmi <image_id>
  ```

- **Build an Image**:
  ```sh
  docker build -t <image_name>:<tag> .
  ```

- **Run a Container**:
  ```sh
  docker run -d --name <container_name> <image_name>:<tag>
  ```

- **Execute a Command in a Running Container**:
  ```sh
  docker exec -it <container_id> <command>
  ```

## 3. **Dockerfile Basics**

- **Basic Dockerfile Structure**:
  ```Dockerfile
  # Use an image as a parent image
  FROM <base_image>:<tag>

  # Set the working directory in the container
  WORKDIR /app

  # Copy the current directory contents into the container at /app
  COPY . /app

  # Install any needed packages
  RUN <install_command>

  # Make a port available to the world outside the container
  EXPOSE <port>

  # Define environment variable
  ENV <key>=<value>

  # Run a command when the container launches
  CMD ["<command>", "<arg1>", "<arg2>"]
  ```

- **Example Dockerfile**:
  ```Dockerfile
  FROM python:3.9-slim

  WORKDIR /app

  COPY requirements.txt ./
  RUN pip install --no-cache-dir -r requirements.txt

  COPY . .

  EXPOSE 8000

  CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
  ```

## 4. **Docker Compose**

- **Basic `docker-compose.yml` Structure**:
  ```yaml
  version: '3'

  services:
    web:
      image: <image_name>:<tag>
      ports:
        - "5000:5000"
      volumes:
        - .:/app
      environment:
        - ENV_VAR=value
  ```

- **Start Services**:
  ```sh
  docker-compose up
  ```

- **Stop Services**:
  ```sh
  docker-compose down
  ```

- **Build and Start Services**:
  ```sh
  docker-compose up --build
  ```

## 5. **Volumes and Bind Mounts**

- **Create a Volume**:
  ```sh
  docker volume create <volume_name>
  ```

- **Use a Volume in Docker Run**:
  ```sh
  docker run -v <volume_name>:/path/in/container <image_name>
  ```

- **Use a Bind Mount in Docker Run**:
  ```sh
  docker run -v /host/path:/container/path <image_name>
  ```

- **List Volumes**:
  ```sh
  docker volume ls
  ```

- **Remove a Volume**:
  ```sh
  docker volume rm <volume_name>
  ```

## 6. **Networking**

- **List Docker Networks**:
  ```sh
  docker network ls
  ```

- **Create a Network**:
  ```sh
  docker network create <network_name>
  ```

- **Connect a Container to a Network**:
  ```sh
  docker network connect <network_name> <container_name>
  ```

- **Disconnect a Container from a Network**:
  ```sh
  docker network disconnect <network_name> <container_name>
  ```

## 7. **Docker Swarm**

- **Initialize Docker Swarm**:
  ```sh
  docker swarm init
  ```

- **Create a Service**:
  ```sh
  docker service create --name <service_name> -p 80:80 <image_name>
  ```

- **List Services**:
  ```sh
  docker service ls
  ```

- **Scale a Service**:
  ```sh
  docker service scale <service_name>=<replica_count>
  ```

- **Remove a Service**:
  ```sh
  docker service rm <service_name>
  ```

## 8. **Security**

- **Scan Images for Vulnerabilities**:
  ```sh
  docker scan <image_name>
  ```

- **Limit Container Resources**:
  ```sh
  docker run -m 512m --cpus="1.0" <image_name>
  ```

## 9. **Logging and Monitoring**

- **View Container Logs**:
  ```sh
  docker logs <container_id>
  ```

- **Stream Container Logs**:
  ```sh
  docker logs -f <container_id>
  ```

- **Use Docker Stats**:
  ```sh
  docker stats
  ```

## 10. **Optimizing Docker Images**

- **Minimize Image Size**:
  - Use multi-stage builds:
    ```Dockerfile
    # Stage 1: Build stage
    FROM node:14 AS build
    WORKDIR /app
    COPY . .
    RUN npm install
    RUN npm run build

    # Stage 2: Production stage
    FROM nginx:alpine
    COPY --from=build /app/build /usr/share/nginx/html
    ```

- **Use Smaller Base Images**:
  - Opt for Alpine-based images when possible (e.g., `python:3.9-alpine`).

## 11. **Advanced Dockerfile Features**

- **Build Arguments**:
  ```Dockerfile
  ARG BUILD_ENV=production
  ENV ENVIRONMENT=${BUILD_ENV}
  ```

- **Labels**:
  ```Dockerfile
  LABEL maintainer="your_email@example.com"
  ```

- **Health Checks**:
  ```Dockerfile
  HEALTHCHECK --interval=30s --timeout=10s \
    CMD curl -f http://localhost/ || exit 1
  ```

## 12. **Docker Security Best Practices**

- **Run Containers as Non-Root User**:
  ```Dockerfile
  USER nonrootuser
  ```

- **Use Read-Only Filesystem**:
  ```sh
  docker run --read-only <image_name>
  ```

- **Avoid Using Latest Tags**: Specify exact version tags to ensure consistency.

## 13. **Multi-Stage Builds**

- **Example Multi-Stage Build**:
  ```Dockerfile
  # Stage 1: Build stage
  FROM golang:1.16 AS build
  WORKDIR /app
  COPY . .
  RUN go build -o myapp

  # Stage 2: Final stage
  FROM scratch
  COPY --from=build /app/myapp /myapp
  ENTRYPOINT ["/myapp"]
  ```

## 14. **Docker Registries**

- **Login to Docker Hub**:
  ```sh
  docker login
  ```

- **Push an Image to Docker Hub**:
  ```sh
  docker tag <image_name>:<tag> <username>/<repo>:<tag>
  docker push <username>/<repo>:<tag>
  ```

- **Pull an Image from Docker Hub**:
  ```sh
  docker pull <username>/<repo>:<tag>
  ```

- **Configure a Private Registry**:
  - Add registry configuration to Docker:
    ```json
    {
      "insecure-registries" : ["my-registry.local"]
    }
    ```

## 15. **Troubleshooting**

- **Inspect Container**:
  ```sh
  docker inspect <container_id>
  ```

- **Check Container Logs**:
  ```sh
  docker logs <container_id>
  ```

- **Run a Container in Interactive Mode**:
  ```sh
  docker run -it <image_name> /bin/bash
  ```

---

This comprehensive cheat sheet covers advanced Docker features, best practices, and troubleshooting tips. For further details, consult the [official Docker documentation](https://docs.docker.com/).