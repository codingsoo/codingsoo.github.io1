---
title: Kubernetes introduction
keywords: linux container, LXC, docker, kubernetes, microservice,  MSA, k8s
last_updated: June 7, 2020
tags: [lxc, docker, kubernetes]
summary: ""
sidebar: home_sidebar
permalink: kubernetes-introduction.html
folder: kubernetes
---

## Why Kubernetes?

Kubernetes is one of the most popular framework in Microservice Architecture(MSA). 
With MSA gaining popularity, the popularity of Kubernetes is also growing steeply.
A lot of companies (Google, IBM, Slack...) started to use Kubernetes, and the need of Kubernetes developer is increasing every year as well.

![kubernetes-permenant-demand-trend](images/kubernetes/permanent-demand-trend.png "https://www.itjobswatch.co.uk/jobs/uk/kubernetes.do")

What brought it into the spotlight? Let's figure it out!

### On-premise vs Microservice

![compare-monolithic-and-microservice](images/kubernetes/compare-monolithic-microservice.png "https://aws.amazon.com/ko/microservices")

Traditionally, on-premise software has monolithic architecture which means all components are combined into one service. If you want to scale the monolithic architectured software, you should copy all of the components to other server computer. For example, even if you only want to scale user account system, you should copy the whole system because you cannot detach only user account system. Also, it is hard to deal with library conflicts because they are all in the same environment. Lastly, you should build all the components and run them even if you edited small parts of the software.

![build-test-comparison](images/kubernetes/build-test-comparison.png "https://blog.lqcns.com/1278")

On the other hand, microservice architecture easily allows to set different dependencies for each component and also allows component specific scaling. Building and testing process is much simpler than monolithic architecture.
Then, does Microservice only have advantages? No!
The initial setting of microservice system is much harder than monolithic system. 
However, there are some useful tools to help you.
Let's study them now~

### Virtual machine vs Linux Container (LXC)

We now know the benefits of MSA. In MSA, there are two popular deployment types.

![container_evolution](images/kubernetes/container-evolution.svg "https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/")

The biggest difference is virtualized deployment has hardware virtualization part, so it is much slower than container deployment. 
Studies showed that Docker only loss about 1% of performance, but Virtual Machine (VM) loss more than 50%.
Therefore, LXC based deployment is becoming more popular.

### Relationship between LXC and Kubernetes

LXC provides light-weight isolated environment, but if you need hundreds of LXC, it might be hard to handle them one by one.
In this case, Docker helps you use many LXC easily. 
However, nowadays, systems are getting bigger and bigger too. You can easily see companies manage hundreds of Dockers.
Kubernetes allows us to manage lots of Dockers easily.

## Kubernetes Understanding

### LXC

LXC allows us to have isolated system. Linux provide LXC using Linux Namespace and Linux Control Group. Linux Namespace makes independent environment for each process and Linux Control Group can control resources (RAM, CPU, ...) for each process. You can get more information through this [link](https://linuxcontainers.org/lxc/getting-started/), but you don't need to study them to use Kubernetes and Docker.
### Docker

Docker is a very famous framework for managing LXC. It supports various OSs (Linux, Windows, Mac, ...) and a powerful client.
We can build images with program, library, and source code. With the image, we can build a LXC.
Docker provides powerful interface for this process. We will study this in the next lecture.

### Kubernetes

Docker is a very convenient tool, but if your service is large, you might need lots of Dockers.
We have a solution! Kubernetes!
Kubernetes is developed by Google with Go laungage. It helps to control large quantities of Dockers.

### DevOps

Devops is a compound word combining development and operationer. Developers usually make an appliaction and operation engineers usually make an infrastructure. They used to work seperately before, but DevOps can make them cowork easily by managing their life cycle together. 