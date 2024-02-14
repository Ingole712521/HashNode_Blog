---
title: "Unleashing the Power of Ansible"
seoTitle: "Unleashing the Power of Ansible"
datePublished: Wed Feb 14 2024 04:30:31 GMT+0000 (Coordinated Universal Time)
cuid: clslanghl000809l3e2wffsvy
slug: unleashing-the-power-of-ansible
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707668725575/95d1ecf7-61b1-4d92-89e5-784b292e563e.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1707668817192/4a64eeb1-0df9-4623-bf9e-260e96408658.png
tags: ubuntu, aws, ansible, devops, redhat, learning-journey, devops-articles, ansible-playbook

---

Welcome to our comprehensive guide to Ansible, the game-changing automation tool that simplifies complex tasks with ease. Whether you're just starting your journey into the world of tech or looking to expand your skill set, this blog will provide you with a solid foundation in Ansible, complete with animations to enhance your learning experience.

## **Introduction to Ansible**

Ansible is an open-source automation platform that streamlines IT operations by automating repetitive tasks, simplifying configuration management, and orchestrating complex workflows. Unlike other automation tools, Ansible requires no agents or additional software installed on remote systems, making it lightweight and easy to deploy.

## **Getting Started with Ansible**

Let's dive right in! To begin using Ansible, you'll need to set up a control node, which serves as the central hub for managing your infrastructure. This control node can be any machine with Python installed, such as your local computer or a dedicated server.

Once you have your control node set up, you can start writing Ansible playbooks, which are YAML files that define the desired state of your infrastructure. Playbooks consist of tasks, which are executed sequentially, and each task defines a specific action to be performed, such as installing software, configuring settings, or restarting services.

## **Understanding Ansible Core Concepts**

Before we delve deeper into Ansible playbooks, let's familiarize ourselves with some core concepts:

1. **Inventory**: An inventory is a file that contains a list of hosts (remote systems) that Ansible will manage. Hosts can be grouped into categories, making it easy to target specific subsets of your infrastructure.
    
2. **Modules**: Ansible modules are reusable units of code that perform specific tasks, such as managing files, installing packages, or executing shell commands. Modules are idempotent, meaning they can be run multiple times without changing the system's state if the desired state is already achieved.
    
3. **Tasks**: Tasks are individual actions defined within Ansible playbooks. Each task specifies a module to execute and any required parameters. Tasks are executed sequentially and can include conditionals, loops, and error handling to handle complex scenarios.
    

## **Creating Your First Ansible Playbook**

Now that we have a basic understanding of Ansible's core concepts, let's create our first playbook to automate a simple task: installing a package.

```yaml
- name: Install Nginx
  hosts: web_servers
  become: true
  tasks:
    - name: Ensure Nginx is installed
      yum:
        name: nginx
        state: present
    - name: Start Nginx service
      service:
        name: nginx
        state: started
```

### In this playbook

* We specify the name of the playbook and the target hosts in the `hosts` section.
    
* We use the `yum` module to install the Nginx package.
    
* We use the `service` module to start the Nginx service.
    

## **Executing Your Ansible Playbook**

Once you've created your playbook, you can execute it using the `ansible-playbook` command:

```yaml
ansible-playbook -i inventory.yaml playbook.yaml
```

Replace `inventory.yaml` with the path to your inventory file and `playbook.yaml` with the path to your playbook file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707668089545/d3f3979c-380e-4929-89ed-1c5e7e492ce3.png align="center")

## **Hadoop Setup with the help of Ansible playbook**

First, let's outline the steps involved:

1. Set up the inventory file to define the groups of Ubuntu and Red Hat Linux instances.
    
2. Install Java on all instances (required for running Hadoop).
    
3. Download and install Hadoop on all instances.
    
4. Configure Hadoop on the master node.
    
5. Configure Hadoop on the slave nodes.
    
6. Start the Hadoop services.
    

Now, let's create the Ansible playbook (`hadoop_cluster.yml`) and explain each step:

```yaml
- name: Set up Hadoop cluster
  hosts: all
  become: true
  vars:
    hadoop_version: "3.3.1"
    java_package: "openjdk-11-jdk"  
    hadoop_download_url: "https://archive.apache.org/dist/hadoop/common/hadoop-{{ hadoop_version }}/hadoop-{{ hadoop_version }}.tar.gz"
    hadoop_install_dir: "/opt/hadoop"

  tasks:
    - name: Install Java
      package:
        name: "{{ java_package }}"
        state: present

    - name: Download Hadoop
      get_url:
        url: "{{ hadoop_download_url }}"
        dest: "/tmp/hadoop-{{ hadoop_version }}.tar.gz"

    - name: Extract Hadoop
      ansible.builtin.unarchive:
        src: "/tmp/hadoop-{{ hadoop_version }}.tar.gz"
        dest: "{{ hadoop_install_dir }}"
        remote_src: yes
        creates: "{{ hadoop_install_dir }}/bin/hadoop"

    - name: Configure Hadoop
      template:
        src: "{{ item }}"
        dest: "{{ hadoop_install_dir }}/etc/hadoop/{{ item }}"
      with_items:
        - core-site.xml
        - hdfs-site.xml
        - mapred-site.xml
        - yarn-site.xml

    - name: Format HDFS NameNode
      command: "{{ hadoop_install_dir }}/bin/hdfs namenode -format"
      environment:
        HADOOP_HOME: "{{ hadoop_install_dir }}"
      when: inventory_hostname in groups['namenodes']

    - name: Start Hadoop services
      shell: "{{ hadoop_install_dir }}/sbin/start-all.sh"
      args:
        executable: /bin/bash
      environment:
        HADOOP_HOME: "{{ hadoop_install_dir }}"
      when: inventory_hostname in groups['namenodes'] or inventory_hostname in groups['datanodes']
```

## Explanation of the playbook

* ### Set up Hadoop cluster
    
    Defines the playbook to run on all hosts with elevated privileges.
    
* ### Variables
    
    Defines variables for Hadoop version, Java package, download URL, and installation directory.
    
* ### Install Java
    
    Installs Java on all hosts.
    
* ### Download Hadoop
    
    Downloads the Hadoop binary package to the temporary directory.
    
* ### Extract Hadoop
    
    Extracts the Hadoop binary package to the installation directory.
    
* ### Configure Hadoop
    
    Copies configuration files (core-site.xml, hdfs-site.xml, mapred-site.xml, yarn-site.xml) from the playbook directory to the Hadoop configuration directory.
    
* ### Format HDFS NameNode
    
    Formats the HDFS NameNode, applicable only to hosts in the 'namenodes' group.
    
* ### Start Hadoop services
    
    Starts all Hadoop services, applicable to hosts in the 'namenodes' and 'datanodes' groups.
    

Make sure to adjust the playbook according to your AWS setup, such as updating the Java package for Red Hat Linux and defining the specific groups for NameNodes and DataNodes in your inventory file.

Additionally, you'll need to create template files (`core-site.xml`, `hdfs-site.xml`, `mapred-site.xml`, `yarn-site.xml`) in the same directory as the playbook, containing the configuration settings for your Hadoop cluster.

That's it! You now have an Ansible playbook to set up a Hadoop cluster on Ubuntu and Red Hat Linux instances on AWS.

---

## **Conclusion**

Congratulations! You've now learned how to set up a Hadoop cluster using Ansible on both Ubuntu and Red Hat Linux instances in the AWS environment. With automation tools like Ansible, complex tasks become manageable and repeatable, saving you time and effort in your infrastructure management.

**Ready to Dive In?** If you have any questions or need further assistance in setting up your Hadoop cluster, feel free to reach out to [Nehal Ingole](https://twitter.com/IngoleNehal). I'm here to help!

**J**[**oin Me**](https://learnwithnehal.hashnode.dev/)**:** Are you passionate about technology and eager to share your knowledge with others? If so, I invite you to join me in writing blog posts and tutorials to help others navigate the world of tech. Together, we can make learning more accessible and enjoyable for everyone. Reach out to me if you're interested in collaborating!

Thank you for reading, and happy automating! 🚀✨