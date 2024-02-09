---
title: "Mario Game in Docker"
seoTitle: "Mario Game in Docker"
seoDescription: "In this project we are going to look in docker how to install and run a Mario game in it"
datePublished: Fri Dec 08 2023 09:45:50 GMT+0000 (Coordinated Universal Time)
cuid: clpwfz0pl000608l80jwehtag
slug: mario-game-in-docker
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1702028920375/f0c695ba-b353-4199-a939-24ef8082f64a.webp
tags: docker, aws, vscode-cjevho8kk00bo1ss2lmqqjr51, instance, super-mario

---

In this project we are going to look in docker how to install and run a Mario game in it. But at the first we are going to look what is docker ??

What is Docker ??

Docker is an open platform for developing, shipping, and running applications. It allows you to package your application and its dependencies into a standardized unit called a container. This container can then be deployed to any environment, whether it's a local development machine, a staging server, or a production environment.

![Image of Docker logo](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQyi96VasEDgB0zTIIAj-Ukw9ZqWYLZO9KdlzUS7nr1VUKq9fjqasWWK7L44hrV align="center")

**Benefits of using Docker:**

* **Portability:** Docker containers are portable and can run on any system that has the Docker Engine installed. This makes it easy to share and deploy your applications across different environments.
    
* **Isolation:** Docker containers are isolated from the host system and each other. This means that a problem in one container won't affect other containers or the host system.
    
* **Reproducibility:** Docker containers are built from Docker images, which are static and immutable. This means that you can always recreate the same environment, no matter where you are or what system you're using.
    
* **Scalability:** Docker containers are lightweight and can be started and stopped quickly. This makes it easy to scale your applications up or down.
    

**Components of Docker:**

* **Docker Engine:** The Docker Engine is the software that builds, runs, and manages Docker containers. It is available for Windows, macOS, and Linux.
    
* **Docker Hub:** Docker Hub is a public registry where you can find and share Docker images. There are over 10 million images available on Docker Hub, which includes images for popular languages, frameworks, and applications.
    
* **Docker Compose:** Docker Compose is a tool that allows you to define and run multi-container applications. With Docker Compose, you can define all of the services that make up your application in a single YAML file.
    

---

Let's see demo

At the first create a AWS ec2-instance and launch it

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702027428627/58315754-ccba-49b4-8006-94aaa47ebc40.png align="center")

You can see we successfully created a ec2-instance , copy public IP address of instance in IDE or any SSH tools. (I my using VScode for launching ec2-instance).

At the first install docker by using

```yaml
yum install docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702027597470/a51bda33-1232-4401-9f6a-6ee83b88a077.png align="center")

Run the docker in instance by using

```yaml
systemctl start docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702027806698/7320bb7b-97c2-4e96-896c-05766bb510b8.png align="center")

Check docker is running or not by using

```yaml
systemctl status docker
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702027849479/e56ff188-8238-446d-b826-45d1aab21323.png align="center")

Pull the docker image from docker hub

```yaml
docker pull nehal71/mario:latest
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702027880461/4e82fb13-0299-4af3-9fd4-a95e1da23644.png align="center")

we completed our work just we need to run image in our instance by using

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702027980350/a5eb0dd3-12de-403e-8894-c8f732c1df94.png align="center")

just copy IP address of Instance and paste it in browser!!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702028053467/59d64eba-a9a2-4906-9e56-8b4ab443dfe6.png align="center")

%[https://youtu.be/xduKG-PX9Rk] 

In this project the docker image is taken from profile

[kaminskypavel/mario](https://hub.docker.com/r/kaminskypavel/mario)

*That's all for this blog and stay tuned for more* ***amazing project*** *and more such tech.*

*Thank you for Reading:)*

*#Happy Reading!!*

***Any query and suggestion are always welcome -*** [***Nehal Ingole***](http://www.linkedin.com/in/nehal-ingole)