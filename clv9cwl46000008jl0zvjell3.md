---
title: "Day_8 : Deploying a Docker Environment on Google Cloud Platform with Terraform"
datePublished: Sun Apr 21 2024 09:59:29 GMT+0000 (Coordinated Universal Time)
cuid: clv9cwl46000008jl0zvjell3
slug: day8-deploying-a-docker-environment-on-google-cloud-platform-with-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713691537232/5290d35e-8378-4516-b879-c50320c00fe9.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1713693562990/d27c16d5-4746-49ef-985e-cc9c89570f0e.png
tags: docker, terraform, dockerfile, docker-images, learning-journey, learning-in-public, terraform-state, terraform-cloud, learn-in-public, terraweekchallenge

---

## Introduction

In today’s rapidly evolving technological landscape, the ability to quickly deploy and manage infrastructure is crucial. Infrastructure as Code (IaC) tools like Terraform allow developers and system administrators to automate the provisioning and configuration of cloud resources, enabling more efficient and consistent deployments. In this blog post, we’ll explore how to use Terraform to deploy a Docker environment on Google Cloud Platform (GCP).

Code file :- [https://github.com/Ingole712521/Terraform\_Expert/tree/main/Day\_8\_GCP](https://github.com/Ingole712521/Terraform_Expert/tree/main/Day_8_GCP)

---

## Explanation

Google Cloud Platform (GCP) offers a plethora of services and features for building, deploying, and managing applications in the cloud. Docker, on the other hand, is a popular containerization platform that enables developers to package their applications and dependencies into lightweight, portable containers.

In this tutorial, we will leverage Terraform, a widely-used IaC tool, to automate the deployment of a virtual machine (VM) instance on GCP and install Docker on it. Let's break down the Terraform configuration file step by step:

```powershell
data "google_compute_image" "demo" {
  family  = "ubuntu-2204-lts"
  project = "ubuntu-os-cloud"
}
```

Here, we're defining a data source to retrieve the Ubuntu 22.04 LTS image from the Google Cloud Platform project "ubuntu-os-cloud".

```powershell
locals {
  region            = var.region
  availability_zone = var.zone
}
```

This block defines local variables for the region and availability zone based on input variables.

```powershell
resource "tls_private_key" "ssh" {
  algorithm = "RSA"
}
```

This resource generates an RSA private key that will be used for SSH access to the VM instance.

```powershell
resource "google_compute_instance" "demo" {
  // Configuration for the Google Compute Engine VM instance
}
```

This block defines a Google Compute Engine instance resource named "demo".

```powershell
metadata_startup_script = <<EOT
  // Shell script to be executed on instance startup
EOT
```

Here, we define a startup script that will be executed when the VM instance starts. This script updates the package list and installs Docker CE.

```powershell
resource "google_compute_firewall" "demo-ssh-ipv4" {
  // Configuration for the firewall rule allowing SSH traffic
}
```

This block defines a firewall rule that allows SSH traffic to the VM instance.

```powershell
resource "local_file" "local_ssh_key" {
  // Configuration for saving the generated private key to a local file
}
```

This block saves the generated private key to a local file on the machine running Terraform.

```powershell
output "instance_ip" {
  // Output variable for the instance's public IP address
}
```

This block defines an output variable for the public IP address of the VM instance.

```powershell
output "instance_ssh_key" {
  // Output variable for the path to the generated SSH private key file
}
```

This block defines an output variable for the path to the generated SSH private key file.

---

## Demo

Main.tf file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713690207917/fcc43f42-7604-40a1-8285-3caee1767dce.png align="center")

varible.tf file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713690234062/e8cab75f-902e-4fdf-b07d-afd3f68dd004.png align="center")

provider.tf file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713690249547/572506f1-690a-4feb-bd45-208a91748502.png align="center")

Final Result :-

1. ssh\_key creation
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713690709703/c119103b-6016-4486-a574-ef127a64f488.png align="center")

2. Output of main.tf file
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713690768003/7e10c525-c7be-4a3a-af40-4f392f70b553.png align="center")

3. Output from GCP
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713690819913/8a60b684-832e-4da4-99e8-625468b6c984.png align="center")
    
4. Deleting
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713690879648/26ba6b73-eea2-43be-acfd-75fb3d4c25fc.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713690961043/0a8bbbb2-921d-4150-a000-fb4ed18474f0.png align="center")
    

---

## Video

%[https://youtu.be/ViDbRiR3ajI?si=IEzAmkjTDzlUNg0K] 

## Conclusion

Terraform simplifies the deployment of Docker environments on Google Cloud Platform (GCP), offering efficiency and consistency. This tutorial has walked through the Terraform configuration, showcasing how it orchestrates the provisioning of GCP resources. Additionally, a video demonstration accompanies this guide, providing a visual walkthrough of the deployment process. By leveraging Terraform and GCP, developers can automate infrastructure management, focusing more on building and deploying applications. Happy deploying!

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)
    
* GitHub :- [https://github.com/Ingole712521](https://github.com/Ingole712521)