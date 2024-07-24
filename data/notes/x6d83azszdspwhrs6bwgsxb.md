# Kind, Group and Version in Kubernetes
## Group
Group is a collection of related functionality. As each group progresses over time it is classified into different versions
e.g. /api/apps/v1 but for the core group it is still /api/v1 like for pods

## Kind
API group-version contains one or more API types, which we call Kinds

## Resource 
It's the declaration of a specific kind.

So a particular version of kind is GVK group version kind and a particular resource is GVR group version resource.

## Different API's for Kubernetes
https://kubernetes.io/docs/reference/generated/kubernetes-api/v{what version to look for}