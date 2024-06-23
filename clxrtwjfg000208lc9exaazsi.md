---
title: "Run own Desktop by using Docker image"
seoTitle: "Run own Desktop by using Docker images"
seoDescription: "Docker is an open-source platform that automates the deployment, scaling, and management of applications inside lightweight, portable containers"
datePublished: Sun Jun 23 2024 17:34:36 GMT+0000 (Coordinated Universal Time)
cuid: clxrtwjfg000208lc9exaazsi
slug: run-own-desktop-by-using-docker-image
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719163854937/498b9ecd-cdc5-4e75-9154-5b84dccd173a.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1719164050896/91fd0c50-d999-4d4f-8d58-2907e226fbbf.jpeg
tags: desktop, docker, aws, projects, docker-images, project-controls-engineer-resume

---

![Docker Image vs Container: Everything You Need to Know](https://stackify.com/wp-content/uploads/2019/05/Feature-Image-Blog-Post-Docker-Container-vs-Image-881x441-1.jpg align="left")

## Introduction to Docker

Docker is an open-source platform that automates the deployment, scaling, and management of applications inside lightweight, portable containers. Containers allow developers to package an application with all its dependencies and run it in any environment that supports Docker.

### Key Concepts

* **Container**: A lightweight, standalone, and executable package of software that includes everything needed to run an application: code, runtime, system tools, libraries, and settings.
    
* **Image**: A read-only template with instructions for creating a Docker container. Often, an image is based on another image, with some additional customization.
    
* **Dockerfile**: A script containing a series of instructions on how to build a Docker image.
    
* **Docker Hub**: A cloud-based repository where Docker users and partners create, test, store, and distribute container images.
    

### Advantages of Using Docker

1. **Portability**: Containers can run on any system that supports Docker, ensuring consistency across different environments.
    
2. **Isolation**: Applications and their dependencies are isolated from each other, improving security and stability.
    
3. **Efficiency**: Containers share the same OS kernel and are more lightweight than traditional virtual machines, using fewer resources.
    
4. **Scalability**: Docker enables easy scaling of applications by managing containers through orchestration tools like Kubernetes.
    

---

## Running Ubuntu on Docker

Running an Ubuntu container is a common use case to create a development environment or run specific applications within an isolated environment. Below is a step-by-step guide to setting up and running an Ubuntu container using Docker.

### Step-by-Step Guide

1. **Open your terminal**: Start your command-line interface.
    
2. **Pull the Ubuntu image from Docker Hub**: Run the following command to download the latest Ubuntu image.
    
    ```sh
    docker pull ubuntu
    ```
    
    This command fetches the latest Ubuntu image from Docker Hub.
    
3. **Verify the downloaded image**: List all the Docker images to verify that the Ubuntu image is downloaded.
    
    ```sh
    docker images
    ```
    
    You should see an entry for `ubuntu` in the list.
    
4. **Run an Ubuntu container**: Start a container using the downloaded Ubuntu image.
    
    ```sh
    docker run -it ubuntu
    ```
    
    The `-it` flags attach an interactive terminal session to the container.
    
5. **Explore the Ubuntu container**: Once the container is running, you will be inside the Ubuntu shell.
    
    ```sh
    root@container_id:/#
    ```
    
    You can now run any command you would run on a typical Ubuntu system.
    
6. **Exit the container**: To exit the container's shell, simply type:
    
    ```sh
    exit
    ```
    
    This will stop the container. If you want to leave the container running in the background, use `Ctrl+P` followed by `Ctrl+Q`.
    

---

### Managing Ubuntu Containers

* **List running containers**: To see all running containers, use:
    
    ```sh
    docker ps
    ```
    
* **List all containers**: To see all containers (running and stopped), use:
    
    ```sh
    docker ps -a
    ```
    
* **Start a stopped container**: Use the container ID or name to restart a stopped container.
    
    ```sh
    docker start container_id_or_name
    ```
    
* **Stop a running container**: To stop a running container, use:
    
    ```sh
    docker stop container_id_or_name
    ```
    
* **Remove a container**: To remove a stopped container, use:
    
    ```sh
    docker rm container_id_or_name
    ```
    
* **Remove an image**: To delete an image from your system, use:
    
    ```sh
    docker rmi image_id_or_name
    ```
    

---

### Advanced Usage

* **Dockerfile for Custom Ubuntu Image**: Create a `Dockerfile` to build a custom Ubuntu image with specific software and configurations.
    
    ```Dockerfile
    # Use the official Ubuntu base image
    FROM ubuntu:latest
    
    # Install desired packages
    RUN apt-get update && apt-get install -y \
        vim \
        curl \
        git \
        && rm -rf /var/lib/apt/lists/*
    
    # Set the working directory
    WORKDIR /root
    
    # Copy files from the host to the container
    COPY . /root
    
    # Define the command to run when the container starts
    CMD ["bash"]
    ```
    

---

## Project

You can run your own Ubuntu OS using a Docker image, which provides an isolated environment to work with Ubuntu without the need for a full virtual machine. This approach is lightweight, efficient, and ideal for development, testing, and learning purposes. With Docker, you can easily pull an official Ubuntu image, start a container, and have a fully functional Ubuntu system at your disposal.

You can download all the images from this docker repo :- [https://hub.docker.com/r/kasmweb/chrome](https://hub.docker.com/r/kasmweb/chrome)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719073538911/75a8dcae-da8b-4e82-9a39-c5cdbc7fa57e.png align="center")

Pull the docker image

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719073481246/2c674e73-0d0d-497b-a343-0ca634133ba5.png align="center")

Check whether the image is download or bot

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719073503044/ad373f96-2528-4349-9810-112dcb256a5b.png align="center")

Run docker image by providing the password and port number

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719073518476/c27de7ed-3c07-4fce-a897-a5a7078918b7.png align="center")

### Final Result

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719073552700/5e8a729b-0ac5-4ded-bf74-eb3ba938fc63.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719073670357/39976a91-d923-4a9c-97a8-fbd10a425139.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719073656436/0294fddb-3fea-437f-aafb-fe546234af2a.png align="center")

---

## Conclusion

Using this setup, you can run your own desktop environment, providing a flexible and powerful solution for accessing a complete Ubuntu OS. This method leverages Docker's efficiency and ease of use, enabling you to quickly set up and manage your desktop environment without the overhead of traditional virtualization methods.

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)
    
* GitHub :- [https://github.com/Ingole712521](https://github.com/Ingole712521)