# Jenkins Kubernetes Example

This is an example setup to run Jenkins.

## Overview of setup

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

## Project dependencies

These are the dependencies this project has. Sorry not everything will have a link
 * Kind
 * Kubectl
 * docker

This jenkins example was built around building and deploying this
[sample project](https://github.com/BrianMehrman/simple-python-app/tree/jenkins-build-test).


## Launch dependencies

```
kind create cluster --name=test-env
kubectl create ns jenkins
kubectl config set-context --current --namespace=jenkins
kubectl apply -k kubernetes
```

## Expose Jenkins locally

```
kubectl port-forward service/jenkins 8080:8080 -n jenkins
```

## Connect to Jenkins pod

Find the pod name using `kubectl get pods`. It will be prefixed with `jenkins`.

For example my pods name was `jenkins-5c497b9b-t57s2`. Replace my pod id with yours.

```
kubectl exec -it jenkins-5c497b9b-t57s2  -c jenkins bash
```

## References:

__Main Source__: https://www.youtube.com/watch?v=eRWIJGF3Y2g

* https://github.com/marcel-dempers/docker-development-youtube-series/tree/master/jenkins
* https://medium.com/vivid-seats-engineering/how-to-kubernetes-pods-as-jenkins-build-agents-a726d3886861
* https://nieldw.medium.com/curling-the-kubernetes-api-server-d7675cfc398c
