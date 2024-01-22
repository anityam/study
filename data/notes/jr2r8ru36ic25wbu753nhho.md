# Kubernetes Tools
This section is a subset of Containers tools where we will entirely discuss upon kubernetes based tools.

## Management
The tools that can be used to manage the kubernetes cluster itself.

### K9
Tool to manage kubernetes.[[Kubernetes.tools.K9]]


## Shell
### Kubectx
`brew install kubectx` This will make it easy to change context between different kubernetes cluster defined in your config file. More detail on [installation](https://github.com/ahmetb/kubectx)
Setting up autocompletion for kubens and kubectx 
```bash
 mkdir ~/.oh-my-zsh/custom/completions
 chmod -R 755 ~/.oh-my-zsh/custom/completions
```
Get the zsh autocompletion from the github repo and create a file in the `~/.oh-my-zsh/custom/completions/{_kubectx.zsh,_kubens.zsh}`. Make it executable and check the script for the location of the cli in your environment. then
```bash
echo "fpath=($ZSH/custom/completions $fpath)" >> ~/.zshrc
```
 If it still doesn't workout after the source of `~/.zshrc` then add `autoload -U compinit && compinit` to your `zshrc`

### Kubens 
`brew isntall kubectx` will install the kubens tools too which is useful in changing the namespace quickly.

### Kube-ps1
This is a addons prompt for the zsh or bash
```brew install kube-ps1```

update your `.zshrc` to add 
```
plugins=(
  kube-ps1
)

PROMPT='$(kube_ps1)'$PROMPT # or RPROMPT='$(kube_ps1)'
```

### Stern
For logs 
```
brew install stern
```

### Popeye
Find vulnerability in k8 cluster
```
brew install derailed/popeye/popeye
```

### zsh plugins
Kubectl plugin add it to the `~/.zshrc`
```
plugins=(
    ...
    kubectl
)```





## Document
https://agrimprasad.com/post/supercharge-kubernetes-setup/ ---> Kubernetes setup
https://github.com/ahmetb/kubectx Kubectx Project
https://github.com/stern/stern --> stern project
https://agrimprasad.com/post/supercharge-kubernetes-setup/ 
