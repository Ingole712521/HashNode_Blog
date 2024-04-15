---
title: "Day-2  Terraform provisioner"
seoTitle: "Day-2 Terraform provisioner "
datePublished: Mon Apr 15 2024 08:50:58 GMT+0000 (Coordinated Universal Time)
cuid: clv0ptd4e000o08l26nrre21l
slug: day-2-terraform-provisioner
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713170890048/919f9031-6a15-40a2-84ee-7ae97ddb9d22.webp
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1713170946335/24658b85-192d-41c9-ac05-83096ba878b8.webp
tags: aws, terraform, learning-in-public, terraform-state, terraform-cloud, cicd-complete-proccess, cicd-jenkins-goal, provisioner

---

In Day-2 of Learning terraform from zero to expert we are going to see how the provisioner work and some practical implementation in it.

Let's break down the Terraform configuration provided and explain each part step by step

---

### Setting up the AWS Provider

```powershell
provider "aws" {
  region = "ap-south-1" # Update with your desired AWS region
}
```

Here, we specify the AWS region where we want to deploy our resources. In this example, we've chosen the "ap-south-1" region, but you can replace it with your preferred region.

### Defining the EC2 Instance Resource

```powershell
resource "aws_instance" "clear" {
  ami           = "ami-09298640a92b2d12c" # Update with your desired AMI ID
  instance_type = "t2.micro"
  key_name      = "Project_Mario_game"

  vpc_security_group_ids = [aws_security_group.allow_all.id]
  subnet_id              = aws_subnet.default.id

  tags = {
    Name = "example-instance"
  }
}
```

Here, we define an EC2 instance resource named "clear." We specify the AMI ID, instance type, and key pair name. Additionally, we reference the security group and subnet to associate with the instance.

### Configuring Provisioners

```powershell
provisioner "file" {
  source      = "./script.sh"
  destination = "/tmp/script.sh"
}

provisioner "remote-exec" {
  inline = [
    "chmod +x /tmp/script.sh",
    "/tmp/script.sh"
  ]
}
```

We use provisioners to configure the instance after it's launched. The first provisioner copies a local script ([`script.sh`](http://script.sh)) to the instance. The second provisioner executes the script inside the instance.

### Defining Security Group Rules

```powershell
resource "aws_security_group" "allow_all" {
  name        = "allow-all"
  description = "Allow all traffic"

  vpc_id = aws_default_vpc.default.id

  ingress {
    from_port   = 0
    to_port     = 65535
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

This code defines a security group named "allow-all" that allows all inbound and outbound traffic. We set the ingress rules to allow TCP traffic on all ports and the egress rules to allow all outbound traffic.

### Creating a Default VPC and Subnet

```powershell
resource "aws_default_vpc" "default" {}

resource "aws_subnet" "default" {
  vpc_id = aws_default_vpc.default.id
}
```

These resources create a default VPC and subnet. We associate the default VPC with the security group and instance.

---

### Running the terraform file

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713169996586/e2de2e4b-f88b-470e-ac64-d73f6804002f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713170021318/3d25a8ea-49b2-4d5e-b2b9-dd3cbd369c70.png align="center")

---

### Final\_result

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713169937531/77ddf49d-9c50-4ea5-8b94-86f9cb809532.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713169873237/1ae96f3c-c1d9-4697-9ec2-0cd0cd6e95f5.png align="center")

By following these steps and executing the Terraform configuration, you'll be able to provision an EC2 instance on AWS with the specified settings and configurations. This approach enables you to automate the deployment of infrastructure and streamline your development workflow.

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)