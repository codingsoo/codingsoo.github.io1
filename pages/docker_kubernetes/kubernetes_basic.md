---
title: Basic of Kubernetes
keywords: kubernetes
last_updated: June 8, 2020
tags: [kubernetes]
summary: "Let's start kubernetes basic! Reference: https://www.notion.so/3f5794b5aafe44e7835e55e70c8debf5 (Korean)"
sidebar: home_sidebar
permalink: kubernetes-basic.html
folder: kubernetes
---

## Kubernetes

### Introduction

We learned Docker enables to manage Containers easily. In the similar way, Kubernetes can manage Dockers conveniently. Kubernetes can treat lots of nodes as one big computer. 

![kubernetes-architecture](images/kubernetes/k8s-architecture.png "https://dockerlabs.collabnix.com/kubernetes/beginners/what-is-kubernetes/#what-is-kubernetes")

- Master node: Control the whole kubernetes system 
- API server: It acts like a captain. It manages authentication, permission, and communication of Kubernetes elements. Only it can access etcd, controller-manager, scheduler, and worker node.
- Etcd: Database of cluster configuration
- Scheduler: Determine which container goes to which node.
- Controller-manager: Manage resources.
- Worker node: Manage application execution
- Kubelet: It acts like a captain in the worker node. Receive command from API server and manage the container runtime.
- Kube-proxy: Manage communication of the worker node.

### Benefits

- Simple deployment (infrastructure is abstracted)
- Easy resource management (each pod and node can be moved easily)
- Convenient monitoring
- Self reparing system
- Easy development (no dependency problem & exactly the same environment)
- Auto-scaling
- Auto-testing

### Installation

Check these first.

1. Each node should have different host name (/etc/hostname)
2. Each node should have different MAC address
3. Use NAT network (not NAT)
4. Turn off swap (type sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab and reboot)

If you use Ubuntu or Debian, copy and paste below commands.
If you use other OS, follow instructions in this link: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
```
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

Start master node

```
# You should type this in master node
kubeadm init
```

When the initialization is finished, You might see two configuration instructions.

1. To start using your cluster, you need to run the following as a regular user: [content 1]
2. Then you can join any number of worker nodes by running the following on each as root: [content 2]

Copy and paste [content 1] to master node in regular user terminal and [content 2] to work node in root user terminal.

If you want to join another work nodes, type "kubeadm token create --print-join-command" on your master node to get [content 2] again.

### Setting network

Now, we need to set network. 
There are some networks and they have their own advantages and disadvantages, but we will install Weavenet here.
If you want to use other network, see this link: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/
Type below command in master node.

```
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```

### Commands in Kubernetes

```
# Reset kubeadm. If you use have problem in joinning, type this in each work node.
kubeadm reset

# Deploy kubernetes
kubectl create deploy [app name] --image=[docker image name]
```
