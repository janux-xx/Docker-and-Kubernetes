# T10-01 The Service ClusterIP

*In Kubernetes, [Services](https://kubernetes.io/docs/concepts/services-networking/service/) are an abstract way to expose an application running on a set of Pods.*

*[Services](https://kubernetes.io/docs/concepts/services-networking/service/) can have a cluster-scoped virtual IP address (using a Service of type: ClusterIP). Clients can connect using that virtual IP address, and Kubernetes then load-balances traffic to that Service across the different backing Pods.*

## Deploy the service

    kubectl apply -f clusterip.yaml

## Deploy the app

    kubectl apply -f deploy-app.yaml

## Deploy Busybox

    kubectl apply -f pod.yaml

## Get the pods list

    kubectl get pods -o wide

## Connect to the BusyBox container

    kubectl exec mybox -it -- /bin/sh

## Get the Nginx home page thru the ClusterIP service

    wget -qO- http://svc-example:8080
    exit

## Cleanup

    kubectl delete -f clusterip.yaml
    kubectl delete -f deploy-app.yaml
    kubectl delete -f pod.yaml --grace-period=0 --force

[More info...](https://kubernetes.io/docs/concepts/services-networking/cluster-ip-allocation/)