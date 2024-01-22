# Kubernetes API
Kubernetes api is the main communication channel for the kubernetes cluster. It is a part of the `kubernetes control plain`. This is the heart of communication

## Function
1. Serve the kubernetes API for state change
    1. Reading state : get,list and streaming
    2. Mutating state: create, update delete
2. Proxy cluster component so other tools can use them like pod exec by kubectl or log streaming etc

## How 
The main concept is api calls in kubernetes are `rest API` based calls exposed through https with json or `protobuf` payload. The rest method used are GET,POST,PUT, PATCH, DELETE.

## What 
The terms used
1. Kind: All resource types have a concrete representation (their object schema) which is called a kind --> or a simple definition is json-schema of an object
    1. persistent object like pod, service etc
    2. list of persistent objects like pods 
    3. Simple --> Special purpose kinds used like APIGroup or APIResource , or simply a specific action on a persistent resource(object)
2. Group: Collection of related kinds 
3. Version: The version of apiGroup to be used v1alpha1,  v1beta1 etc
4. Resources: These are the endpoints of the kubernetes api api/{resource}. This can also be termed as an item of a `kind`
    ```
    kubectl api-resources
    kubectl api-resources -v 6 # -v 6 means "extra verbose logging"
    ```
5. Objects: This is similar to kind which means persistent entities with intent (desired state) and the status (actual state) of the cluster. So it has some defined fields.
    ```
    kubectl explain  # commands helps with 
    ```

## Declare
Declarative state in kubernetes. `Spec` describes what you want.`Status` is the current state of the resource you described in the `spec`.

## Query
API server can be queried through the REST http calls so once the api server endpoint is exposed we can query the 
`/apis/group/version/{namespace/namespace_name}/resource` --> namespaced resources need the namespace. For more info on the api-resources{endpoint}
```bash
kubectl api-resources
kubectl api-versions
```

## API Operation
###  Cluster
Creating a cluster for testing API code can be found at [kubernetesGo](https://github.com/anityam/kubernetesGo).

### API calls
In daily 

## Request
The request once done is passed through a chain of filters which is processed by [DefaultBuildHandlerChain](https://github.com/kubernetes/kubernetes/blob/2cb31c9333adca3f212920d7a1a4e0a3a239598d/staging/src/k8s.io/apiserver/pkg/server/config.go#L790C6-L790C30). 



## Reading
https://kubernetes.io/docs/reference/using-api/api-concepts/#:~:text=Kubernetes%20API%20terminology&text=All%20resource%20types%20have%20a,also%20usually%20represents%20an%20object --> API
https://iximiuz.com/en/posts/kubernetes-api-structure-and-terminology/ --> Terminologies

## Working repo
https://github.com/anityam/kube-programming 

