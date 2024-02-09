---
title: "Day 2  Learn about  Microsoft  Azure"
seoTitle: "Day 2  Learn about  Microsoft  Azure"
datePublished: Thu Jan 25 2024 12:40:21 GMT+0000 (Coordinated Universal Time)
cuid: clrt7cclc000009l1be0y5puv
slug: day-2-learn-about-microsoft-azure
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706186333849/d6a7be0e-82e9-4b69-9584-23d3a56b3d9a.webp
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1706186382191/e5b31c7b-5914-4f82-adc2-7058ea06cc13.png
tags: cloud, azure, cloud-computing, devops

---

# What is Azure Resource Manager?

Azure Resource Manager is the service that manages and deploys Azure resources. It has a management layer that allows us to create, update, and delete Azure account resources. After deployment, we employ administration tools like access control, locks, and tags to secure and organize our resources.

## **Consistent management layer**

When you send a request through any of the Azure APIs, tools, or SDKs, Resource Manager receives the request. It authenticates and authorizes the request before forwarding it to the appropriate Azure service. Because all requests are handled through the same API, you see consistent results and capabilities in all the different tools.

The following image shows the role Azure Resource Manager plays in handling Azure requests.

![Diagram that shows the role of Azure Resource Manager in handling Azure requests.](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/media/overview/consistent-management-layer.png align="center")

## **What is a resource group?**

A resource group is a container that enables you to manage related resources for an Azure solution. By using the resource group, you can coordinate changes to the related resources. For example, you can deploy an update to the resource group and have confidence that the resources are updated in a coordinated operation. Or, when you're finished with the solution, you can delete the resource group and know that all of the resources are deleted.

There are some important factors to consider when defining your resource group:

* All the resources in your resource group should share the same lifecycle. You deploy, update, and delete them together. If one resource, such as a server, needs to exist on a different deployment cycle it should be in another resource group.
    
* Each resource can exist in only one resource group.
    
* You can add or remove a resource to a resource group at any time.
    
* You can move a resource from one resource group to another group.
    
* The resources in a resource group can be located in different regions than the resource group.
    
* When you create a resource group, you need to provide a location for that resource group.
    

## The benefits of using Resource Manager

There are several benefits of using the Azure Resource Manager, some of them are stated below:

* Use the declarative templet to manage the infrastructure.
    
* Rather than managing individual resources, deploy, manage, and monitor all of our solution's resources as a group.
    
* Define resource dependencies so that they are distributed in the correct order.
    
* Use tags to organize all of the resources in our subscription sensibly.
    
* View prices for a set of resources with the same tag to better understand our organization's billing.
    

## Understand scope

Management groups, subscriptions, resource groups, and resources are the four degrees of scope available in Azure. An example of these layers can be seen in the figure below.

![What is Azure Resource Manager](https://static.javatpoint.com/tutorial/microsoft-azure/images/what-is-azure-resource-manager2.png align="left")

At any of these scope levels, we can apply management settings. The setting's scope is determined by the level we choose. The settings from higher levels are passed down to lower levels.

Tenants, management groups, subscriptions, and resource groups can all receive templates.

## Resource groups

When defining our resource group, keep the following points in mind:

* Our resource group's resources should all have the same lifespan. We deploy, update, and remove them all at the same time. If a resource, such as a server, has to be deployed at a different time, it should be in a distinct resource group.
    
* One resource group can contain an isolate resource.
    
* We can add or remove a resource from a resource group at any point of time.
    
* We can move a resource group from one to another.
    
* A resource group's resources can be in distinct areas than the resource group itself.
    
* We must have a good habit of giving the resource group a proper name and location while we are creation it. One might be thinking, "Why is it necessary for a resource group to have a physical location? And, if the resources can be in different places than the resource group, why does the location of the resource group matter?"  
    The metadata about the resources is stored in the resource group. When we give a resource group a location, we're telling it where to keep its metadata. We may need to verify that our data is stored in a specific location for compliance reasons.  
    Because the metadata is inaccessible when the resource group's area is momentarily unavailable, we can't change resources in the resource group.
    
* A resource can be linked to others in the same resource group. When two resources are related but not in the same lifetime, this is a common circumstance.
    
* When we delete a resource group, it also deletes all of the resources within it. For more details on how Azure Resource Manager manages those deletions, go here.
    
* Every resource group can have up to 800 instances of resource type. The 800-instance restriction may not apply to all resource types.
    
* There are some resources that are not part of a resource group. The subscriber, management group, or tenant receives these resources.
    

Remember, the cloud is vast, and Azure is your key to unlocking its full potential. Join us tomorrow as we dive deeper into the azure depths, uncovering more treasures that await on our journey through the cloud. Until then, happy exploring!

*Thank you for Reading:)*

*#Happy Reading!!*

***Any query and suggestion are always welcome -***[***Nehal Ingole***](http://www.linkedin.com/in/nehal-ingole)***or***[***Twitter***](https://twitter.com/IngoleNehal)