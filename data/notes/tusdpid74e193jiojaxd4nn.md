# Go Programming In Kubernetes

## Introduction
Kubernetes is a container orchestration tools which uses declarative method. Kubernetes has an API through which we can interact. It is a REST HTTP based API.

## Working
In the beginning of the chain, users declare a high level resources like Pods, Deployments etc. Once the resources are declared then the middle level component called controllers are activated to transfer them into low-levels Pods. Then the schedular distributes those resources in the nodes. Now the node agent deploys the Pod in the scheduled cluster.

## Control Plane
The control plane is the main brain of the kubernetes. It handles all the complexity of handling the declared resources in the cluster. It's main components are 
1. The API Server - This is the main gateway through which the communication to the cluster is done
2. The etcd database - This is a database which stores the state of the cluster. Only accessible through API server.
3. The controller manager - This manages the controllers which transforms the users declared resources to kubernetes low level components. The controller sync with the API to maintain the state of the resources.
4. Schedular - It maintains the resource distribution in the nodes. It watches the api server for change
5. Kubelet - Agent in each nodes. It manages workload specified to it's specific node after schedular schedules it. It watches the API server for any change in its node.
6. Kube-Proxy - Agent to manage network. Runs on all nodes and watches the API server for any change

## API
##  Cluster
Creating a cluster for testing API code can be found at [kubernetesGo](https://github.com/anityam/kubernetesGo).

### OpenAPI
Kubernetes uses the openAPI format to specify it REST API HTTP calls. To check