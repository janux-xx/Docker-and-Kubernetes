# T13-01 The Secrets

*A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image.*

>Using a Secret means that you don't need to include confidential data in your application code.

*Because Secrets can be created independently of the Pods that use them, there is less risk of the Secret (and its data) being exposed during the workflow of creating, viewing, and editing Pods.*

*Kubernetes, and applications that run in your cluster, can also take additional precautions with Secrets, such as avoiding writing sensitive data to nonvolatile storage.*

Secrets are similar to [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/) but are specifically intended to hold confidential data.

>Caution:

>Kubernetes Secrets are, by default, stored unencrypted in the API server's underlying data store (etcd). Anyone with API access can retrieve or modify a Secret, and so can anyone with access to etcd. Additionally, anyone who is authorized to create a Pod in a namespace can use that access to read any Secret in that namespace; this includes indirect access such as the ability to create a Deployment.

>In order to safely use Secrets, take at least the following steps:
> 1. Enable Encryption at Rest for Secrets.
> 2. Enable or configure RBAC rules with least-privilege access to Secrets.
> 3. Restrict Secret access to specific containers.
> 4. Consider using external Secret store providers.

For more guidelines to manage and improve the security of your Secrets, refer to [Good practices for Kubernetes Secret](https://kubernetes.io/docs/concepts/security/secrets-good-practices/)s.


> Let's start !

To quickly encode/decode strings into base64

    https://www.base64encode.org/
    https://www.base64decode.org/

or on Windows, install base64

    choco install base64

on Linux/Mac

    echo [string] | base64
    echo [encodedString] | base64 -d

## Create the Secrets

    kubectl apply -f secrets.yaml

## Look at the secrets

    kubectl get secret
    kubectl describe secret secrets
    kubectl get secret secrets -o YAML

## Deploy the pod

    kubectl apply -f pod.yaml

## Connect to the Busybox

    kubectl exec mybox -it -- /bin/sh

## Display the USERNAME and PASSWORD env variables

    echo $USERNAME
    echo $PASSWORD
    exit

## Cleanup

    kubectl delete -f secrets.yaml
    kubectl delete -f pod.yaml --force --grace-period=0


[More info...](https://kubernetes.io/docs/concepts/configuration/secret/)