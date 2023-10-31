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
    2. [Docker Compose](#docker-compose)
7. [Docker Container](#docker-container)
8. [Container Lifecycle](#container-lifecycle)
9. [Docker Networking](#docker-networking)
    1. [Bridge Network](#bridge-network)
    2. [Host Network](#host-network)
    3. [None Network](#none-network)
10. [Docker Volume](#docker-volume)
11. [Docker Registry](#docker-registry)
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

