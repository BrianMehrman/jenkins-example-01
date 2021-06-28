# Jenkins Kubernetes Example

This is an example setup to run Jenkins.

Source: https://www.youtube.com/watch?v=eRWIJGF3Y2g


https://github.com/nestybox/sysbox/blob/master/docs/user-guide/install-k8s.md



1. In jenkins build docker image of app
    1. pull branch
    2. build image in jenkins worker. 
    3. rely on image being available in local docker registry
2. Launch deployer job to build new customization configs
  1. pass in url to configs
  2. pass in images name
  3. pass in options for environment that need to overridden
3. Apply configs to cluster to test namespace.
4. Launch test job to test namespace, wait for job to finish.
5. When job is finished clean up namespace.
6. If test passed push image up to docker hub
7. Notify user of build and test results.


## Launch dependencies

```
kind create cluster --name=test-env
kubectl create ns jenkins
kubectl config set-context --current --namespace=jenkins
kubectl apply -k kubernetes
```


## Expose port

```

```