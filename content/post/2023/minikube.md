---
title: "Setup Minikube on Ubuntu 22.04 LTS without virtualization support"
date: 2023-08-03T01:47:56+05:30
lastmod: 2023-08-03T01:47:56+05:30
draft: true
keywords: []
description: "Setup Minikube in Thinkpad  T480 without virtualization support"
tags: ["kubernetes", "minikube"]
categories: []
author: "Raman Tehlan"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: false
postMetaInFooter: false
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""

---

I always wanted to have a home server, which I could ssh into from 
anywhere, and run my side projects on it. Last month I decided to 
create one, and I am documenting the process here.

## Hardware

I had an old laptop lying around, which I decided to use as my home server. It's ThinkPad T480, 16GB RAM, 512GB SSD, and i5 8th gen processor. I installed Ubuntu 22.04 LTS on it, and it's working great. Unfortunately, It doesn't have virtualization support, so I can't run VMs on it. But I can run containers, which is enough for my use case. 

## Software

I was going through different options for running containers, and I decided to go with Kubernetes. It's a great tool for running containers, and it's used by most of the big companies. However, instead of installing Kubernetes, I decided to run a development/learning on my server. This server isn't intended to be used in production anyway.

There are many tools to create a k8s learning/development environment, Like Kind, Kubectl, or even Docker Desktop was an option.


Docker Desktop however needs virtualization support, which my laptop doesn't have. So I thought of using Kind or Minikube, and I couldn't find any major difference between the two. Though, Minikube is more popular. 


## Installing Docker

You can find the instructions here: https://docs.docker.com/engine/install/ubuntu/

```bash

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Installing Minikube

You can find the instructions here: https://minikube.sigs.k8s.io/docs/start/
Minikube supports multiple drivers, like docker, kvm2, virtualbox, etc. I am using docker driver, as it's the only one which works on my laptop. Podman is experimental, KVM, VirtualBox, QEMU require virtualization support, which my laptop doesn't have. (I wish I had a better laptop :P)

```bash
minikube config set driver docker
```

```bash 
minikube start --alsologtostderr -v=1 --extra-config=kubelet.resolve-conf=/etc/resolv.conf --container-runtime=containerd --cpus 6 --memory 14000
# --alsologtostderr is optional, it's used to print logs to stdout
# -v is used to set the log level, 1 is the lowest level, and 5 is the highest
# --extra-config=kubelet.resolve-conf=/etc/resolv.conf is used to fix the DNS issue, which I was facingA
# --container-runtime=containerd is used to set the container runtime to containerd, which is required for the docker driverA
# --cpus 6 is used to set the number of CPUs to 6
# --memory 14000 is used to set the memory to 14GB
```

That's all folks, that's all it takes to set up your mini Kubernetes cluster on your laptop. You can now use kubectl to interact with your cluster. 

I will talk about connecting to the k8s cluster from your local machine in the next post and connecting it to SSH, we will also set up a reverse proxy to access the k8s dashboard from outside the server.

The plan is to eventually setup different projects on this server. Stay tuned for more updates.


