# T05-02 Declarative way vs Imperative way

Let's deploy an Nginx container using both methods.

## Imperative: The shell way "typing it !!"

    kubectl create deployment mynginx1 --image=nginx

## Declarative: The elegance of crete a yaml file and call it !!

    kubectl create -f deploy-example.yaml

## Cleanup

    kubectl delete deployment mynginx1
    kubectl delete deploy mynginx2