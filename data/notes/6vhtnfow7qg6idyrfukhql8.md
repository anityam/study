# GitOps

The core idea of GitOps is having a Git repository that always contains declarative descriptions of the infrastructure currently desired in the production environment and an automated process to make the production environment match the described state in the repository. If you want to deploy a new application or update an existing one, you only need to update the repository - the automated process handles everything else. It’s like having cruise control for managing your applications in production.

## Why to use GitOps
1. Deploy faster and more often: This is the benefit of using version control. 
2. Easy and fast recovery: Easy to move back to previously known configuration
3. Secure: Let tools apply changes to cluster not the developers directly
4. Documenting: Easy to watch the git repo for what changes have happen and what are upcoming changes

## How it works
Central repository that holds the environment and application setup. It can be branched out into two separate repository or a single git repository. 

## Deployment Style
### Pull Based Deployment
In this system there is an operator making sure to sync the environment. So a developer makes changes to the application and new images is build. The operator constantly monitors the image or the environment and will update to the latest code when it sees the new image.

### Push Based Deployment
This is a deployment style where a push of code to the application triggers a series of deployment procedures which finally results in environment change in the cluster.


Reading:
[GitOps pdf](./gitops.pdf)
