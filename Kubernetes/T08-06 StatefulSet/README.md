# T08-06 The StatefulSet

*A StatefulSet runs a group of Pods, and maintains a sticky identity for each of those Pods. This is useful for managing applications that need persistent storage or a stable, unique network identity.*

StatefulSet is the workload API object used to manage stateful applications.

Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.

Like a Deployment, a StatefulSet manages Pods that are based on an identical container spec. Unlike a Deployment, a StatefulSet maintains a sticky identity for each of its Pods. 

These pods are created from the same spec, but are not interchangeable: each has a persistent identifier that it maintains across any rescheduling.

Let's now create a StafulSet.

## Create the Deployment

    kubectl apply -f statefulset.yaml

## Get the pods list

    kubectl get pods -o wide

## Get a list of the PersistentVolumes Claims

    kubectl get pvc

## Create a file in nginx-sts-2

Open a session in nginx-sts-2 and create a file in the folder mapped to the volume.

    kubectl exec nginx-sts-2 -it -- /bin/sh
    cd var/www
    echo Hello > hello.txt

## Modify the default Web page

    cd /usr/share/nginx/html
    cat > index.html
    Hello
    Ctrl-D
    exit

## Open a session in nginx-sts-0 and reach nginx-sts-2

    kubectl exec nginx-sts-0 -it -- /bin/sh
    curl http://nginx-sts-2.nginx-headless
    exit

## Delete pod 2

Delete a pod and watch as it is recreated with the same name.

    kubectl delete pod nginx-sts-2

## Is the file still there?

Open a session in nginx-sts-2 and see if the file is still present.

    kubectl exec nginx-sts-2 -it -- /bin/sh
    ls var/www
    exit

## Cleanup

    kubectl delete -f statefulset.yaml
    kubectl delete pvc www-nginx-sts-0
    kubectl delete pvc www-nginx-sts-1
    kubectl delete pvc www-nginx-sts-2


[More info...](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)