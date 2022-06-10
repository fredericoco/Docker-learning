# What is Docker?

 Docker is a platform that lets you package, develop, and run applications in containers. A container is a virtual environment on top of the OS kernel to capture all of its software - libraries, dependencies, etc.

## Why does Docker matter?

 A more lightweight approach than virtual machines to isolated coding and project environments. Portability to the major architectures and operating systems. Helps achieve continuous integration and deployment for development operations.

## Who does docker affect most?

 Developers and software engineers. Operators and DevOps engineers. Start ups and enterprises.

## Main features

 Create containers and images. Docker compose for multicontainer applications. Docker swarm to utilize multiple machines running Docker.

 https://github.com/15Dkatz/docker-guides

## The Kernel

 The kernel is the software at the core of an operating system, with complete control. The CPU is the core circuitry which executes program instructions. Docker runs on top of original kernel - making it the host machine.
![image](https://media.discordapp.net/attachments/693899305584558081/984822350270828574/unknown.png)
## The docker engine

 Consists of the docker server, an API, and command line interface. The server is also called the docker daemon. A daemon is a background process on an operating system. Docker daemon is like a construction team on the host machine.
![image](https://cdn.discordapp.com/attachments/693899305584558081/984820986522239037/unknown.png)
## Docker container environments

The processes of one container cannot affect the process of another. A container has limits on resource usage like the CPU and memory. Application-specific code.

## What is a docker container?

A Docker container is a loosely isolated environment running within a host machine's kernel that allows us to run application-specific code.

## Why are containers useful?

Portability to multiple operating system environments.Less time setting up, more time coding. Development, continuous integration, deployment environments.

## Containers vs Virtual machines

Virtual machines abstracts an entire computer system. To run 2GB of software, on a VM it will require 2GBs to run the image, so on 5VMs it will require 10GB. To run it on containers you will need 2GB +0.001^Nn to run it. This is because of the file system and both systems have their advantages and disadvantages.

## Docker Images
Read only templates with instructions for creating docker container. Define the container code,libraries, environment variables, configuration files and more.

## Dockerfile

Outlines instructions for how an image will create a container.
## Image to container relationship
![](images\image%20to%20container.png)
## Dockerhub
Collects images from Docker users and hosts them as online repositories. 

## Run an Ubuntu container and a container Shell