# T17-01 Helm

*Helm is the best way to find, share, and use software built for [Kubernetes.](https://kubernetes.io/)*


## Prerequisites

1. A Kubernetes cluster.
2. Deciding what security configurations to apply to your installation, if any.
3. Installing and configuring Helm

## Install Helm

Now from the official "[Installing Help](https://helm.sh/docs/intro/install/)" guide, we are going to use the windows install via chocolate:

    choco install kubernetes-helm

Once installed ask helm for the installed version:

    helm version 

    version.BuildInfo{Version:"v3.18.1", GitCommit:"f6f8700a539c18101509434f3b59e6a21402a1b2", GitTreeState:"clean", GoVersion:"go1.24.3"}


## Initialize a Helm Chart Repository

Once you have Helm ready, you can add a chart repository. Check [Artifact Hub](https://artifacthub.io/packages/search?kind=0) for available Helm chart repositories.

> Note: If you installed the Metrics Serve you should have already some repos installed under Helm, so list them, if not add the nex one:

 ```
 helm repo add bitnami https://charts.bitnami.com/bitnami
 ```

Once this is installed, you will be able to list the charts you can install:
```
helm search repo bitnami
```

In my case my repos was corrupted :O. lets fix it !!

*helm search repo bitnami
WARNING: Repo "bitnami" is corrupt or missing. Try 'helm repo update'*

```
helm repo update
```
The output:
```sh
helm repo update               
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "kubernetes-dashboard" chart repository
...Successfully got an update from the "bitnami" chart repository
Update Complete. ⎈Happy Helming!⎈
```

Now we can run the search over bitnami repo and will see a lot of charts

```sh
helm repo list                 
NAME                    URL
bitnami                 https://charts.bitnami.com/bitnami
kubernetes-dashboard    https://kubernetes.github.io/dashboard/
```

Now lets create a Namesapce called dev and lets sitch to it:

```sh
kubectl create ns dev
kubectl get ns
kubectl config set-context --current --namespace=dev
```
## Get the pods

    kubectl get pods

## Install an Example Chart

```sh
helm install bitnami/mysql --generate-name

```
In the output we can see a flag called: REVISION
```text
NAME: mysql-1750260840
LAST DEPLOYED: Wed Jun 18 09:34:04 2025
NAMESPACE: dev
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: mysql
CHART VERSION: 13.0.2
APP VERSION: 9.3.0
```
Lets list what we installed
```sh
helm list
```
Nice and cool we got it ! our 1th helm install.

If we list the pods we can see it there, runnin:
```sh
 kubectl get pod
 ```

Now lets uninstall it using the past output command taking the NAME field, in my case:

```sh
helm uninstall mysql-1750260840
```

Reading the Help Test
```sh
helm get -h
```

Lets clean up:
```
kubectl get ns
kubectl config set-context --current --namespace=default
kubectl delete ns=dev

```

And we are done with a small part of how to use Helm.