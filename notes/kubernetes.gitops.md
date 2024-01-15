---
id: 6vhtnfow7qg6idyrfukhql8
title: Gitops
desc: ''
updated: 1705336152951
created: 1705326094609
---
# GitOps

The core idea of GitOps is having a Git repository that always contains declarative descriptions of the infrastructure currently desired in the production environment and an automated process to make the production environment match the described state in the repository. If you want to deploy a new application or update an existing one, you only need to update the repository - the automated process handles everything else. It’s like having cruise control for managing your applications in production.

## Why to use GitOps
1. Deploy faster and more often: This is the benefit of using version control. 
2. Easy and fast recovery: Easy to move back to previously known configuration
3. Secure: Let tools apply changes to cluster not the developers directly
4. Documenting: Easy to watch the git repo for what changes have happen and what are upcoming changes

## How it works
Central repository that holds the environment and application setup. It can be branched out into two separate repository or a single git repository. 



Reading:
[GitOPs pdf](./gitops.pdf)
