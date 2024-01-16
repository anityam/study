---
id: tpze4uuw6xjq2id69dy1nw5
title: flux
desc: ''
updated: 1705368111365
created: 1705325162586
---

# Flux
Flux is a tool for keeping Kubernetes clusters in sync with sources of configuration (like Git repositories), and automating updates to configuration when there is new code to deploy.

## How it works 

It syncs the Git based kubernetes declarative code with the kubernetes cluster. It deploys operators in cluster who constantly monitor the versioned controlled repository.


## GitOps toolkit

### Source
The main role of the source is to provide an interface for artifact acquisitions. This contains the location of source of truth and a way to connect to it. For example
```yaml
apiVersion: source.toolkit.fluxcd.io/v1
kind: GitRepository
metadata:
  name: flux-system
  namespace: flux-system
spec:
  interval: 1m0s
  ref:
    branch: main
  secretRef:
    name: flux-system
  url: ssh://git@github.com/anityam/fluxy
  ```
  This above declaration contains the definition of a [git repository](https://github.com/anityam/fluxy) over ssh which is synced at an interval of 1m(defaults to 5m).
  
  The source produces an artifact that is consumed by other flux components to perform actions.All sources are specified as Custom Resources in a Kubernetes cluster, examples of sources are GitRepository, OCIRepository, HelmRepository and Bucket resources. More reading on [source resource](https://fluxcd.io/flux/components/source/) and [spec](https://github.com/fluxcd/source-controller/tree/main/docs/spec)

  Features:
    1. Validate source definitions
    2. Authenticate to sources (SSH, user/password, API token)
    3. Validate source authenticity (PGP)
    4. Detect source changes based on update policies (semver)
    5. Fetch resources on-demand and on-a-schedule
    6. Package the fetched resources into a well-known format (tar.gz, yaml)
    7. Make the artifacts addressable by their source identifier (sha, version, ts)
    8. Make the artifacts available in-cluster to interested 3rd parties
    9. Notify interested 3rd parties of source changes and availability (status conditions, events, hooks)


## Reconciliation
The process to make sure a given state matches a desired state which is declared in a versioned controlled repo.

1. **HelmRelease reconciliation**: ensures the state of the Helm release matches what is defined in the resource, performs a release if this is not the case (including revision changes of a HelmChart resource).
2. **Bucket reconciliation**: downloads and archives the contents of the declared bucket on a given interval and stores this as an artifact, records the observed revision of the artifact and the artifact itself in the status of resource.
3. **Kustomization reconciliation**: ensures the state of the application deployed on a cluster matches the resources defined in a Git or OCI repository or S3 bucket.

## Kustomization
Kustomization CRD is local set of overlays that flux needs to reconcile to the cluster. Reconcile runs every 5m but this can be adjusted. If you make any changes to the cluster using kubectl edit/patch/delete, they will be promptly reverted. You either suspend the reconciliation or push your changes to a Git repository.

For more information, take a look at the [Kustomize FAQ](https://fluxcd.io/flux/faq/#kustomize-questions) and the [Kustomization CRD](https://fluxcd.io/flux/components/kustomize/kustomizations/).

## Bootstrap
Bootstrapping flux to a cluster i.e installing flux component in gitOps manner. Flux manages itself through git similar to other application and infrastructure management. The manifests are applied to the cluster, a GitRepository and Kustomization are created for the Flux components, then the manifests are pushed to an existing Git repository (or a new one is created).  

For more information, take a look at the [bootstrap documentation](https://fluxcd.io/flux/installation/bootstrap/).


## Demo
[Fluxy](https://github.com/anityam/fluxy)


## Reading
[Documentation](https://fluxcd.io/flux/)
