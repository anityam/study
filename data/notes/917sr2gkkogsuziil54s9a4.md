# Etcd
This is the defacto storage implementation for the kubernetes cluster. Etcd is a separate project which was adopted by kubernetes community to be used as the backend

## Key concepts of Etcd

1. Written in go and has a SDK([clientV3](https://pkg.go.dev/go.etcd.io/etcd/clientv3))
2. `Watch()` API support which is used by kubernetes also `gRPC` protocols
3. Support for time-travel queries through Multi-Version Concurrency Control([MVCC](https://en.wikipedia.org/wiki/Multiversion_concurrency_control))


## Working

### Key Value store
It is like a dictionary {"key":"value"}. 

### Etcd server





## More Information
### Reading
https://pierrezemb.fr/posts/notes-about-etcd/

### Tools
https://hub.docker.com/r/bitnami/etcd/ ---> etcd docker based images
