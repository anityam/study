# Kubernetes 
The major orchestration tool in the market that every one uses. 

## Introduction


## Component
All components in kubernetes are loosely coupled actors which communicate through REST API which is backed by a highly available store called etcd.
![ kubernetes component](./assets/images/k8s-arch.png. 

All the component and the kubelet work in a continuous loop to bring the resources to the current state defined in the etcd and informed by the API server. The api implements push bashed notification system called `watch`(Need more details on this)

### Etcd




## Reading 
https://www.mgasch.com/2021/01/listwatch-part-1/