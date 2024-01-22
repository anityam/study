---
id: gbadp33e8k0kkmvcnic0ucs
title: Kind
desc: Local cluster tool
updated: 1690635927681
created: 1690635610877
---
# Kind 

This is a local development environment. This is a tool to build a local k8 cluster in your local laptop for testing or development.The tool is maintained by the kubernetes team.

## Usage 
It is based on the concept of creating a kubernetes cluster with containers. So it does required the presence of docker or any other container runtime in the system be present. `kind` is a local cli tool that can be use to create, delete or interact with the cluster.


### Cli
The cli can be installed through go
```bash 
go install sigs.k8s.io/kind
```

In mac it can be installed through brew
```bash
brew install kind
```



## Document
https://kind.sigs.k8s.io/ ---> Kind Docs