---
title: "Simplifying Azure Load Balancing with Terraform"
seoTitle: "Simplifying Azure Load Balancing with Terraform"
datePublished: Mon Feb 12 2024 04:30:15 GMT+0000 (Coordinated Universal Time)
cuid: clsifrehe000008lhggtqfn99
slug: simplifying-azure-load-balancing-with-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707324249179/bc129e3d-2abd-4a53-8425-f306b1fba8a6.jpeg
tags: azure, devops, azure-devops, 2articles1week, learning-journey

---

## Introduction

Load balancing is a critical component of modern cloud infrastructures, enabling efficient distribution of incoming traffic across multiple instances to enhance reliability and scalability. In this blog post, we'll walk through the process of using Terraform to provision an Azure instance of type t2 medium and connect it to an Azure Load Balancer, ensuring seamless traffic distribution and high availability.

### Step 1: Define Azure Provider

```yaml
provider "azurerm" {
  features {}
}
```

Explanation: This block specifies the Azure provider for Terraform, enabling communication with the Azure APIs to manage Azure resources.

### Step 2: Create Azure Resource Group

```yaml
resource "azurerm_resource_group" "example_rg" {
  name     = "example-resource-group"
  location = "East US"
}
```

Explanation: This block defines an Azure resource group, a logical container for grouping Azure resources. Replace "example-resource-group" with the desired name and "East US" with the desired Azure region.

### Step 3: Define Virtual Network and Subnet

```yaml
resource "azurerm_virtual_network" "example_vnet" {
  name                = "example-vnet"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.example_rg.location
  resource_group_name = azurerm_resource_group.example_rg.name
}

resource "azurerm_subnet" "example_subnet" {
  name                 = "example-subnet"
  resource_group_name  = azurerm_resource_group.example_rg.name
  virtual_network_name = azurerm_virtual_network.example_vnet.name
  address_prefixes     = ["10.0.1.0/24"]
}
```

Explanation: These blocks define an Azure virtual network and subnet within the previously created resource group. Adjust the address space and subnet prefix as needed.

### Step 4: Provision Virtual Machine

```yaml
resource "azurerm_virtual_machine" "example_vm" {
  name                  = "example-vm"
  location              = azurerm_resource_group.example_rg.location
  resource_group_name   = azurerm_resource_group.example_rg.name
  network_interface_ids = [azurerm_network_interface.example_nic.id]
  vm_size               = "Standard_B2s"

  storage_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }

  os_profile {
    computer_name  = "hostname"
    admin_username = "adminuser"
    admin_password = "P@ssw0rd1234!"
  }

  os_profile_linux_config {
    disable_password_authentication = false
  }
}
```

Explanation: This block provisions an Azure virtual machine within the specified resource group and virtual network. Adjust the VM size, image, and authentication details according to your requirements.

### Step 5: Create Network Interface

```yaml
resource "azurerm_network_interface" "example_nic" {
  name                      = "example-nic"
  location                  = azurerm_resource_group.example_rg.location
  resource_group_name       = azurerm_resource_group.example_rg.name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.example_subnet.id
    private_ip_address_allocation = "Dynamic"
  }
}
```

Explanation: This block defines a network interface for the virtual machine, associating it with the previously created subnet and enabling dynamic private IP address allocation.

### Step 6: Create Azure Load Balancer

```yaml
resource "azurerm_lb" "example_lb" {
  name                = "example-lb"
  location            = azurerm_resource_group.example_rg.location
  resource_group_name = azurerm_resource_group.example_rg.name
  sku                 = "Standard"

  frontend_ip_configuration {
    name                 = "PublicIPAddress"
    public_ip_address_id = azurerm_public_ip.example.id
  }

  backend_address_pool {
    name = "backendPool"
  }

  probe {
    name                      = "tcpProbe"
    protocol                  = "Tcp"
    port                      = 80
    interval                  = 15
    threshold                 = 3
  }

  load_balancing_rule {
    name                       = "httpRule"
    frontend_ip_configuration = azurerm_lb.example_lb.frontend_ip_configuration[0]
    backend_address_pool_id    = azurerm_lb.example_lb.backend_address_pool[0].id
    probe_id                   = azurerm_lb.example_lb.probe[0].id
    protocol                   = "Tcp"
    frontend_port              = 80
    backend_port               = 80
  }
}
```

Explanation: This block defines an Azure Load Balancer, configuring frontend IP, backend address pool, health probe, and load balancing rule for TCP traffic on port 80.

## Conclusion

By following this step-by-step guide and utilizing Terraform to automate the provisioning of Azure resources, you can effortlessly set up a scalable and highly available infrastructure with Azure Load Balancer. Leveraging infrastructure as code principles, you can ensure consistency, repeatability, and efficiency in managing your cloud environment.

Remember, the cloud is vast, and Azure is your key to unlocking its full potential. Join us tomorrow as we dive deeper into the azure depths, uncovering more treasures that await on our journey through the cloud. Until then, happy exploring!

*Thank you for Reading:)*

*#Happy Reading!!*

***Any query and suggestion are always welcome -***[***Nehal Ingole***](http://www.linkedin.com/in/nehal-ingole)***or***[***Twitter***](https://twitter.com/IngoleNehal)