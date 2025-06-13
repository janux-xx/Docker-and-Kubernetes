# T10-03 The Load Balancer

*On cloud providers which support external load balancers, setting the type field to LoadBalancer provisions a load balancer for your Service.*

*The actual creation of the load balancer happens asynchronously, and information about the provisioned balancer is published in the Service's **.status.loadBalancer** field.*


Let's expose a deployment using a Load Balancer service, locally using Docker Desktop.

## Deploy the app

    kubectl apply -f deploy-app.yaml

## Deploy the Load Balancer service

    kubectl apply -f loadbalancer.yaml

## Get the pods list

    kubectl get pods -o wide

## Use the Load Balancer

Since we are using Docker Desktop and that the Docker Desktop node is mapped to localhost, to reach the service you need to use **localhost**.

When using a Cloud provider, you would need to get a Load Balancer external IP address instead of localhost.

Get the load balancer public IP address. This will output **localhost** on Docker Desktop.

    kubectl get svc -o wide

## Cleanup

    kubectl delete -f loadbalancer.yaml
    kubectl delete -f deploy-app.yaml






[More info...](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)