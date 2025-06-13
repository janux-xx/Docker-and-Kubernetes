# T08-04 The DaemonSet

*A DaemonSet defines Pods that provide node-local facilities. These might be fundamental to the operation of your cluster, such as a networking helper tool, or be part of an add-on.*

A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected. 

Deleting a DaemonSet will clean up the Pods it created.

Some typical uses of a DaemonSet are:

* running a cluster storage daemon on every node
* running a logs collection daemon on every node
* running a node monitoring daemon on every node

In a simple case, one DaemonSet, covering all nodes, would be used for each type of daemon. A more complex setup might use multiple DaemonSets for a single type of daemon, but with different flags and/or different memory and cpu requests for different hardware types.*

Let's deploy a Busybox as a DaemonSet.

## Create the Deployment

    kubectl apply -f daemonset.yaml

## Get the pods list

There should be one for each worker node.

    kubectl get pods --selector=app=daemonset-example -o wide

## Cleanup

    kubectl delete -f daemonset.yaml

[More info...](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)