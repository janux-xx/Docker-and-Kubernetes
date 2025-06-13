# T08-01 The Multicontainer Pods

*As cloud-native architectures continue to evolve, Kubernetes has become the go-to platform for deploying complex, distributed systems. One of the most powerful yet nuanced design patterns in this ecosystem is the sidecar pattern—a technique that allows developers to extend application functionality without diving deep into source code.*



Let’s create multiple containers in a Pod using a YAML file.  We'll use the Busybox container to get the default page served by the Nginx container.

## Create the pod

    kubectl create -f two-containers.yaml

## Get some info

    kubectl get pods -o wide
    kubectl describe pod two-containers

## Connect to the BusyBox container

    kubectl exec -it two-containers --container mybox -- /bin/sh

## Fetch the HTML page served by the Nginx container

This will output the content of the Web page in the terminal.

    wget -qO- localhost

## Quit

    exit

## Cleanup

    kubectl delete -f two-containers.yaml --force --grace-period=0


[More info...](https://kubernetes.io/blog/2025/04/22/multi-container-pods-overview/)