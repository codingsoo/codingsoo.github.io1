---
title: Start docker and kubernetes
keywords: linux container, LXC, docker, kubernetes, microservice,  MSA
last_updated: June 7, 2020
tags: [docker, kubernetes]
summary: "Let's start docker and kubernetes! Reference: https://www.notion.so/3f5794b5aafe44e7835e55e70c8debf5 (Korean)"
sidebar: home_sidebar
permalink: start-docker-and-kubernetes.html
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

### Virtualization vs Container

We now know the benefits of MSA. In MSA, there are two big deployment types.

![container_evolution](images/kubernetes/container-evolution.svg "https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/")

The biggest difference is virtualized deployment has hardware virtualization part, so it is much slower than container deployment. Studies showed that Docker only loss about 1% of performance, but Virtual Machine (VM) loss more than 50%.

### Conclusion

Linux Container(LXC) provides light-weight isolated environment. Docker can manage LXCs. Kubernetes is able to manage LXCs and Dockers.

## Microservice Understanding

### LXC

LXC allows us to have isolated system.Linux provide LXC uses Linux Namespace and Linux Control Group. Linux Namespace makes independent environment for each process and Linux Control Group can control resources (RAM, CPU, ...) for each process. 

### Docker

Docker is the most famous framework which manage LXCs. It supports various OSs (Linux, Windows, Mac, ...) and provides Containerd which manages LXCs.
We can build images with program, library, and source code. With the image, we can build LXCs.
Docker provides powerful interface for this process. We will study this in the next lecture.
However, even if we use Docker, it is hard to manage all the LXCs if the service is large. 
We have solution! Kubernetes!

### Kubernetes

Kubernetes is developed by Google with Go laungage. It helps to control large quantities of Dockers and LXCs.

### DevOps

Devops is a compound word combining development and operationer. Developers usually make appliaction and operation engineers usually make infrastructure. They seperately work before, but DevOps can make them cowork easily by managing life cycle together. 