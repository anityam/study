---
id: ognetf4t332vazgadsvn0ir
title: API Request
desc: ''
updated: 1705967779458
created: 1705965465269
---
# API Request
Kubernetes API is a REST Http API. So basic http calls can be made against the Kubernetes API.

## Setup
### Kind cluster
We will be using a kind cluster to setup the kubernetes cluster and make API calls against the kubernetes control plane created in the Kind cluster
Creating a cluster for testing API code can be found at [kubernetesGo](https://github.com/anityam/kubernetesGo/blob/main/README.md).

## Request

Kubectl is the main API client used for interacting with kubernetes API. Kubectl builds and makes the API calls on behalf of the user but to inspect the calls we can use the verbose option with different levels.

```bash
kubectl get pods -v6
I0122 18:26:21.852266   48957 loader.go:395] Config loaded from file:  ~/.kube/config
I0122 18:26:21.878357   48957 round_trippers.go:553] GET https://127.0.0.1:50107/api?timeout=32s 200 OK in 24 milliseconds
I0122 18:26:21.881194   48957 round_trippers.go:553] GET https://127.0.0.1:50107/apis?timeout=32s 200 OK in 1 milliseconds
I0122 18:26:21.890185   48957 round_trippers.go:553] GET https://127.0.0.1:50107/api/v1/namespaces/default/pods?limit=500 200 OK in 2 milliseconds
```
This will print the request header and request url

For further inDepth information on the request use the `-v8` which shows both request and response

### Labels
The most and powerful way of filtering a resource in kubernetes is through `labels`. Similar to 
```bash
kubectl get po -l k8s-app=kube-proxy -n kube-system
```
similar to 
```
curl http://localhost:8080/api/v1/namespaces/kube-system/pods?labelSelector=k8s-app==kube-proxy&limit=10
```

#### Advance labels 
Advance selection can be made with `in` `not in` selectors

in option
```bash
curl http://localhost:8080/api/v1/namespaces/kube-system/pods?labelSelector=k8s-app+notin+(kube-proxy,kindset)&limit=10
```
not in option
```bash
curl http://localhost:8080/api/v1/namespaces/kube-system/pods?labelSelector=k8s-app+in+(kube-proxy,kindset)&limit=10
```

### Field Selector
You can filter resources using a limited set of fields. For all resources, you can filter on the metadata.name field; and for all namespaced resources, you can filter on the metadata.namespace field. Plus some other additional fields are provided

```bash
curl http://localhost:8080/api/v1/namespaces/kube-system/pods?fieldSelector=status.phase=Running
```

### Deleting Resource
```bash
curl -X http://localhost:8080/api/v1/namespaces/project1/pods/nginx
```

### Updating Resource
For updating we need to use the PUT call
