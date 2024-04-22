---
title: "Day_9 Simplified Guide to AWS EKS Deployment with Terraform"
seoTitle: "Day_9 Simplified Guide to AWS EKS Deployment with Terraform"
datePublished: Mon Apr 22 2024 14:38:48 GMT+0000 (Coordinated Universal Time)
cuid: clvb2bn1q000q09mdbueyh3nz
slug: day9-simplified-guide-to-aws-eks-deployment-with-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713796623406/daa257a3-7720-4469-9ee6-63f9c5275786.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1713796648267/d24ad149-c7c7-45b5-95ec-5972e86b6cea.png
tags: aws, kubernetes, terraform, eks, aws-certified-solutions-architect-associate, terraform-cloud, eks-cluster, eksctl, terraweekchallenge, eks-project

---

## Introduction

Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service provided by Amazon Web Services (AWS) that makes it easy to deploy, manage, and scale containerized applications using Kubernetes. In this blog post, we'll walk through the process of setting up an EKS cluster on AWS using Terraform, a popular infrastructure as code tool.

## Why Terraform?

Terraform enables you to define and provision infrastructure using a declarative configuration language. It's particularly well-suited for managing cloud resources like those on AWS, as it allows you to codify your infrastructure requirements and manage them efficiently.

## Prerequisites:

1. An AWS account.
    
2. Terraform installed on your local machine.
    
3. Basic familiarity with Kubernetes concepts.
    

## Step to create EKS

Certainly! Let's break down the code provided in the blog post and explain each line:

### Step 1: Set up IAM Roles and Policies

```powershell
provider "aws" {
  region = "us-west-2" # Change to your desired region
}
```

* This line configures the AWS provider for Terraform and specifies the AWS region where the resources will be provisioned.
    

```powershell
resource "aws_iam_role" "eks_service_role" {
  name               = "eks-service-role"
  assume_role_policy = data.aws_iam_policy_document.eks_service.json
}
```

* This block defines an IAM role named "eks-service-role" that will be assumed by the EKS service. The `assume_role_policy` attribute specifies the trust policy for the role.
    

```powershell
data "aws_iam_policy_document" "eks_service" {
  statement {
    actions = ["sts:AssumeRole"]

    principals {
      type        = "Service"
      identifiers = ["eks.amazonaws.com"]
    }
  }
}
```

* This block defines a data source that represents an IAM policy document. It specifies the permissions that the EKS service will have by allowing it to assume the IAM role.
    

```powershell
resource "aws_iam_policy" "eks_policy" {
  name        = "eks-policy"
  description = "Allows necessary permissions for EKS cluster"
  policy      = data.aws_iam_policy_document.eks_policy.json
}
```

* This block creates an IAM policy named "eks-policy" that defines the permissions required for the EKS cluster. The policy document is sourced from the previously defined data source.
    

```powershell
data "aws_iam_policy_document" "eks_policy" {
  statement {
    actions   = ["eks:*"]
    resources = ["*"]
  }
}
```

* This block defines another IAM policy document that grants permissions to perform any action (`eks:*`) on any resource (`*`), effectively granting full permissions for EKS operations.
    

```powershell
resource "aws_iam_role_policy_attachment" "eks_policy_attachment" {
  role       = aws_iam_role.eks_service_role.name
  policy_arn = aws_iam_policy.eks_policy.arn
}
```

* This block attaches the IAM policy created earlier to the IAM role, allowing the EKS service to assume the role and perform operations defined in the policy.
    

### Step 2: Create the EKS Cluster Configuration

```powershell
module "eks_cluster" {
  source            = "terraform-aws-modules/eks/aws"
  cluster_name      = "my-eks-cluster"
  cluster_version   = "1.20"
  subnets           = ["subnet-12345678", "subnet-87654321"] # Your subnets
  vpc_id            = "vpc-0123456789abcdef0" # Your VPC ID
  node_group_name   = "my-node-group"
  node_group_desired_capacity = 2
  node_group_min_size         = 1
  node_group_max_size         = 3
  node_group_instance_type    = "t3.medium" # Change to your desired instance type
  node_group_volume_size      = 20
  node_group_key_name         = "my-key-pair"
  node_group_security_groups  = ["sg-0123456789abcdef0"] # Your security group
  node_group_subnet_ids       = ["subnet-12345678", "subnet-87654321"] # Your subnets
}
```

* This block defines a Terraform module that provisions an EKS cluster. It specifies various configuration parameters such as cluster name, version, subnets, VPC ID, node group details, instance type, security groups, and subnets.
    

### Step 3: Deploy the EKS Cluster

```bash
terraform init
terraform apply
```

* These commands initialize Terraform and apply the configuration, provisioning the resources defined in the Terraform files.
    

### Step 4: Configure kubectl

```bash
aws eks --region <region> update-kubeconfig --name <cluster-name>
```

* This command configures `kubectl` to communicate with the newly created EKS cluster by updating the kubeconfig file with the necessary authentication and endpoint information.
    

### Step 5: Verify Cluster Status

```bash
kubectl get nodes
```

* This command verifies the status of the EKS cluster by listing the nodes (compute instances) that are part of the cluster. It confirms whether the cluster is up and running successfully.
    

## Conclusion

In this guide, we've demonstrated how to deploy an AWS EKS cluster using Terraform. By following the steps outlined, you can efficiently set up a managed Kubernetes environment on AWS. Leveraging Terraform's infrastructure as code approach, we defined our cluster configuration and deployed it seamlessly. With AWS EKS and Terraform, you can streamline cluster management, enabling rapid deployment and scaling of containerized applications. Embrace this simple, scalable solution for your cloud-native projects and unlock the power of Kubernetes on AWS.

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)
    
* GitHub :- [https://github.com/Ingole712521](https://github.com/Ingole712521)