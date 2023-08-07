---
id: fg4zd4onhild1u1uhv2h2ju
title: cluster
desc: 'GitOps Cluster'
updated: 1689734742672
created: 1689734234547
---

# Cluster 
The main orchestration tool for the contianers that will be deployed. The approach is to have a local cluster using a tool like kind or minikube and then deploye and maintain the resources in the cluster using a tool like flux.

## Local Deployment
The main initial step for the cluster is to have an infrastrucutre where the cluster can be installed. Just like any other piece of software the cluster orchestration tool requires an infrastructure which is a seriers of servers or contianers that provides an interface like a server.In a enterprise level that can be a datacenter with a series of servers with extensive cpus, memory and storage or a cloud based interface like eks, ecs etc. For a local deployment we will be using the virtualization tools like hyperV to build a virutal servers or container based environment with kind or minikube.

In this example we will use KinD.

