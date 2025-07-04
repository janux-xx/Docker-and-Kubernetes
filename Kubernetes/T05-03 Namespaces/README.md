# T05-03 The Namespaces

*Provides a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces. Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc.) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc.).*


## Get namespaces

Open a terminal and get the currently configured namespaces.

    kubectl get namespaces
    kubectl get ns

## Get the pods list

Get a list of all the installed pods.

    kubectl get pods

You get the pods from the default namespace.  Try getting the pods from the docker namespace.  You will get a different list.

    kubectl get pods --namespace=kube-system
    kubectl get pods -n kube-system

## Change namespace

Change the namespace to the docker one and get the pods list.

    kubectl config set-context --current --namespace=kube-system

## Get the pods

    kubectl get pods

## Now change back to the default namespace

    kubectl config set-context --current --namespace=default
    kubectl get pods

## Create and delete a namespace

    kubectl create ns [name]
    kubectl get ns
    kubectl delete ns [name]


[More info...](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)