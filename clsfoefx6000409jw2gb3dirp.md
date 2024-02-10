---
title: "Cheat Sheet of Docker and Kubernetes"
seoTitle: "Cheat Sheet of Docker and Kubernetes"
datePublished: Sat Feb 10 2024 06:08:48 GMT+0000 (Coordinated Universal Time)
cuid: clsfoefx6000409jw2gb3dirp
slug: cheat-sheet-of-docker-and-kubernetes
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1707545265977/95ae183c-29c0-4bc1-b2cd-f00d804335b7.png
tags: docker, kubernetes, hashnode, cheatsheet, public-speaking, docker-compose, learning-journey, kubernetes-container, docker-network, kubernetes-persistent-volumes

---

## Mastering Kubernetes

![Kubernetes wallpapers](https://static.learnk8s.io/ce26d407ce85d5c042eb6ed6079b27d7.png align="left")

Kubernetes is a powerful container orchestration platform that allows you to deploy, manage, and scale containerized applications with ease. However, mastering Kubernetes requires familiarity with its command-line interface (CLI) tools. In this guide, we'll explore essential Kubernetes commands and their usage.

### Basic Commands

* **Create Resource (**`kubectl create -f <yaml-file>`): This command is used to create Kubernetes resources defined in a YAML file. It can be used to create Pods, Deployments, Services, and more.
    
* **Get Resource(s) (**`kubectl get <resource>` or `kubectl get <resource> <name>`): Use this command to retrieve information about Kubernetes resources. You can query resources such as Pods, Deployments, Services, etc., either by type or by specific name.
    
* **Describe Resource (**`kubectl describe <resource> <name>`): Provides detailed information about a specific Kubernetes resource, including its current state, events, and configurations.
    
* **Delete Resource (**`kubectl delete <resource> <name>`): Deletes a Kubernetes resource. Be cautious when using this command, as it permanently removes the specified resource.
    
* **Apply Changes (**`kubectl apply -f <yaml-file>`): Applies changes to Kubernetes resources defined in a YAML file. It updates existing resources or creates new ones if they don't exist.
    
* **Edit Resource (**`kubectl edit <resource> <name>`): Opens the specified Kubernetes resource in the default editor, allowing you to make changes interactively.
    
* **Get Logs (**`kubectl logs <pod-name>`): Retrieves the logs of a specific Pod, helping you troubleshoot issues and monitor application behavior.
    
* **Execute Command in Pod (**`kubectl exec -it <pod-name> -- <command>`): Allows you to run a command inside a running Pod interactively. Useful for debugging or performing administrative tasks within containers.
    

### Resource Types

* **Pod (**`kubectl run <pod-name> --image=<image>`): Creates a new Pod with the specified container image.
    
* **Deployment (**`kubectl create deployment <deployment-name> --image=<image>`): Defines a Deployment, which manages a set of replicated Pods running the same container image.
    
* **Service (**`kubectl expose <pod-name> --type=NodePort --port=<port>`): Exposes a Pod or a set of Pods to the outside world, typically through a NodePort or LoadBalancer.
    
* **Namespace (**`kubectl create namespace <namespace-name>`): Creates a new namespace, which provides a way to logically isolate resources within a Kubernetes cluster.
    
* **ConfigMap (**`kubectl create configmap <configmap-name> --from-file=<path-to-file>`): Creates a ConfigMap, which stores configuration data as key-value pairs.
    
* **Secret (**`kubectl create secret generic <secret-name> --from-literal=<key>=<value>`): Creates a Secret, which securely stores sensitive information such as passwords, API tokens, etc.
    
* **PersistentVolume (**`kubectl create -f <persistent-volume.yaml>`): Defines a PersistentVolume, which is a piece of storage in the cluster that has been provisioned by an administrator.
    
* **PersistentVolumeClaim (**`kubectl create -f <persistent-volume-claim.yaml>`): Requests storage resources from a PersistentVolume.
    
* **Ingress (**`kubectl create -f <ingress.yaml>`): Configures access to HTTP and HTTPS services from outside the Kubernetes cluster.
    
* **ServiceAccount (**`kubectl create serviceaccount <account-name>`): Creates a ServiceAccount, which provides an identity for Pods that run in the cluster.
    
* **Role (**`kubectl create role <role-name> --verb=<verb> --resource=<resource>`): Defines a Role, which specifies a set of permissions within a namespace.
    
* **RoleBinding (**`kubectl create rolebinding <binding-name> --role=<role-name> --serviceaccount=<namespace>:<account-name>`): Binds a Role to a ServiceAccount, granting permissions to the ServiceAccount.
    

### Configuration

* **kubectl Configuration (**`~/.kube/config`): The configuration file for the Kubernetes CLI, which stores cluster information, authentication details, and context settings.
    
* **kubectl Contexts (**`kubectl config get-contexts`): Lists available contexts, which are combinations of clusters, users, and namespaces.
    
* **Switch Context (**`kubectl config use-context <context-name>`): Changes the current context, allowing you to switch between different Kubernetes clusters.
    

### Troubleshooting

* **Check Cluster Info (**`kubectl cluster-info`): Displays information about the Kubernetes cluster, including the master and services running in the cluster.
    
* **Check Node(s) (**`kubectl get nodes`): Retrieves a list of nodes in the Kubernetes cluster along with their status and resource usage.
    
* **Check Pod(s) (**`kubectl get pods`): Lists all Pods in the cluster, along with their current status and other relevant information.
    
* **Check Events (**`kubectl get events`): Shows recent events in the cluster, such as Pod creations, deletions, errors, etc.
    
* **Check API Resources (**`kubectl api-resources`): Lists all available API resources supported by the Kubernetes API server.
    
* **Check Component Status (**`kubectl get componentstatuses`): Checks the health status of various Kubernetes components running in the cluster.
    

### Advanced Operations

* **Rollout Status (**`kubectl rollout status <resource> <name>`): Checks the status of a rollout, such as a Deployment or a DaemonSet.
    
* **Rollout History (**`kubectl rollout history <resource> <name>`): Displays the revision history of a rollout, allowing you to track changes over time.
    
* **Rollout Undo (**`kubectl rollout undo <resource> <name>`): Reverts a rollout to a previous revision, useful for rolling back to a stable state in case of issues.
    
* **Scale Deployment (**`kubectl scale --replicas=<count> deployment/<deployment-name>`): Scales the number of replicas in a Deployment to the specified count.
    
* **Autoscale Deployment (**`kubectl autoscale deployment <deployment-name> --min=<min-pods> --max=<max-pods> --cpu-percent=<cpu-threshold>`): Configures autoscaling for a Deployment based on CPU usage.
    
* **Node Drain (**`kubectl drain <node-name> --ignore-daemonsets`): Prepares a node for maintenance by evicting all Pods (except DaemonSets) scheduled to run on it.
    

### Custom Resources

* **Custom Resource Definition (**`kubectl create -f <crd.yaml>`): Defines a new custom resource type, extending the Kubernetes API.
    
* **Custom Resource (**`kubectl create -f <custom-resource.yaml>`): Creates an instance of a custom resource, allowing you to store and manage custom data types within the cluster.
    

### Helm Commands

* **Install Chart (**`helm install <release-name> <chart>`): Installs a Helm chart, which is a package containing Kubernetes resources, templates, and configuration files.
    
* **Upgrade Chart (**`helm upgrade <release-name> <chart>`): Upgrades an existing Helm release to a new version, applying changes to the Kubernetes resources defined in the chart.
    
* **List Releases (**`helm list`): Lists all releases managed by Helm, along with their status, version, and other details.
    
* Delete Release (\`helm delete \`): Deletes a Helm release, removing all associated Kubernetes resources from the cluster.
    

---

## **Mastering Docker**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707461497281/db5cdf81-622b-4717-ac5b-402690b52ab5.webp align="center")

Docker has revolutionized the way we build, ship, and run applications, enabling developers to package applications and their dependencies into containers. In this guide, we'll explore essential Docker commands and concepts to help you become proficient in container management.

### **1\. Docker Basics:**

#### Pull an Image

The `docker pull <image-name>` command fetches a Docker image from a registry like Docker Hub or a private registry. This is the first step before running containers based on that image.

#### Run a Container:

With `docker run <image-name>`, you instantiate a Docker container based on a specific image. This command creates a new instance of the image and starts the container.

#### List Running Containers:

To see which containers are currently running, you can use `docker ps`. This command provides a list of running containers along with their IDs, status, and other details.

#### List All Containers (including stopped):

To view all containers, including those that have stopped, you can add the `-a` flag: `docker ps -a`. This gives you a comprehensive overview of all containers on your system.

#### Stop a Container:

To halt a running container, you use `docker stop <container-id>`. This command sends a SIGTERM signal to the container, giving it a chance to gracefully shut down.

#### Remove a Container:

Once a container has stopped, you can remove it from your system using `docker rm <container-id>`. This permanently deletes the container, freeing up resources.

#### Remove an Image:

To delete an image from your local registry, you can use `docker rmi <image-id>`. This command removes the specified image, freeing up disk space.

### **2\. Image Management**

#### List Local Images:

`docker images` lists all Docker images stored locally on your system. This includes both images you've pulled from registries and those you've built yourself.

#### Remove an Image:

Similar to removing containers, you can delete images with `docker rmi <image-id>`. This command removes the specified image from your local registry.

#### Build an Image:

The `docker build -t <image-name> .` command builds a Docker image from a Dockerfile located in the current directory (`.`). You can tag the image with a name using the `-t` flag.

#### Tag an Image:

To tag an image with a specific name and version, you use `docker tag <image-id> <new-image-name>:<tag>`. This is useful for versioning and identifying images.

### **3\. Container Operations**

#### Attach to a Running Container:

With `docker attach <container-id>`, you can attach your terminal to a running container's standard input, output, and error streams. This allows you to interact with processes inside the container.

#### Execute a Command in a Running Container:

The `docker exec -it <container-id> <command>` command lets you run a specific command inside a running container. The `-it` flags allocate a pseudo-TTY and keep STDIN open even if not attached.

#### Inspect a Container:

`docker inspect <container-id>` provides detailed information about a container, including its configuration, networking, and mounted volumes.

#### View Logs of a Container:

To view the logs generated by a container, you can use `docker logs <container-id>`. This is helpful for troubleshooting and monitoring containerized applications.

### **4\. Docker Networks**

#### List Networks:

Docker supports different types of networks for containers. You can list the available networks with `docker network ls`.

#### Create a Network:

To create a custom network for your containers, you can use `docker network create <network-name>`. This allows containers to communicate with each other using the network name.

#### Connect a Container to a Network:

After creating a network, you can connect a container to it using `docker network connect <network-name> <container-id>`. This enables communication between containers on the same network.

#### Disconnect a Container from a Network:

If needed, you can disconnect a container from a network with `docker network disconnect <network-name> <container-id>`. This removes the container from the specified network.

### **5\. Docker Volumes**

#### List Volumes:

Docker volumes provide persistent storage for containers. You can list existing volumes with `docker volume ls`.

#### Create a Volume:

To create a new volume, you can use `docker volume create <volume-name>`. This allocates storage that can be attached to containers.

#### Inspect a Volume:

With `docker volume inspect <volume-name>`, you can view detailed information about a specific volume, including its mountpoint and configuration.

#### Mount a Volume to a Container:

To mount a volume to a container, you use the `-v` flag when running the container: `docker run -v <volume-name>:<container-mount-path> <image-name>`. This allows the container to persist data beyond its lifecycle.

### **6\. Docker Compose**

#### Run Services defined in a Compose file:

Docker Compose simplifies the management of multi-container applications. You can start services defined in a Compose file with `docker-compose up`.

#### Stop Services defined in a Compose file:

To stop and remove containers defined in a Compose file, you use `docker-compose down`. This stops and removes containers, networks, and volumes.

#### Build and run services defined in a Compose file:

If changes have been made to your services or Dockerfiles, you can rebuild and run them with `docker-compose up --build`.

#### View Compose logs:

To view the logs of services defined in a Compose file, you can use `docker-compose logs`. This displays the logs of all services or a specific service.

### **7\. Dockerfile Directives**

#### FROM:

The `FROM` directive in a Dockerfile specifies the base image to use for subsequent instructions. It's the starting point for building your Docker image.

#### COPY:

`COPY` copies files or directories from the host into the image at build time. This is useful for adding application code, configuration files, or other dependencies.

#### RUN:

The `RUN` directive executes commands within the image during the build process. You can use it to install dependencies, set up the environment, or run build scripts.

#### CMD:

`CMD` specifies the default command to run when the container starts. This can be overridden at runtime, but it defines the initial behavior of the container.

#### EXPOSE:

The `EXPOSE` directive informs Docker that the container listens on specific network ports at runtime. It's a declaration, not a command to actually open ports.

#### WORKDIR:

`WORKDIR` sets the working directory for subsequent instructions in the Dockerfile. It's similar to `cd` in a shell and affects subsequent instructions.

#### ENV:

`ENV` sets environment variables in the container. This allows you to configure the container's environment and behavior.

#### ENTRYPOINT:

`ENTRYPOINT` configures the container to run as an executable. It specifies the command that will be executed when the container starts.

With this comprehensive guide, you're now equipped to efficiently manage both Kubernetes clusters and Docker environments using command-line interfaces. Whether you're deploying applications, troubleshooting issues, or performing advanced operations, the commands and concepts covered here will be invaluable in your containerization journey.

By incorporating these tools into your daily routine, you can streamline development and deployment workflows, maximizing the potential of containerization technology to drive innovation and efficiency in your projects.

Stay updated for further blog.

*Thank you for Reading:)*

*#Happy Reading!!*

***Any query and suggestion are always welcome -***[***Nehal Ingole***](http://www.linkedin.com/in/nehal-ingole)