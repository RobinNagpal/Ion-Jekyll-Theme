---
layout: post
title:  "Understanding Containers and Docker"
date:   2015-09-15 14:37:44
categories: DevOps
---

Containers provide a lightweight and high-speed alternative to Virtual Machines. Containers run inside a host operating system and provide very convenient way of application process and network isolation.  A virtual machine runs its own kernel and operating system, whereas container shares its kernel with the host operating system. Even though there can be multiple containers running on the host machine, each of these containers containers is completely isolated from one another. 

Using docker, when we start a new container, it create a set of namespaces and control groups for that container

### Namespace 
A namespace wraps a global system resource in an abstraction that makes it appear to the processes within the namespace that they have their own isolated instance of the global resource. Namespaces makes the container look like a separate little environment.

### Control Groups  
Cgroups allow allocation of resources—such as CPU time, system memory, network bandwidth, or combinations of these resources—among user-defined groups of tasks (processes) running on a system

So because of separate namespaces and control groups, containers get

* Process Isolation - Processes running within a container cannot see or affect the processes running in separate containers, or in the host machine
* Independent Network Stack - Each container has its own independent network stack. Container interact just like other internet interfaces i.e. via IP address and Port. They can ping other devices, send/receive UPD packets and establish TCP connections.  Container can interact to each other just like they interact with external devices. 
 
Container had been used in past by companies like Google for deploying their applications, but Docker provides many other components that makes it very easy to work with containers. Here is an official docker diagram that puts all of these components together
<img src="{{ site.baseurl }}/images/posts/2015/understanding-docker/architecture.svg" class="half-fit image">

### Container Image 
Images are readonly templates that are used for creating containers. Docker users Union File System for creating its images. UnionFS allows a file system to appear as writable, but without actually allowing writes to change the file system, also known as copy-on-write. Whenever a process attempts to make a change to the file, it first create a separate (private) copy of that file to prevent its changes from becoming visible to all the base image. 

Docker provides simple ways to create and save images. You can either create an image from scratch, but typically you will choose a base image like ubuntu, centos etc from docker hub and can then add your layers on top if it.  Docker hub has thousands of preconfigured images of applications like nginx, tomcat, mysql, redis etc. These images provide a nice starting point to developers as they can use these images and apply configurations and code specific to their application or project on it.

### Container 
Container are the runtime for applications that are based on images.  While creating a container from an Image, docker adds another file layer on top of the image. This layer holds the container generated metadata and files. You can commit and save your container as an image.  As explained earlier, container provides an isolated runtime for the application process. Here is the official diagram of docker container
<img src="{{ site.baseurl }}/images/posts/2015/understanding-docker/docker-filesystem.png" class="half-fit image">

### Docker Daemon 
Docker daemon is a persistent process that is responsible for managing containers. It is installed on a host machine and we typically interact with it using a docker client.

### Docker Client   
Whenever we install docker, it installs the demon + cline on our machine. Docker client is the "docker" binary, which accepts the commands from user and accordingly interacts with the daemon.

### Docker Registry
Docker registry is repository of docker images. Docker provided a Software-as-a-service "Docker Hub" for managing public and private images. You can download any of the public images and use them. You can also upload your own images to docker hub as public or private images. 

### Dockerfile
A configuration file with build instructions for Docker images. Dockerfiles provide a way to automate, reuse, and share build procedures.