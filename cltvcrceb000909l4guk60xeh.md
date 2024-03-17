---
title: "Streamlining Continuous Integration and Deployment with AWS, Jenkins, Docker, Git, and Terraform"
seoTitle: "Streamlining Continuous Integration"
datePublished: Sun Mar 17 2024 10:06:56 GMT+0000 (Coordinated Universal Time)
cuid: cltvcrceb000909l4guk60xeh
slug: streamlining-continuous-integration-and-deployment-with-aws-jenkins-docker-git-and-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710669459102/319862e8-1366-44bb-8695-66faa00ce9cc.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1710669768703/6a513019-b27f-43be-85e6-fb2e4c1daabe.jpeg
tags: docker, aws, continuous-integration, git, cloud-computing, terraform, jenkins, dockerfile, learning-journey, terraform-cloud, docker-network, learn-in-public, jenkins-pipeline

---

**In this blog we are going to automate installation of Jenkins and launching ec2-instance with the help of terraform**

## **Introduction**

In today's fast-paced software development environment, streamlining CI/CD pipelines is crucial for delivering high-quality software efficiently. This blog post will explore how to leverage AWS, Jenkins, Docker, Git, and Terraform to achieve this goal.

![DevSecOps & DevOps with Jenkins, Kubernetes, Terraform & AWS | Udemy](https://img-c.udemycdn.com/course/750x422/4849818_493a_2.jpg align="center")

## **Setting Up Jenkins on AWS**

**Launching an EC2 Instance:** To launch an EC2 instance on AWS, follow these steps using the AWS Management Console:

1. Log in to the AWS Management Console.
    
2. Navigate to the EC2 dashboard.
    
3. Click on "Launch Instance" and select the desired AMI, instance type, and configure security groups.
    
4. Follow the prompts to create the instance.
    

## **Installing Jenkins**

Once the EC2 instance is up and running, SSH into the instance and install Jenkins using the following commands:

```bash
sudo apt update
sudo apt install default-jre -y
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
```

After installation, start the Jenkins service:

```bash
sudo systemctl start jenkins
```

Access Jenkins through your browser using the instance's public IP address and port 8080.

## **Configuring Jenkins for Continuous Integration**

1. Install necessary Jenkins plugins like Git plugin, Pipeline plugin, etc.
    
2. Create a new Jenkins job and configure it to pull the Medium app's code from the Git repository.
    
3. Set up build triggers to automatically start a build whenever new changes are pushed to the repository.
    

## **Building a Medium App on React**

**Setting Up the Medium App:** Install React and create a new React app using the following commands:

```bash
npx create-react-app medium-app
cd medium-app
```

This will set up a basic React app structure.

## **Implementing CI with Git and Jenkins**

1. Connect your Git repository to Jenkins by providing the repository URL and necessary credentials.
    
2. Configure the Jenkins job to execute build commands for the React app, such as installing dependencies and running tests.
    

### **Deploying with Docker and Terraform**

**Containerizing the Medium App with Docker:** Create a Dockerfile in the root of the React app directory with the following content:

```Dockerfile
FROM node:alpine
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
CMD ["npm", "start"]
```

Build and tag the Docker image:

```bash
docker build -t medium-app .
```

**Automating Infrastructure with Terraform:** Install Terraform and create a [`main.tf`](http://main.tf) file with the following content to provision AWS resources:

```powershell
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "jenkins" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
 
}
```

Execute `terraform init`, `terraform plan`, and `terraform apply` to provision the resources.

### **Deploying the Medium App with Terraform**

Integrate Terraform with Jenkins by executing Terraform commands as part of the Jenkins job. Use Terraform scripts to deploy the Dockerized Medium app onto the AWS infrastructure provisioned earlier.

## **Conclusion**

By leveraging AWS, Jenkins, Docker, Git, and Terraform, developers can create efficient CI/CD pipelines for their projects. Continuous integration, automated deployments, and infrastructure as code methodologies streamline the software development lifecycle, resulting in faster delivery of high-quality software. Explore further optimizations and tools to enhance your CI/CD pipelines and stay ahead in the dynamic world of software development.

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)