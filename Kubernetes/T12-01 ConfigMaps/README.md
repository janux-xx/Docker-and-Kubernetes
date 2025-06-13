# T12-01 The ConfigMaps

*A ConfigMap is an API object used to store non-confidential data in key-value pairs.*

*Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.*

A ConfigMap allows you to decouple environment-specific configuration from your container images, so that your applications are easily portable.

>Caution:

>ConfigMap does not provide secrecy or encryption. If the data you want to store are confidential, use a Secret rather than a ConfigMap, or use additional (third party) tools to keep your data private.


## Create the ConfigMap

    kubectl apply -f cm.yaml

## Get the ConfigMap info

    kubectl get cm
    kubectl describe configmap cm-example

Let's output the same information in YAML format

    kubectl get configmap cm-example -o YAML

## Deploy the pod

    kubectl apply -f pod.yaml

## Connect to the Busybox

    kubectl exec mybox -it -- /bin/sh

## Display the CITY env variable

    echo $CITY
    exit

## Cleanup

    kubectl delete -f cm.yaml
    kubectl delete -f pod.yaml --grace-period=0 --force


[More info...](https://kubernetes.io/docs/concepts/configuration/configmap/)