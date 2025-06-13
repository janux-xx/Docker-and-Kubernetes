# T05-04 The Nodes

*A node may be a virtual or physical machine, depending on the cluster. Each node is managed by the control plane and contains the services necessary to run Pods.*

## Get nodes information

Get a list of all the installed nodes. Using Docker Desktop, there should be only one.

    kubectl get nodes

Get some info about the node.

    kubectl describe node



[More info...](https://kubernetes.io/docs/concepts/architecture/nodes/)