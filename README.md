# Docker Documentation

This documentation provides an overview of core concepts and commands related to Docker, a powerful containerization platform. It's designed to help learners understand Docker and get started with containerization for projects.

## Table of Contents

1. [What is Containerization](#what-is-containerization)
2. [Container vs Virtual Machine](#container-vs-virtual-machine)
3. [Docker](#docker)
4. [Docker Architecture](#docker-architecture)
5. [Docker Engine](#docker-engine)
6. [Docker Image](#docker-image)
    1. [Dockerfile](#dockerfile)
7. [Docker Container](#docker-container)
    1. [Docker Compose](#docker-compose)
8. [Docker Networking](#docker-networking)
    1. [Bridge Network](#bridge-network)
    2. [Host Network](#host-network)
    3. [None Network](#none-network)
9. [Docker Volume](#docker-volume)
10. [Docker Registry](#docker-registry)
    1. [Public Registry](#public-registry)
        1. [Docker Hub](#docker-hub)
    2. [Private Registry](#private-registry)

---

## 1. What is Containerization

Containerization is a lightweight form of virtualization that package and run applications and their dependencies in a consistent and isolated environment called a container. Containers are self-sufficient units that encapsulate an application and all the necessary components it needs to run, including libraries, runtime, and system tools. This encapsulation ensures that the application behaves consistently across different environments, from development to production, regardless of the underlying infrastructure.


## 2. Container vs Virtual Machine

Containers and virtual machines (VMs) are both methods of isolating applications, but they differ in their architecture. Here's a comparison of containers and virtual machines (VMs) to highlight their key differences:

| Concept                  | Containers               | Virtual Machines (VMs)  |
|-------------------------|--------------------------|-------------------------|
| **Isolation**           | Process and file system isolation. Containers share the host OS kernel, making them lightweight. | Full system virtualization, each VM runs its own complete OS instance, which is heavier. |
| **Resource Overhead**  | Minimal resource overhead. Containers use fewer resources due to kernel sharing. | Higher resource overhead. Each VM requires its own OS and consumes more resources. |
| **Portability**         | Highly portable. Containers can run consistently across different environments. | Less portable. VMs can be moved but may require conversion between hypervisor formats. |
| **Boot Time**           | Near-instant startup. Containers start quickly. | Slower startup. VMs require booting an entire OS. |
| **Performance**         | Better performance due to lower overhead and kernel sharing. | Slightly lower performance due to higher resource usage. |
| **Security**            | Containers offer good isolation but may share the same OS kernel, which can pose security risks if not configured properly. | VMs provide stronger isolation as they run separate OS instances, reducing the risk of kernel-level vulnerabilities. |
| **Management**          | Easier to manage and deploy due to their lightweight nature. | More complex to manage, especially when dealing with a large number of VMs. |
| **Scaling**             | Quick and efficient scaling. Containers can be spun up or down rapidly. | Slower scaling. VMs require more time to start and stop. |
| **Use Cases**           | Ideal for microservices, DevOps, and containerized applications. | Suited for running multiple applications with different OS requirements, legacy systems, and more traditional workloads. |
| **Hypervisor**          | No hypervisor required. Containers run on a container runtime (e.g., Docker). | Requires a hypervisor (e.g., VMware, VirtualBox) to manage and run VMs. |
| **Infrastructure**      | Designed for cloud-native and modern infrastructure. | Often used in traditional data center environments. |

It's important to choose between containers and VMs based on the specific requirements of developing applications and infrastructure. Containers are a great choice for cloud-native and microservices-based applications, while VMs are better suited for running legacy software or applications with diverse OS requirements. In some cases, a combination of both containers and VMs may be the most effective solution for complex environments.

## 3. Docker

Docker is a popular platform as a service (PaaS) for containerization. It creates, deploy, and run applications in lightweight, portable containers, which encapsulate an application and its dependencies. Here dependencies refers to the system libraries, runtimes, configuration files, database drivers etc. 


Imagine you have a lunchbox that holds your sandwich, fruit, and a drink. Docker is like a digital lunchbox that holds your software and everything it needs to work properly.



## 4. Docker Architecture

Docker follows a client-server architecture with three main components: the Docker client, Docker server (also known as the Docker daemon), and REST API.

#### Docker Client: 
The Docker client is the primary interface for users to interact with Docker. Users issue Docker commands through the Docker client's command-line interface (CLI). The client can run on the same system where the Docker server (daemon) is located, or it can connect to a remote Docker server.

#### Docker Server (Docker Daemon): 
The Docker server, also known as the Docker daemon, is responsible for managing Docker containers on a host system. It listens for Docker client requests and carries out the commands received. The daemon creates and manages containers, images, networks, and volumes.

#### REST API: 
The Docker server exposes a RESTful API that the client uses to communicate with it. Clients can make HTTP requests to the API to perform actions like creating, starting, stopping, or inspecting containers.


![image](https://github.com/rafid29mehda/Docker/assets/71279591/38024e07-7310-4b03-8c62-8670abb9f4b0)


## 5. Docker Engine

The Docker Engine, often referred to simply as "Docker," is the core component of the Docker platform responsible for building, running, and managing containers. It is the runtime environment that enables the creation and execution of Docker containers on a host system. 

## 6. Docker Image

A Docker image is a fundamental concept in Docker that serves as a template for creating containers. It encapsulates an application along with all its dependencies, libraries, and configuration settings, ensuring that the application runs consistently across different environments. Docker images are read-only, which means they remain unchanged once created. To modify an application or its configuration, we typically create a new image. Some common commands for docker image are written below-

- `docker images`: List available Docker images.
- `docker pull IMAGE[:TAG]`: Download an image from a registry.
- `docker build [options] PATH | URL`: Build a Docker image from a Dockerfile.
- `docker rmi IMAGE`: Remove an image.
- `docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`: Tag an image to give it a new name and/or version.

### 6.1 Dockerfile

A Dockerfile is a script that defines the instructions for creating a Docker image. A Dockerfile is a text file used to define the instructions for creating a Docker image. It specifies how an image should be built, what its base image is, which files and dependencies should be included, and what commands to run when a container is created from the image. Here's an explanation of some common instructions and variables used in a Dockerfile:

1. **`FROM` (Base Image):** This is the first instruction in a Dockerfile and defines the base image from which the image will be built. It sets the foundation for the image. For example, `FROM ubuntu:20.04` specifies the base image as Ubuntu 20.04.

2. **`WORKDIR` (Working Directory):** This instruction sets the working directory within the container where subsequent commands will be executed. It's equivalent to using the `cd` command in a shell. For example, `WORKDIR /app` sets the working directory to `/app`.

3. **`COPY` and `ADD` (Copying Files):** These instructions are used to copy files from the host system into the image. `COPY` is typically used to copy files from the build context (the directory where the Dockerfile is located) into the image. For example, `COPY app.py /app/` copies the `app.py` file from the build context to the `/app/` directory in the image.

4. **`RUN` (Run Commands):** The `RUN` instruction executes commands within the image, which can include installing packages, setting up dependencies, or configuring the environment. For example, `RUN apt-get update && apt-get install -y python` installs Python within the image.

5. **`CMD` and `ENTRYPOINT` (Container Startup Command):** These instructions specify the command that should be executed when a container is started from the image. `CMD` is often used to provide a default command that can be overridden when running the container, while `ENTRYPOINT` is used to define the main executable for the container. For example, `CMD ["python", "app.py"]` specifies that the Python script `app.py` should be executed when the container starts.

6. **Environment Variables:** We can define environment variables using the `ENV` instruction to set configuration values for the image. For example, `ENV MY_VARIABLE=my_value` sets the environment variable `MY_VARIABLE` to "my_value."

7. **`EXPOSE` (Port Mapping):** This instruction documents the ports that a container should listen on when it runs. It does not actually publish the ports but serves as documentation for the image's expected network behavior. For example, `EXPOSE 80` indicates that the container will listen on port 80.

These are some of the common instructions and variables in a Dockerfile. Dockerfiles are flexible and can be customized to suit the specific requirements of any application, making it easy to define how an application should be packaged and executed in a containerized environment.

Example:

```dockerfile
# Use an official Ubuntu image as the base
FROM ubuntu:20.04

# Set the working directory within the container
WORKDIR /app

# Copy application files from the host to the container
COPY app.py /app/
COPY requirements.txt /app/

# Define environment variables
ENV MY_VARIABLE=my_value
ENV DB_HOST=localhost
ENV DB_PORT=5432

# Install system packages and application dependencies
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    && pip3 install -r requirements.txt

# Expose port 80 for incoming connections
EXPOSE 80

# Define the command to run when the container starts
CMD ["python3", "app.py"]

```


## 7. Docker Container

Docker container is based on a Docker image, serving as a runtime instance of that image. It is like a virtual environment for running applications. Let's think of an image as a snapshot or a blueprint of a specific application setup. When we run a container, it's as if we're taking that snapshot and bringing it to life, creating a live instance of the application.

Here's how it works: When we define a Docker image in a Dockerfile, we specify what should be included in the image—things like the application code, system libraries, configurations, and environment variables. The image is static and doesn't change. It's like the master copy.

When we start a container from that image, it becomes a dynamic, running instance. The container is a lightweight, isolated environment where our application runs. It inherits everything from the image, including the application code and all the dependencies. It's similar to using a template to create multiple copies of a document, but each copy can be edited and is independent of the template. A few container management commands-

- `docker run [options] IMAGE [COMMAND] [ARG...]`: Create and start a new container from an image.
- `docker ps`: List running containers.
- `docker ps -a`: List all containers, including stopped ones.
- `docker start CONTAINER`: Start a stopped container.
- `docker stop CONTAINER`: Stop a running container.
- `docker restart CONTAINER`: Restart a container.
- `docker rm CONTAINER`: Remove a container.
- `docker logs CONTAINER`: View container logs.
- `docker exec -it CONTAINER [COMMAND]`: Run a command in a running container.


### 7.1 Docker Compose

Docker Compose is used for defining and running multi-container Docker applications. It specifies an application's services, networks, and volumes in a single file, making it easy to define, manage, and run complex, multi-container applications with a single command.

A `docker-compose.yml` file is used to define the configuration of the services and their interconnections. Here are some common components and variables used in a Docker Compose file:

1. **`version`:** Specifies the version of the Docker Compose file format being used. The format and features available may vary based on the version.

2. **`services`:** This section defines the various services (containers) that make up the application. Each service typically represents an individual component of the application, such as a web server, a database, or an application server.

3. **`image`:** Specifies the Docker image to use for the service. We can use pre-built images from Docker Hub or specify custom images.

4. **`build`:** If we want to build a custom image for a service, we can specify a build context (directory containing a Dockerfile) to build an image from the source code.

5. **`ports`:** Defines port mappings to expose a container's services to the host system or other containers.

6. **`environment`:** Sets environment variables for the container. This is useful for configuring application settings.

7. **`volumes`:** Specifies the volumes to mount inside the container, allowing for data persistence or sharing files between containers.

8. **`networks`:** Defines custom networks that the services should connect to. This helps manage communication between containers.

9. **`depends_on`:** Specifies dependencies between services, ensuring that one service starts only after another service is up and running.

10. **`command` and `entrypoint`: Customize the command or entrypoint that runs when the container starts.

11. **`restart`:** Determines how the service should be restarted in case of failures.

A basic `docker-compose.yml` look like this:

```yaml
version: '3'
services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
  app:
    build: ./myapp
    ports:
      - "5000:5000"
    depends_on:
      - db
  db:
    image: postgres:12
    environment:
      POSTGRES_PASSWORD: mysecretpassword
```

This Docker Compose file defines three services: a web server using the Nginx image, an application server built from a local directory, and a PostgreSQL database. It also specifies port mappings, environment variables, and dependencies between the services. Using `docker-compose`, we can start and manage this multi-container application with a single command. Commands to work with docker-compose-

- `docker-compose up`: Start containers based on the `docker-compose.yml` file.
- `docker-compose down`: Stop and remove containers, networks, and volumes.
- `docker-compose ps`: List the containers and their statuses.
- `docker-compose logs [sevice-name]`: Display logs for services or a specific service.
- `docker-compose exec [service-name] sh`: Execute a command in a service container.
- `docker-compose build`: Rebuild images for services with a `build` directive.
- `docker-compose pull`: Pull the latest images for services with an `image` directive.
- `docker-compose restart`: Restart running containers.



