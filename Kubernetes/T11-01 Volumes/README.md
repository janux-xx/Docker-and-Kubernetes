# T11-01 The Volumes

*Kubernetes volumes provide a way for containers in a pod to access and share data via the filesystem.*

> There are different kinds of volume that you can use for different purposes, such as:

* populating a configuration file based on a ConfigMap or a Secret.

* providing some temporary scratch space for a pod.

* sharing a filesystem between two different containers in the same pod.

* sharing a filesystem between two different pods (even if those Pods run on different nodes).

* durably storing data so that it stays available even if the Pod restarts or is replaced.

* passing configuration information to an app running in a container, based on details of the Pod the container is in (for example: telling a sidecar container what namespace the Pod is running in).

* providing read-only access to data in a different container image.

> Data sharing can be between different local processes within a container, or between different containers, or between Pods

## Create the Persistent Volume

    kubectl apply -f pv.yaml

## Look at the pv

    kubectl get pv

## Deploy the claim

    kubectl apply -f pvc.yaml

## Look at the pvc

    kubectl get pvc

## Deploy the pod

    kubectl apply -f pod.yaml

## Connect to the Busybox instance

    kubectl exec mybox -it -- /bin/sh

## Create a file

    cd demo
    cat > hello.txt
    Hello World
    Enter and Ctrl-D
    ls
    exit

## Delete the pod

Let's delete the pod and deploy it again to validate that the file persisted.

    kubectl delete -f pod.yaml --force --grace-period=0

## Deploy the pod again

    kubectl apply -f pod.yaml

## Connect to the Busybox instance

    kubectl exec mybox -it -- /bin/sh
    cd demo
    ls
    cat hello.txt
    exit

## Cleanup

    kubectl delete -f pod.yaml  --force --grace-period=0
    kubectl delete -f pvc.yaml
    kubectl delete -f pv.yaml


[More info...](https://kubernetes.io/docs/concepts/storage/volumes/)