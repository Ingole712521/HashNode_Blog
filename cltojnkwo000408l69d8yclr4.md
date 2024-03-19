---
title: "Jenkins Firewall"
seoTitle: "Jenkins Firewall"
datePublished: Tue Mar 12 2024 15:45:34 GMT+0000 (Coordinated Universal Time)
cuid: cltojnkwo000408l69d8yclr4
slug: jenkins-firewall
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710258033916/1a2bbf24-7a6f-4d01-bc4b-98fd2cdb52fe.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1710258317169/55fd4046-a034-43a2-a4cc-675c05f79831.jpeg
tags: accessibility, devops, jenkins, firewall, cicd, 2articles1week, ci-cd, learning-journey, learn-in-public, jenkins-port-change

---

## Introduction

Jenkins is a popular automation server used for continuous integration and continuous delivery (CI/CD) pipelines in software development. To allow external access to Jenkins, it's essential to configure the firewall to permit traffic on the Jenkins port. In this guide, we'll walk through the process of enabling Jenkins in Firewalld, ensuring that your Jenkins server can be accessed from outside the local network.

## Setting up Jenkins

Before enabling Jenkins in Firewalld, ensure that Jenkins is installed and running on your server. You can download and install Jenkins from the official website and follow the installation instructions for your operating system.

## Checking Jenkins Port

By default, Jenkins runs on port 8080. However, you should verify the port configuration in the Jenkins settings or configuration file. Note the port number that Jenkins is configured to use, as we'll need it to open the port in Firewalld.

## Opening the Port in Firewalld

To allow traffic on the Jenkins port through Firewalld, follow these steps:

1. Open a terminal or SSH session to your server.
    
2. Use the following command to open the Jenkins port in Firewalld, replacing `8080` with the actual port number if Jenkins is configured to use a different port:
    

```bash
sudo firewall-cmd --zone=public --add-port=8080/tcp --permanent
```

3. This command adds a rule to allow TCP traffic on port 8080 (or the specified port) in the public zone of Firewalld. The `--permanent` option makes the rule persistent, so it persists across firewall reloads or system reboots.
    

## Reloading Firewalld

After adding the port, reload Firewalld to apply the changes:

```bash
sudo firewall-cmd --reload
```

This command reloads Firewalld and applies the changes made to the firewall rules.

## Verifying the Changes

You can verify that the port is open in Firewalld by listing the active zones and checking the allowed ports:

```bash
sudo firewall-cmd --zone=public --list-ports
```

Ensure that the port used by Jenkins (8080 by default) is listed among the allowed ports.

## Testing Jenkins Accessibility

With the firewall configured to allow traffic on the Jenkins port, you should now be able to access Jenkins from outside the local network. Open a web browser on another machine and enter the IP address or domain name of your Jenkins server followed by the port number (e.g., [`http://your_server_ip:8080`](http://your_server_ip:8080)). If Jenkins loads successfully, it means that external access has been enabled.

## Conclusion

Enabling Jenkins in Firewalld is crucial for allowing external access to your Jenkins server and facilitating collaboration among team members. By following the steps outlined in this guide, you can configure Firewalld to permit traffic on the Jenkins port, ensuring seamless access to Jenkins from outside the local network.

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)