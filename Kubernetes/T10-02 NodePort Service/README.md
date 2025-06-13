# T10-02 The NodePort

*if you set the type field to NodePort, the Kubernetes control plane allocates a port from a range specified by --service-node-port-range flag (default: 30000-32767).*

*Each node proxies that port (the same port number on every Node) into your Service.*

*Your Service reports the allocated port in its .spec.ports[*].nodePort field.*

Using a NodePort gives you the freedom to set up your own load balancing solution, to configure environments that are not fully supported by Kubernetes, or even to expose one or more nodes' IP addresses directly.


Let's expose a deployment using a Nodeport service.

## Deploy the app

    kubectl apply -f deploy-app.yaml

## Deploy the NodePort service

    kubectl apply -f nodeport.yaml

## Get the pods list

    kubectl get pods -o wide

## Use the nodeport

Since we are using Docker Desktop and that the Docker Desktop node is mapped to localhost, to reach the service you need to use **localhost** + the **nodeport**.

When using a Cloud provider, you would need to get a node IP address instead of localhost.

Get the node public IP address

    kubectl get nodes -o wide

## Cleanup

    kubectl delete -f nodeport.yaml
    kubectl delete -f deploy-app.yaml

[More info...](https://kubernetes.io/docs/concepts/services-networking/service/#type-nodeport)