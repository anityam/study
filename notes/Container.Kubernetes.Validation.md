---
id: jm9fx4snr8w1lj0hwz2w8eq
title: Validation
desc: ''
updated: 1691836687330
created: 1691835961744
---
# Validation

While working with the declarative language the bigger problem is with validation. The ecosystem of K8 is increasing with ever increasing list of good CRD(custom resource definition). As the declaration gets bigger so does the change of human error. 
We will look at some validation tools and how they can be used.

## Code
https://github.com/anityam/validation



## Scenario
In this topic we will be evaluating tools to validate istio and fluxCD crd's. 



## Tools

## Requirement
To validate kubernetes based native resources like pod, deployment it is easier as the definition of those resources are build in the installation but requires for other resource validation we will need to get the definitions of the crd's declaration for local use or access to a cluster with the CRD installed.
In a gitOps approach validation is good to be done locally before committing it to a automation framework like fluxCD. Each custom resource definition should have a resource definition which can be used.

### Kubectl validate
[kubectl validate](https://github.com/kubernetes-sigs/kubectl-validate) is an open source tool built by 